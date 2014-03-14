--- 
layout: post
title: "Ubuntu: Will Skype jingle?"
tags: 
- skype
- linux
- ubuntu
- voice chat
categories:
- Linux
status: publish
type: post
published: true
meta: 
  dsq_thread_id: "421048324"
---
Skype 2.0 beta has arrived for Linux. I read about this <a href="http://linux.wordpress.com/2007/11/08/skype-20-beta-for-linux-now-with-video-support/">here</a>. I have been trying to get Google Talk support for Linux for a while. I tried that in PLUG <a href="http://plug.org.in/mashup/">mashup</a> event. So summary of what I did was as follows:

<em><strong>What I wanted to achieve?</strong></em>

I wanted to integrate support for voice chat using Pidgin for Google talk users.

<em><strong>What we did?</strong></em>

We started with analysis of <a href="http://code.google.com/apis/talk/libjingle/index.html">libjingle</a> which is xmpp based communication library from Google code. We faced lots of problems in integrating that as a plugin with Pidgin. I could see that there is already a feature request logged with  Pidgin for this support. I tried to work with Ubuntu (Gutsy Gibbon). There were many problems for libraries which are either very old or sometimes difficult to maintain.

There are many issues with the library dependencies of libjingle as well, viz. linphone, gstreamer etc. Each of them require different version which is sometimes quite old than the current stable version.

I will be working on this more to achieve the goal. There seems to be quite few huddles before I could reach there though. I don't know what is current state of this <a href="http://labnol.blogspot.com/2006/08/skype-users-can-connect-to-google-talk.html">post</a>. I am hoping this will start working soon. Till then, I'm there to see how I can add the talk plugin to pidgin.
