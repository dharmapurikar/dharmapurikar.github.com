--- 
layout: post
title: "Linux Myth Buster: What is difference in Server and Desktop Linux?"
categories: 
- Articles
- Linux
- Ubuntu
tags:
- linux
- ubuntu
- introduction
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  dsq_thread_id: "420851967"
---
<em>Disclaimer: This article is too long! This was done to explain lots of historical information which lead to this question. If you are not interested, you can skip to ‘Actual answer begins here…’ section.</em>

<h3>Why this question is here?</h3>

Linux has been part of my technical life since 2001. I have seen Red Hat Linux 6.x early releases and fall of Red Hat Linux. Rise of <a href="http://fedoraproject.org/">Fedora</a> and birth of <a href="http://www.ubuntu.org">Ubuntu</a>. This whole journey is very interesting and enjoying in its own way. Linux is today having a position which is not dominating but surely challenging! Linux is not having aim to replace every desktop in the world (… some might say it just can’t!) but surely its putting a smile on people’s faces who have used it for a while. You can’t just put Linux out of the door and wait to disappear, the small tiny tux is now having a great foot tapping parade of people and organizations which will do whatever they need to make this tux growing!

I have been asked a question many times by my friends and colleagues who are new to Linux or just want to learn Linux. They started the question with, “Sachin, I have a stupid question…” this was always one of questions which I answered very religiously. The only reason I never made any nonsense while answering this question was, they were new to Linux and slight wrong answer might put a wrong foundation about Linux Information in their minds. My friend <a href="http://ashlin.wordpress.com/">Ashish</a> suggested me to write a blog post about the same so that, people can get right information.

The question is not at all stupid! In fact, most of people don't know the answer and they hesitate to ask this. I would request you to read the whole post and if you have any suggestion or question feel free to post a comment about it.

In technical terms, Linux is simply a ~2 MB sized binary file which has all (…almost all) the stuff necessary to manage file systems, networks, processes etc. Usually Mandrake, SuSE, Fedora, RHEL and all other popular Linux flavors contain this ~2MB binary acting as heart and soul of their <em>distribution</em>. Remember the italicized word in last sentence; we are going to come back to that word shortly. You can obtain Linux in pure form from Kernel distribution <a href="http://www.kernel.org">site</a>. That’s most pure and raw form of Linux. If you follow all the instructions and put lots of efforts (although targeted audience is not supposed to do that) you might get a text based console at the max!

Remember the word we italicized? <em>Distribution</em>, yes that is a very important term in this world! Since, Linux started way back in 90s and it was free, people started experimenting with it. People wrote tons of applications which could be run on this robust and naive platform. Most of the applications were coming out of university students, startups, research laboratories and programmers who are dying to try new things! This created a huge sea of application, system, utility software which was unmanageable. Clearly, an effort to make Linux easily adoptable was necessary. This problem lead to a solution called as <strong>Distribution</strong>. The idea was great because of its simplicity. People started delivering Linux along with few <em>must have</em> software nicely wrapped around with a GUI and installer. This contained system, utility, programming, internet and other software categories. A beginner had all things nicely wrapped which were needed a beginner. Soon, the distribution size exploded from few hundred megabytes to 4-5 gigabytes and the size was growing day by day. Tons of software was coming as part of default bundle which was not at all needed by a normal user. To address this chaos and make Linux more targeted to audience, people started creating their own customized distributions! This lead to Live CD, business, small and large sized distributions! Each distribution was targeted for an audience with considering their need of software and applications. Nothing got changed; still a nice GUI and rock solid base functionality was supported. Each distribution (a.k.a. distro) was addressing a very specific problem. There are around 1000+ distributions available to date at the time of writing this post, refer to (<a href="http://www.distrowatch.com">distrowatch</a>).

<h3>Actual answer begins here…</h3>

Linux was really easy to configure and creating a distribution was real fun, which lead to “<a href="http://plato.stanford.edu/entries/problem-of-many/">Problem of Many</a>”. There were unlimited options and unlimited configurations! This created a great amount of chaos and making impossible for new comers to figure out which one of these 1000+ distributions they can use for day-to-day use or what they should use to install a Linux server. When, any organization was supposed to install a Linux powered web server, a ‘Super’ developer used to spend around a week to either create a really custom version of Linux. This used to be based upon some out-of-box distribution which matches close to their criteria. If this doesn't work out well, organization will pay hefty amount of money to purchase Enterprise Linux from vendors like <a href="http://redhat.com">Red Hat</a> or <a href="http://www.novell.com/linux/">SuSE</a>. Commercial software vendor were giving 24x7 supports and other business terms which were comforting to organization which were new to Linux. Today or another day this was supposed to happen. (Let’s leave the topic here as this might be a good discussion over <a href="http://www.slashdot.org">Slashdot</a>)

In simple terms, Linux is a simple binary. Distributions are nothing but customized suite of application, system software which is solving some business, personal computing problem for most of the cases in ‘out-of-box’ fashion. Server and Desktop versions of distributions are nothing but different set of software packaged together. Yes, that simple it is! Just another distribution might be called Server Linux and others might be called different names as well.

<a href="http://www.ubuntu.org">Ubuntu</a>, <a href="http://www.kubuntu.org">Kubuntu</a> are today’s most popular Desktop versions of Linux distributions (from my perspective). Ubuntu as well releases a server <a href="http://www.ubuntu.com/products/WhatIsUbuntu/serveredition">distribution</a> with same quality of bundling and support.

<h3>What can I expect from a Desktop distribution?</h3>

You can expect all the functions (perhaps much more than that) supported by a Installed and Configured Standard Windows box from a Linux Desktop distribution. This includes E-mail client, Internet Browser (Mozilla Firefox etc.), Media Player, Media Browser, Games (basic), Network support, Office and Productivity suite etc. There are tons of other features coming which you just need to explore.

<h3>What can I expect from a Server distribution?</h3>

If you are planning to host a web server which can run database applications written in PHP or Ruby then perhaps this is the distribution you are looking for. This includes Telnet, SSH, FTP, Web and other remote servers. This includes few server applications which are normally needed by web administrators. In all normal cases you don’t need this distribution as you don’t need most of the applications in your day-to-day basis unless you are geek.

<h4>I am still confused, which one is right for me today? Will I miss something if I choose a wrong distribution today?</h4>

Hell No! There is no such phrase called as ‘can’t happen’ in Linux world! If you choose a desktop or server or for that matter any distribution, you will be able to install any application which can run on Linux. Let us take example of standard desktop distribution of Ubuntu. If you installed the standard 1-CD installation and then want to host a web server, please go ahead. You can always find very nice and friendly applications like ‘Apt’ and ‘Package Manager’ which will help you to install web servers, database server, FTP or SSH servers without typing a single command! You can just click the mouse, make sure you are connected to internet and choose any software from repository of ~25000 applications available for Ubuntu! Doesn’t it sound simple and great? So there is no problem in beginning with any distribution of your choice. There might be few distributions which may not support ‘Apt’ but they might be having some parallel application which does the same job. SuSE have ‘yum’, Red Hat has ‘up2date’ and others have similar tools. You just need to find tool which runs in your distribution.

Thank you for reading a lengthy post. Please help me if there is anything which needs rectification.
