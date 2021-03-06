--- 
layout: post
title: Don't put JavaScript validation, I'll Firebug!
categories: 
- Developer
tags:
- javascript
- programming
status: publish
type: post
published: true
meta: 
  _edit_last: "2"
  dsq_thread_id: "420852028"
---
Recently, I was with my friend to book a cab. The cab service provided an online booking facility which allows you to provide some details (phone number, address, destination and time of cab etc.). We went ahead and tried to book the cab and it wasn’t accepting the request. It seemed that they put a validation to check that user shall not book a cab less than 4 hours prior to departure.

Unfortunately, we wanted to book the cab on a 3 hours notice and it was mandatory for us to book the cab.  We couldn’t resist but started looking for options at our hand. We pulled the website in Firefox and opened firebug to see where the validation is executed. We were surprised by the validation was done in browser using a very simple JavaScript. We thought; let’s see if we could just pass the 4 hours validation by bypassing the validation or maybe mocking the action. The validation code was very simple; we just put the breakpoint in the function and then set the variable value via firebug to an acceptable level. Bang! The code ran successfully and cab service accepted the request.

We made a successful cab reservation and my friend could take a peaceful ride back home!  Moral of the story: Please put all the business critical validations on the server side instead of browser based JavaScript. If you really want to do some browser based validation then it will be really good idea to <a href="http://en.wikipedia.org/wiki/Obfuscated_code" title="Obfuscate the code">obfuscate</a> the code.
