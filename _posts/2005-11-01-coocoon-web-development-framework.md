--- 
layout: post
title: Coocoon - Web Development Framework
categories: 
- Developer
- Programming
tags:
- cocoon
status: publish
type: post
published: true
meta: 
  dsq_thread_id: "420850848"
---
I would like to go with Cocoon for my first post on this blog. My first encounter with Cocoon happened, when I was in design of a web based application. I wanted a simple framework which doesn't hogs much server side resources and gives me ability of a very dynamic and configurable web application.

I saw into Cocoon and the concept of Pipeline appealed me a lot. Its really like a assembly line, you can see your content is fetched by business logic, serialized to various forms, transformed to various formats and finally published over web. More to it, you can customize the way pipeline behaves. By just modifying a simple XML you can change the complete behaviour of the pipeline.
Thats complete other story that I couldn't fit the framework in my needs as I was needing more than just a web-development framework. But there were few things which I wanted to highlight about cocoon:

* Continuation: Cocoon gave me ability to use the continuatoin in the web pages, this is a ability which I needed from many days, but I was not knowing somebody has already implemented it. This is something like you write and execute a function.
	
	There is a excellent information on what is continuation in cocoon on this page. Just <a href="http://cocoon.apache.org/2.1/userdocs/flow/continuations.html">click here.</a>

* Content-Logic Seperation: This is something which was tried many times before but very few people got success into it. You write your logic somewhere else into java classes or something you like. Configure your control flow and thats it. You are ready to transform your output into the way you like. It allows to you to seperate the view tier completely from the business logic. You generate one output from the business logic. Convert it into XML (well nowdays cocoon has many inbuilt serializers for many interfaces.

Ending up the list here is unfair with cocoon. You may like to visit and see the actual product and its features on <a href="http://cocoon.apache.org/2.1/userdocs/concepts/index.html">here.</a>

All in all, another excellent product from Apache. I know after reading the list hardly you can resist to download and try it.
