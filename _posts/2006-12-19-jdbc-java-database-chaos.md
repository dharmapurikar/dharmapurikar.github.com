--- 
layout: post
title: "JDBC: Java DataBase Chaos"
categories: 
- Developer
- Java
- Programming
tags:
- jdbc
- programming
- chaos
status: publish
type: post
published: true
meta: 
  dsq_thread_id: "421060592"
---
"Write once run everywhere!” this tagline has won many developers. Java has been there for more than a decade and I love the way it ports itself to various platforms with little or no platform specific code. But, when it comes down to JDBC I feel like loosing my patience. We recently wrote a Database specific layer for our application, and that took lots of energy and time of my team. We first analyzed the behavior of different databases, their error codes and then code specific handling.

When, Java seamlessly works with multiple operating systems, what happens to that when it comes to JDBC? For any exception or error it only throws "SQLException" and a long database specific error code and message string.

I find it very common to encounter ColumnNotFound, DuplicateKey, IncompatibleDataType and similar exceptions in my application.  Since, my application is designed to handle data at runtime; we are not having control over strict scrutiny of the data to check compatibility. If we do that, it will consume our lot of bandwidth to check input query data against dynamically generated table structures. So we directly push incoming data traffic to database without any strict checking. This leads to 98% hit ratio of proper insertion which saves our lot of processing power as well code efforts. To handle different kinds of errors we have inherited our custom exception hierarchy which wraps SQLException object. This way we always get proper exceptions and the design remains easy to understand.

So far there seems no problem, the real problem starts when we try to make our application compatible with other databases. We have to study each exception or error codes, their messages and other tons of database specific information which seems pretty difficult to manage. Although rare but if any database vendor changes an error code our whole application is for toss and we are forced to run a rigorous test cycle to ensure integrity and working of application!

This becomes very difficult if we are supporting large number of databases. So I was wondering, instead of hundreds of database specific error codes why JDBC doesn't cover exception hierarchy. Then database vendors have liberty to use their error codes while making implementation of JDBC driver generic. Since complete JDBC exception hierarchy will be arranged in similar to IOException, if any user doesn’t want to catch granular exceptions they are free to use generic SQLExceptions.

This will surely help me to chop my code size by 1.5 K of lines :)

