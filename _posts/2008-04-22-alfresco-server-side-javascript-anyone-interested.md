--- 
layout: post
title: "Alfresco: Server side JavaScript, anyone interested?"
categories: 
- Developer
- Java
- Programming
tags:
- alfresco
- javascript
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  dsq_thread_id: "420852051"
---
I started with <a title="Visit Alfresco" href="http://www.alfresco.com">Alfresco</a> and its amazing software suite. For people, who don't know about content repositories, in short its hierarchical, versionable storage (read <a href="http://en.wikipedia.org/wiki/Content_repository_API_for_Java"> more</a>). Alfresco is one step ahead of other content repository implementations and it is full content management suite. This means, you have workflow, content repository and a portal which allows you to do lot of standard things e.g. communicating with external world via API, portal, security/authentication etc. From my perspective Alfresco is really great product considering the amount of features it provides and the quality of them.

I am working on a project which involves some bit of alfresco customization to meet the customer needs. This involves configuring alfresco for Windows SSO, allowing users to map their home space in alfresco as network share, knitting a workflow tightly integrated with their business process and writing some dynamic content generation code for reporting, user interaction and for auditing purpose. We could do most of the things straight away and we are quite happy with kind of response alfresco was giving. Everything is clean and configurable. Basically alfresco is built using spring framework; so you can configure custom beans or extend existing beans very easily via some xml files. There are tons of different services and pre-configured beans which might be little overwhelming for the beginners but, as you started to get familiar it doesn't feel so bad.

We were at a point where we wanted to write some server side logic to create a dynamic (web 2.0) UI which has lot of interaction based on data queries with content repository. So we needed easy approach to query repository, minimal xml configuration, ability to change / update logic easily, faster development cycle to start with. Alfresco provides lot of options to communicate to repository -

* Java API (most raw access to the repository, repository instance is singleton so that will be injected as dependency via spring configuration)
* Web Service - Very standard SOAP and XML RPC based communication
* RMI - Java RMI which is another standard method looks similar to Web Services
* RESTful JavaScript API :)

I was excited by last option the most. I thought, lets explore the last one as first three were mundane and I knew what are the pros-cons of most of them. Alfresco provides a clean MVC around content repository and other parts of Alfresco (viz. workflow, user homes and some root objects) where controller is a pre-configured servlet, model is JavaScript code and view is a freemarker template. The beauty of the system is lying in the simplicity of JavavScript code.

Alfresco provides a nice feature rich JavaScript API (more <a href="http://wiki.alfresco.com/wiki/JavaScript_API">here</a>) where some of the objects are injected from scripting engine as root objects. These object provides the building blocks for JavaScript API e.g. search, user home, workflows etc. You can write your own Java services and inject them as root object using simple configuration to extend this foundation. Once your basic services are in place, then you can start knitting or wiring your business logic using these foundation blocks. JavaScript is an ideal choice as it expects small, working code instead of heavy logic which Java can handle. With small fluff of code you will be looking at some fantastic results.

I was amazed and surprised by the simplicity but there are few things which I needed to finalize before I decided to make a choice -


* Performance - JavaScript is interpreted in Alfresco using <a href="http://www.mozilla.org/rhino/&lt;br &gt;&lt;/a&gt;">Rhino</a> which is high performance engine by Mozilla. So, no worries about performance. I have evaluated Rhino some time back and that was really great in performance.
* Testability - That was major concern. Unit testing with JavaScript was not easy. <a href="http://www.thefrontside.net/crosscheck&lt;br &gt;&lt;/a&gt;">Crosscheck</a> is a good choice to begin with. There are other options like <a href="http://www.jsunit.net/">JsUnit</a> and some browser based frameworks which are not that popular.
* Debugging - Alfresco provides a very nice JavaScript debugger where you have luxury of an IDE. Its launched from browser (firefox, IE) and works with ease. Standard debugger features like breakpoints, watches and navigation control are provided.
* Ease of deployment - Most of the scripts are convention based (naming conventions, location conventions etc) and very standard. Server can identify updated scripts and no server restart required (in development environment thats a needed feature)
* Ability to talk to Java logic - If you want to use a external third-party library from JavaScript, no problem! JavaScript code can use API which are written in Java and work with them with ease. You can even write your heavy-weight business logic components in Java and inject that as service to reduce time and achieve code-reuse.

After all concerns are addressed, I was pretty sure I will be writing most of my business logic code and writing the services in JavaScript. I haven't stressed much in this post on view as its pretty standard <a href="http://freemarker.sourceforge.net/">freemarker</a> template engine. I would like to touch upon that later.

If you are considering the Alfresco and writing your business logic in JavaScript (called as Web Scripts in Alfresco) then I would seriously recommend following things for reading/viewing -

* Douglas Crockford — "The JavaScript Programming Language" series of videos (found <a href="http://developer.yahoo.com/yui/theater/&lt;br &gt;&lt;/a&gt;">here</a>)
* Alfresco Developer series - For basic hands-on tutorials for Alfresco customization and understanding (found <a href="http://ecmarchitect.com/alfresco-developer-series/">here</a>)

Have a great time functional programming! :)

