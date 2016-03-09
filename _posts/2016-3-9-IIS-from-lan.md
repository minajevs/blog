---
layout: post
title: Accessing IIS Express from LAN
---

Today I encountered the need of debugging a web app from external server (located in our companies LAN). The problem is that the Web App is running under local IIS Express, and it should be requested from outer world.

Well, I am actually surprised it doesn't work "from the box". After launching my app from VS I tried accessing it from remote machine in chrome by IP. No success.
![](http://i.imgur.com/uRw1O7s.png)

Funny stuff - it doesn't necessary NOT work. Chrome was endlessly loading the page (Infinite timeout?), but just couldn't show it up. Pings go through, so better check project web configuration. I am (almost) sure I got dmitrijsminajevs/ domain as a DNS for ip, so why not trying replacing localhost with domain? Ofcourse it didn't work.
![](http://i.imgur.com/UDXohJA.png)

Google now I guess? 

//On progress
