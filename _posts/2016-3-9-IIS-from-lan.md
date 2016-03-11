---
layout: post
title: Accessing IIS Express from LAN
---

Today I encountered the need of debugging a web app from external server (located in our companies LAN). The problem is that the Web App is running under local IIS Express, and it should be requested from outer world.

Well, I am actually surprised it doesn't work "from the box". After launching my app from VS I tried accessing it from remote machine in chrome by IP. No success.
![](http://i.imgur.com/uRw1O7s.png)

Funny stuff - it doesn't necessary NOT work. Chrome was endlessly loading the page (Infinite timeout?), but just couldn't show it up. Pings go through, so better check project web configuration. I am (almost) sure I got dmitrijsminajevs/ domain as a DNS for ip, so why not trying replacing localhost with domain? Ofcourse it didn't work.
![](http://i.imgur.com/UDXohJA.png)

But I am almost sure there were a way how to tell IIS to capture multiple ports and IPs. After some time of googling in bing and binging in google I found out that IIS applications have it's own hosts file. Older releases of IIS store it in 

```
%username%\Documents\IISExpress\config\applicationhost.config
```

Things are little bit different for the newer versions of IIS. It creates application hosts file for every ASP.NET project in

```
%projectdir%\.vs\config\applicationhost.config
```

What I did was that I added new new binding configuration for my webapp. To the existing

```
<bindings>
  <binding protocol="https" bindingInformation="*:8300:localhost" />
</bindings>
```

I added 

```
  <binding protocol="https" bindingInformation="*:8300:dmitrijsminajevs" />
```

After that I allowed that IP to be used by non-Admin accounts

```
netsh http add urlacl url=http://dmitrijsminajevs:8300/ user=everyone
```

Aaaaaand that's really it. I restarted IIS, rerun my app and voilà, it's now available to everyone in my LAN network. :) 


P.S: There still may be troubles with firewall blocking connections to that specific port, so that's another thing to check.  
