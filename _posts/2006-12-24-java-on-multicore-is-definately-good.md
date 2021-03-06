--- 
layout: post
title: "Java on Multicore: Is definately good!"
categories: 
- Developer
- Java
tags:
- performance
- java
status: publish
type: post
published: true
meta: 
  dsq_thread_id: "421059806"
---
This is another new discussion topic in Java circle. To get the background for this post you would like <a href="http://www.devwebsphere.com/devwebsphere/2006/11/multicore_may_b.html">this</a> good article. This post has some great comments so don't miss that either. Followed by <a href="http://dev2dev.bea.com/blog/hstahl/archive/2006/12/multicore_is_go.html">this</a> and <a href="http://www.infoq.com/news/2006/11/multi-core-java">this</a> article. There are different opinions about the topic. I studied Parallel computing &amp; architecture as my graduate studies. So I would like to poke my nose in this topic. ;)

This discussion is circling around GC threads and JavaEE threading model. Although experienced bloggers have already touch length and breadth of the topic, I would like to express my view in this regard. Operating system designers and architects thought a lot about Uniprocessor and Multiprocessor execution methods. There is huge literature present on these topics on public sources. But multicore techniques are relatively new.

Java scales very well on multi-processor servers from long time. Since multi-core is similar to multiprocessor in great sense, there should be increase in performance. Although as Billy mentioned there is GC bottleneck but, that is something can be worked out through JVM only. If JVM can utilize different processor for GC then why not different core?

In addition to that, there are very sophisticated parallel computing algorithms and utilities which may increase the performance by re-writing the existing application or designing new applications to work better on multi-core architectures.

This problem can be worked out and not impossible. If Java is having problem so do all the other monolithic applications which were designed by keeping in mind uniprocessor / unicore architectures.

And there is always option to use libraries like <a href="http://www.pervasivedatarush.com/">Pervasive Datarush</a> and <a href="http://javolution.org/">Javolution</a> to increase application performance without bothering about details of architectures :)
