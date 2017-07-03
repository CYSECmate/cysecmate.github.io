---
layout: post
title: Pyramid of Pain for adversaries
published: true
date: 2016-09-26 20:45:35
categories: [Pyramid-Of-Pain, Threat-Intelligence, Indicator-Of-Compromise]
---

{% assign imagedir = "/images/" | prepend: site.baseurl | prepend: site.url   %}

I have read a post written by David Bianco that I found very interesting. I recommend the read [here](http://detect-respond.blogspot.com.au/2013/03/the-pyramid-of-pain.html).

![Pyramid-Of-Pain.JPG]({{ "Pyramid-Of-Pain.JPG" | prepend: imagedir}})  
*(from http://detect-respond.blogspot.com.au/2013/03/the-pyramid-of-pain.html)*


### In summary

The Pyramid of Pain is a way to determine the amount of pain caused to adversaries by an IOC created by your oganisation to block/detect an Intrusion/APT.

As shown on the above picture, more you go up to in the pyramid, more it's complicated for adversaries to find a way to use the same attack.

* __Hash Values__: A hash is considered as unique and a simple byte within the executable will change the hash value. It means that IOC based on hash value is the most accurate but it's also the easiest way for adversaries to keep attacking the organisation.

* __IP addresses__: Easy to change for adversaries (VPN, TOR, Proxy, Etc.). 

* __Domain Names__: More difficult to change than IP address (it can takes couple of days to get a new domain) but it can still be done easily

* __Network & Host Artifacts__: The organisation might have detected the adversaries thanks to a specific User Agent, a specific type of request, etc. Adversaries will need to understand how the company has detected them and then reconfigure/recompile the tool.

* __Tools__: The organisation has created IOCs based on specific tool artefacts. It can be done through AV detection, Yara rules, etc. This kind of detection is very painful for the adversaries since they will need to rewrite the original tool in order to bypass the detection.

* __Tactics, Techniques & Procedures__: This is the top level for the organisation. Indeed, the detection is done on behaviours and not against tools. Adversaries will need to restart from scratch ...
