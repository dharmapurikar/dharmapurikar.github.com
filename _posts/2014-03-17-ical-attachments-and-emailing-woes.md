---
layout: post
title: "iCal attachments and emailing woes"
description: ""
categories:
- Articles
- Programming
tags: 
- programming 
- php 
- symfony
- iCalcreator
- iCal
---

Calendar notifications are becoming more common in collaborative applications. Scheduling systems are easy to build but difficult to integrate as there are large number of clients and service providers. Our product went through a painful time regarding integrating with various email clients and online services regarding iCalendar integration.

This series of posts is going to make sure, I document them for anybody who is facing similar problems. If you have any questions regarding specifics, I will be happy to respond on a stackoverflow question or comment below.

I am not going to create a HOW-TO list of articles here - but document things I bumped against. So if you're looking for a detailed tutorial, you'll need to research on your own.

### Brief about our solution
Our application is built on PHP 5.4 + Symfony 1.4. We are using [iCalcreator](http://kigkonsult.se) library for the generation of iCal files. In my research, this is the most comprehensive standard compliant library out there for PHP. It supports RFC2445 and RFC5545. If you're on PHP platform and looking for iCal generating library, you're search ends here.

Our calendar system generated events between only two parties; organiser and attendee. So the event generation is pretty straightforward. We generate iCal files and just dispatch as attachment. Fairly simple. Still I managed to bump against couple of nasty issues on the way.

### Issue 1 - Email clients won't welcome us

iCal files are creates a tricky issue for client compatibility. You can respond to users of your website depending upon their environment. You can define custom CSS classes, generate responses based on browser, location etc. When you're dealing with iCal files, you don't get to do any of that. Your file is attached and you let the chips fall wherever they might be. So there is no alternative to extensive testing with various browsers, email clients and email service providers. Our focus was on -

* Microsoft Exchange, Outlook (Desktop), Outlook Web Access (OWA) with version 2007, 2010, 2013
* Thunderbird with iCal plugin
* Google Mail
* Yahoo Mail
* Outlook.com

These clients provided a broad spectrum of variation which gives us enough comfort in our solution. 

We wanted email clients to recognise calendar emails and show action buttons to respond to the event. Usually you'll see "Yes", "Maybe" or "No" buttons with additional context information in a special bar by these email clients.

Our emails were not able to achieve this feature. We investigated a lot but didn't happen. My investigations told me you'll need to do few things while attaching iCal file to email before clients will recognise it. These were -

* Email body header should be "multipart/alternative"
* Optionally attach the ics file as well.
* Attach iCal file to email with following specifications -
	* Encoding base64 or 7-bit
	* Content type "text/calendar"
	* Header parameter "method=REQUEST"

For Swift mailer sample code might be like this -

	$messageObject = Swift_Message::newInstance();
	$messageObject->setContentType("multipart/alternative");
	$messageObject->addPart("Email message body goes here", "text/html");

	$messageObject->setSubject("Subject line goes here")
	  ->setFrom("Sachin Dharmapurikar");

	$messageObject->setTo(array('johnsmith@example.com'));
	$ics_content = file_get_contents("/tmp/sample.ics");
	$ics_attachment = Swift_Attachment::newInstance()
	  ->setBody(trim($ics_content))
	  ->setEncoder(Swift_Encoding::get7BitEncoding());
	$headers = $ics_attachment->getHeaders();
	$content_type_header = $headers->get("Content-Type");
	$content_type_header->setValue("text/calendar");
	$content_type_header->setParameters(array(
	  'charset' => 'UTF-8',
	  'method' => 'REQUEST'
	));
	$headers->remove('Content-Disposition');
	$messageObject->attach($ics_attachment);

	$mailObject = Swift_Mailer::newInstance($transportObject);
	$mailObject->send($messageObject);
	
If you look carefully, the message is marked with headers appropriately and the ical attachment is inline rather than as file. 

If you look at the source of email generated with above type of code -

	Delivered-To: johnsmith@example.com
	Received: by 10.220.78.135 with SMTP id l7csp244293vck;
	        Thu, 13 Mar 2014 04:04:02 -0700 (PDT)
	X-Received: by 10.224.151.130 with SMTP id c2mr1291334qaw.67.1394708642049;
	        Thu, 13 Mar 2014 04:04:02 -0700 (PDT)
	Return-Path: <00000144bb1cf5e9-fd06-4945-b4fc-386af484b339-000000@amazonses.com>
	Received: from a8-35.smtp-out.amazonses.com (a8-35.smtp-out.amazonses.com. [54.240.8.35])
	        by mx.google.com with ESMTP id f6si1004430qap.152.2014.03.13.04.04.01
	        for <johnsmith@example.com>;
	        Thu, 13 Mar 2014 04:04:02 -0700 (PDT)
	Received-SPF: pass (google.com: domain of 00000144bb1cf5e9-fd06-4945-b4fc-386af484b339-000000@amazonses.com designates 54.240.8.35 as permitted sender) client-ip=54.240.8.35;
	Authentication-Results: mx.google.com;
	       spf=pass (google.com: domain of 00000144bb1cf5e9-fd06-4945-b4fc-386af484b339-000000@amazonses.com designates 54.240.8.35 as permitted sender) smtp.mail=00000144bb1cf5e9fd06-4945-b4fc-386af484b339-000000@amazonses.com
	Return-Path: 00000144bb1cf5e9fd06-4945-b4fc-386af484b339-000000@amazonses.com
	Message-ID: <00000144bb1cf5e9fd06-4945-b4fc-386af484b339-000000@email.amazonses.com>
	Date: Thu, 13 Mar 2014 11:04:01 +0000
	Subject: Calendar appointment
	From: Support <noreply@serviceprovider.com>
	To: johnsmith@example.com
	MIME-Version: 1.0
	Content-Type: multipart/mixed;
	 boundary="_=_swift_v4_1394708669_02698d0808f167b864966fe96816eec3_=_"
	X-SES-Outgoing: 2014.03.13-54.240.8.35


	--_=_swift_v4_1394708669_02698d0808f167b864966fe96816eec3_=_
	Content-Type: multipart/alternative;
	 boundary="_=_swift_v4_1394708669_9fe42676490416322d81ca192ce8c5f7_=_"


	--_=_swift_v4_1394708669_9fe42676490416322d81ca192ce8c5f7_=_
	Content-Type: text/html; charset=utf-8
	Content-Transfer-Encoding: quoted-printable

	<div>Hello World!</div>

	--_=_swift_v4_1394708669_9fe42676490416322d81ca192ce8c5f7_=_--


	--_=_swift_v4_1394708669_02698d0808f167b864966fe96816eec3_=_
	Content-Type: text/calendar; charset=UTF-8; method=REQUEST
	Content-Transfer-Encoding: 7bit

	BEGIN:VCALENDAR
	VERSION:2.0
	PRODID:-//Service Provider Inc//NONSGML kigkonsult.se iCalcreator 2.18//
	CALSCALE:GREGORIAN
	METHOD:REQUEST
	X-WR-TIMEZONE:America/New_York
	BEGIN:VEVENT
	UID:20140313T070425EDT-3998irwScV@Service Provider Inc
	DTSTAMP:20140313T110425Z
	ATTENDEE;CUTYPE=INDIVIDUAL;ROLE=REQ-PARTICIPANT;PARTSTAT=ACCEPTED;RSVP=TRUE
	 ;CN=John Smith:MAILTO:johnsmith@example.com
	ATTENDEE;CUTYPE=INDIVIDUAL;ROLE=REQ-PARTICIPANT;PARTSTAT=NEEDS-ACTION;RSVP=
	 TRUE;CN=Jane Smith:MAILTO:janesmith@example.com
	DESCRIPTION:
	DTSTART:20140316T103000
	DTEND:20140316T110000
	LOCATION:Meeting venue
	ORGANIZER:MAILTO:johnsmith@example.com
	SEQUENCE:0
	SUMMARY:Meeting about discussion of future
	END:VEVENT
	END:VCALENDAR

	--_=_swift_v4_1394708669_02698d0808f167b864966fe96816eec3_=_--

This works with all the popular email clients. This was the first problem we encountered.

### Issue 2 - Despite of writing above code, email clients still didn't respect us

Now thats a bummer. I spent lot of time and made sure that all the required parameters are satisfied but still no luck with showing calendar invitations properly. Spent lot of time reading original messages sent to the users and figured out that the email headers and everything is stripped out by our vendor.

Our email sending API vendor used to parse message and headers, and convert them to generic message for god knows reasons. Then I decided to switch email sending API from current vendor to Amazon SES. SES allows you to send raw messages which makes life extremely easy. That solved our problem completely.

So if you're using above code and your email headers are not appearing correctly, try a different way to send your email. It might work for you.

Most of the modern email service providers allow you read the source of the email received. Keep checking that for the headers. That is incredebly helpful.

### Issue 3 - Occasionly our users received error in Outlook

Some of outlook users started receiving "not supported calendar attachment.ics" attachment with the emails. This was weird as nobody else receive this error. 

Again, I started investigating this issue and figured out that there is some issue with RRULE directive in Outlook if the iCal file is created from specific clients e.g. Lotus Notes. Our case didn't have that issue as we don't deal with RRULE (recurring appointments) or using Lotus Notes to generate iCal files.

Later I figured out that due to a bug in our code, we were occasionly sending 0 byte attachments. This was treated like no attachment in modern email clients but Outlook gave this error message to the users. 

### Issue 4 - Outlook used to show 3-4 hour differences in meeting timings

This one was the most weird issue I faced. Google, iCal on mac or Yahoo used to show correct meeting timings but Outlook used to show timings with 3-4 hour time difference. This one was a huge problem. 

{% include JB/setup %}
