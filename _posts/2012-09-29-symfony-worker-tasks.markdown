---
layout: post
title: "Symfony Worker Tasks"
description: ""
categories:
- Articles
- Programming
tags: 
- programming 
- php 
- symfony
- mysql
---
Every large application needs background worker tasks for sending emails, cleaning up files or archiving content. We are using symfony 1.4 for our current project. In symfony, this can be achieved by creating tasks. Tasks can be created by generator. You can  trigger these using cron, hooked with a queuing system or invoked manually. 

In my experience, writing a symfony task in general is very easy and fun. When you want to run a task for long time, that's tricky! We created a task to send emails asynchronously. Our solution involves three components.

1. **Web Application** this is where we decide to send a notification email. Create email text and then save it in a persistent store. Notify access identifier to RabbitMQ to dispatch using worker.
2. **sfRabbit** this plugin allows to create consumer class, invoked by a symfony task. Each event consumer has a callback. When qualifying event is received, `execute` method of the callback is invoked.
3. **Email Dispatcher** we use Amazon SES for sending emails. We wrote a dispatcher class which handles the responsibility of fetching the content from persistent storage and then dispatch email.

Looks like a simple process which shouldn't be difficult to implement. At least I thought so.

I quickly created a database backed symfony task. It will use doctrine to connect to MySQL and fetch email information, dispatch emails and I can go have a beer. Not so easily.


### Issue 1

After some time, I saw an error message in log file -

    MySQL server has gone away
    
So this means, there was some connection idle for more than `wait_time` configured in MySQL. In my case it was set to 28800 (8 hours). This was long enough duration to hit at least one query. It didn't happen over the night and the task stopped sending emails. Snippet from my task code -

    
    protected function execute($arguments = array(), $options = array())

    $databaseManager = new sfDatabaseManager($this->configuration);

    $connection = $databaseManager->getDatabase($options['connection'])->getConnection();

    // more code with database goes here

    }

When you instantiate `sfDatabaseManager` in symfony task, it will create a connection using provided configuration. This connection will be killed if it idles for `wait_time`. If you kept issuing _ping_ queries, then you don't have that issue. Upon using the connection to query database `wait_time` will keep resetting to 0 and you'll reuse the connection again and again.

This is exactly what happens when symfony is processing a web request. Only 1 connection is opened and that is reused throughout the lifecycle of the request. At the end of the request, the connection is closed and that's how no memory leaks or connection leaks happen.

To tackle this connection getting killed, I just started creating `sfDatabaseManager` every time I received a message. Just like the symfony web request procedure.

    $databaseManager = new sfDatabaseManager($this-&gt;configuration);
    // Use database to do operations
    $databaseMangare->shutdown();

`$databaseManager->shutdown()` is actually supposed to close all the active connections and then shut itself down. Sounds reasonable and worked for me until I hit second issue.

### Issue# 2

That trick worked for a while and I bumped across another MySQL error -

    Too many connections

I was surprised. Database manager is getting shutdown, I debugged code and I saw that each connection is issued `close` call. Why there is database connection leak?! I kept investigating.

What I found was very interesting.

Symfony task used `sfDatabaseManager` to manage database activity. I used doctrine so `sfDatabaseManager` internally used `Doctrine_Manager`. Doctrine uses PDO to finally connect to the database server. I found that right way to manage a PDO connection is simple -

    $dbh = new PDO('mysql:host=localhost;dbname=test', $user, $pass);
    $dbh = null;

Setting a PDO reference to `null` will close the connection. Simple enough.

From documentation -

    Upon successful connection to the database, an instance of the PDO class is returned to your script. The connection remains active for the lifetime of that PDO object. To close the connection, you need to destroy the object by ensuring that all remaining references to it are deleted -- you do this by assigning NULL to the variable that holds the object. If you don't do this explicitly, PHP will automatically close the connection when your script ends.

My interpretation says, you assign `null` to the PDO (which symfony code did) and then PDO will close connection immidiately. If you didn't assign `null` then connection will be held until script ends. This is not how it happens. If you assign `null` it doesn't get freed immediately. When the script ends, that connection will be _actually closed_. Till that time, MySQL will think of it as an idle connection. _Bummer!_

I didn't find any easy way to force close the connection immediately.

### How I solved this issue?

After lot of Googling, reading I didn't find anything which can be used as solution. I had two options:

* **Increase `wait_time`** -- Increasing **wait_time** to something like 72 hours. No matter what happens, I will send 1 email in 72 hours and that will keep the connection alive. I didn't prefer this solution as it will just delay the problem instead of fixing it. This will allow me to use my first solution of instantiating **sfDatabaseManager** only once and keep re-using the connection.

* **Reduce `wait_time` ** -- Reduce `wait_time` and use second solution of creating `sfDatabaseManager` on each message receipt. This is as bad as first solution. Just different approach so I _really_ resisted this solution as well.
	
Finally, I found the solution which is not my favorite but doing the trick --

* Create another task which will carry out _unit_ work for you e.g. in my case sending 1 email. This task will use database connection and will be good for only 1 email processing.
* Make the sfRabbit callback task as lightweight as possible. Just receive message and then invoke the unit worker task using `exec()` function.

### How does it solve the problem?

sfRabbit consumer task will keep running forever, and it will _not_ use any database connections. This allows us not to worry about database connection leaks.

Using `exec()` function it will invoke the unit worker task which actually initiates the `sfDatabaseManager` which will create a connection. Unit worker will be destroyed once the task is carried out. As script ends, PDO will close the connection automatically.

Not the most elegant solution but seems like the only option to me.

{% include JB/setup %}
