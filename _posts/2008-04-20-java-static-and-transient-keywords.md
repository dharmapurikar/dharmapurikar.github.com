--- 
layout: post
title: "Java: static and transient keywords"
categories: 
- Java
- Programming
tags:
- java
status: publish
type: post
published: true
meta: 
  _edit_last: "2"
  dsq_thread_id: "420852016"
---
I came across <code>transient</code> keyword and wanted to get few more details about it. This is one of the most ignored or rarely used keyword by me. It is really funny but, I never really used this keyword extensively. The main reason is, this keyword has a very specific use and most of the applications don't need that for building the business applications. As per info <a href="http://mindprod.com/jgloss/transient.html" title="Transient">here</a>, when any object state is getting serialized, static and transient variables will be ignored for serialization. Still, Java compiler doesn't give any warning or prohibit from making a variable static and transient at the same time. I don't think this as error but a warning should make more sense in this case.
