--- 
layout: post
title: Are we ready for Web 2.0?
tags: 
- ajax
categories:
- Articles
- Programming
status: publish
type: post
published: true
meta: 
  dsq_thread_id: "420850946"
---
Hushhh... last week was a real rough! Got some time to breath and felt to write a post. I am currently developing software which has a web-based application component. We tried to ajaxify it to give better user experience. We did it really well. There is lot of buzz going on since last few months around Ajax. Ajax is going to play a vital role in Web 2.0. In this post I would like to shed some light on Ajax only. Before we go too ahead, what we need to think is, are we **really** ready for this?

Ajax gives a very rich experience to user. Ajax gives richness of web and feel of desktop applications in true sense. While development, I felt that we are not that ready to hit the road. The first and foremost important thing is, the platform which runs the Ajax i.e. browsers are not supporting it natively. If browsers provide a clean abstract level implementation of Ajax then a new developer will not get confused by tons of different frameworks. Instead of number of frameworks, we need native support for Ajax and similar things. That will save lot much efforts of developer and in turn it will allow us to concentrate more on the business logic.

<a href="http://code.google.com/webtoolkit/" title="Google Web Toolkit" target="_blank">GWT </a>(Google Web Toolkit), <a href="http://www.tibco.com/software/ria/gi_resource_center.jsp" title="Tibco GI Home">Tibco GI</a>, <a href="http://www.nextapp.com/platform/echo2/echo/" title="Echo">Echo2 </a>and <a href="http://www.openlaszlo.org/" title="Open Laszlo">Laszlo DHTML</a> are good efforts towards simplyfying the development cycle. Still, Echo2 and Laszlo needs server side runtimes and GWT has better still Java based approach. I will really appreciate if IE or Mozilla support the Ajax just like form handling or any other task in the JavaScript. There shouldn't be any headache to handle responses, marshall / unmarshall the XML etc. XML responses should be handled properly.

The fact still remains that there is huge compatibility issue with JavaScript. <a href="http://www.ecma-international.org/publications/standards/Ecma-357.htm" title="ECMAScript Standards">ECMAScript 4</a> standard is out and I don't know why browsers don't support it. Flex people were successful by implementing the ECMAScript 4 standard natively which supports E4X, the new way to handle xml, and other many powerful features.

Now I am not interested to start any flame war or address to JavaScript machos who will say Ajax is simple though. Still majority of people find it painful and we run into trouble many times.

To be really ready for Web 2.0 we need Web 2.0 ready web-browsers. Instead of handful of frameworks we need native support from browsers. ECMAScript 4 should be supported by all leading browsers. Most of all, I plea to Microsoft for not making their own standard for browsers. That really creates huge application portability issues. If they really want to create own standard then let it be public so that other people can get benefit out of it!

Peace.
