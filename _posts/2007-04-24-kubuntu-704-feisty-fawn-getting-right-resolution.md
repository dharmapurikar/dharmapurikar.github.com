--- 
layout: post
title: Kubuntu 7.04 Feisty Fawn - Getting right resolution
tags: 
- kubuntu
- linux
- ubuntu
categories:
- Linux
status: publish
type: post
published: true
meta: 
  dsq_thread_id: "420851882"
  _edit_last: "1"
---
Yesterday, on first day of vacation, I installed <a href="http://http://www.kubuntu.org/">Kubuntu</a> Feisty Fawn release. This time, I wanted to try something else than Ubuntu. I faced lots of usability issues with Ubuntu. It had some problems in auto detecting my network settings. I use my laptop in various network environments, office, home and public places. I had to every time select the proper network adapter to get running. I never figured out whether there is some other way to do things but out-of-box configuration didn't allow that. There were similar problem on other grounds too.

Kubuntu was amazing in these regards, I plugged my WD passport drive and immediately it shown me the dialog (like windows :) ) to open or view pictures. I liked the way they picked up good features of windows. When I plugged in my network cable, it automatically configured itself to proper device and I had to do nothing except waiting for couple of seconds! So my first impressions of Kubuntu are really good!

I faced only one issue with Kubuntu, getting 1440x990 resolution my Dell Latitude D620. Laptop configuration is as follows:

* Core 2 Duo T7200 CPU (2 64-bit 2.00 GHz processors)
* WXGA+ screen, 1440x900
* NVidia Quadro 110M Turbo Cache
* 1GB RAM
* Integrated bluetooth, usual ports and networking (Wi-Fi etc.)

The problem I faced was, NVidia Quadro 110M has 64 MB onboard memory and it can use shared memory upto 256 MB. Somehow the out-of-box driver with Kubuntu was not able to allocated shared memory which was forcing me to use lower resolution than 1440x900. I hate that resolution as there comes some weird shadow effect around text characters and even the desktop seems to be skewed a little bit.

<a href="http://i71.photobucket.com/albums/i157/dharmapurikar/ThoughtWorker/adept.png"><img class="alignnone" title="Adept" src="http://i71.photobucket.com/albums/i157/dharmapurikar/ThoughtWorker/adept.png" alt="" width="800" height="500" /></a>

I was also facing problem in having widescreen display and was forced to use 4:3 display. I tried to google for the problem but no luck there too. I searched for Adept Installer for "nvidia" and I could see two packages in the "System" category.

I selected the second binary driver (as shown in the image) and applied the changes. Later, I restarted the X-Server by (Ctrl+Alt+Bksp) and I could see the NVidia logo which was sign that the driver is in action. After login, I could go to "System Settings" and in administrator mode, I set my monitor to be "16:9". Then I restarted the X server again. Later I could set the proper resolution to 1440x900 and it needed another restart of X server.

There might be some optimal way of doing that in one restart (e.g. editing the xorg.conf file manually) but I prefer to use wizards whenever possible to avoid syntax errors in the configuration files.

Finally I can use my laptop in 1440x900 resolution. :)
