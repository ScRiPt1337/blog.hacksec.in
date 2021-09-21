---
title: how to use Shodan
date: 2021-09-13
description: "Complete Guide to Shodan | Shodan Tutorial"
image: images/shodan/Purple Blue Abstract Gamer YouTube Channel Art.png
alt: Shodan
---

##  Shodan Use In Bug Bounty


### What is shodan

Shodan is a search engine that lets users search for various types of servers (webcams, routers, servers, etc.) connected to the internet using a variety of filters. Some have also described it as a search engine of service banners, which are metadata that the server sends back to the client. This can be information about the server software, what options the service supports, a welcome message or anything else that the client can find out before interacting with the server.

## Why Shodan is better than Google? 

The search engine crawlers browse the web and when it finds a device, it collect metadata about the device.  Unlike Google, crawls the internet looking for websites, Shodan navigates the Internet’s back channels.

It keeps looking for the servers, printers, routers, webcams, and all the other stuff that is connected to and makes up the Internet.  The basic thing is Shodan searches for devices those have a web interface. Shodan is also called dark Google, scariest search engine ever and  ‘hacker’s search engine at the same time. 

## How to use Shodan?

Shodan does not allow you to fetch all data free of cost. If you search about ‘camera’, it will display 323,647 results. However, you can access to only 10 of them and after that you need to login.

## Shodan dork 

### Server

Find the devices or servers that contain a specific server header flag. You can research vulnerable servers.

`server: "apache 2.2.3"`

or you can use directly the flag

`apache 2.2.3`

### hostname:

Find devices with specific hostname worldwide. The hostname is a label that’s assigned to a device connected to a network that is used to spot the device in various kinds of transmission, like the World Wide Web. You can use multiple filters altogether included in the shodan cheat sheet to narrow your search.

`server: "apache" hostname:"google"`

### Net:

Find devices or machines based on an IP address or /x CIDR. This filter can also be used to find the IP range or certain IP addresses and subnet masks.

`net:34.98.0.0/16`

### Databases:

Databases often hold critical bits of information. When exposed to the public internet—whether for ease of development access or simply due to misconfiguration—can open up a huge security hole.
To find MongoDB database servers which have open authentication over the public internet within Shodan, the following search query can be used:

`"MongoDB Server Information" port:27017 -authentication` 

MongoDB also has a web management application similar to phpMyAdmin called Mongo Express Web GUI, which we can find with the following query: 

`"Set-Cookie: mongo-express=" "200 OK"` 

Similarly, to find MySQL-powered databases:

`mysql port:"3306"` 

And to look up PostgreSQL databases:

`port:5432 PostgreSQL` 

### Port: 

Searching for services running on open port saccessible on the public internet—like FTP servers, SSH servers and others—is possible by using the following queries.

For FTP, querying for proftpd, a popular FTP server:

`proftpd port:21` 

To look for FTP servers that allow anonymous logins: 

`"220" "230 Login successful." port:21` 

To query for OpenSSH, a popular SSH server: 

`openssh port:22`

To look up EXIM-powered mail servers on port 25:

`port:"25" product:"exim"`

Memcached, commonly seen on port 11211, has been a major source of UDP amplification attacks leading to huge DDoS attacks. Services running Memcached available on the public internet are often exploited for these attacks:

`port:"11211" product:"Memcached"`

Jenkins is a popular automated build, deploy and test tool, often the starting point of any software being built for release. It can be found via the following query:

`"X-Jenkins" "Set-Cookie: JSESSIONID" http.title:"Dashboard"` 

### DNS servers 

DNS servers with recursion enabled can be a huge source of  network threats. To find these servers, one can use the query:

`"port: 53" Recursion: Enabled` 

### Network infrastructure 

To find devices running a specific version of a RouterOS operating system that powers routers, switches and other networking equipment from the company MikroTik, we use the following search query:

`port:8291 os:"MikroTik RouterOS 6.45.9"`

This allows us to find those switches, routers and other networking gear running an older and possibly vulnerable version of the RouterOS operating system which runs on port number 8291, used for the web management UI.

### Web servers 

Shodan makes it possible to find and filter out web server versions as well. For example, we’ll use this to find IPs that host a specific version of the popular web server Apache:

`product:"Apache httpd" port:"80"`

With the above query, we can find Apache web servers on port 80, the most common port for web servers.

Similarly, to look up Microsoft IIS-powered websites and web servers:

`product:"Microsoft IIS httpd"`

To look up Nginx-powered websites and web servers:

`product:"nginx"`

The above product query can be combined with the “port” option too. For example, if you wish to lookup Nginx-powered web servers on port 8080:

`"port: 8080" product:"nginx"` 

### Operating systems 

Querying for older and possibly end-of-life operating systems like Windows 7 is also possible in Shodan, by using the following query:

`os:"windows 7"`

Similarly, to look up specific build versions of Windows 10, the following query can be used, wherein we look up Windows 10 Home edition with build version 19041:

`os:"Windows 10 Home 19041"`

To filter and find Linux-based devices, the following query can be used:

`os:"Linux"` 

### location 

At certain points of time, the amount of data returned by Shodan might be a bit too much. To make things easier to filter, the Country or City filter can be applied:

For example, if you wish to filter by country:

`country:"IN"`

To filter by city:

`"city: DELHI"`

Last but not least, you can even look up via GPS coordinates of a region or city:

`geo:"61.5274, 0.XXXX"`

This location filter can be combined with other filters as well. For example, if you wish to find Windows 7 devices in the United Kingdom, the following query can be used:

`os:"windows 7" country:"IN"` 

### SSL certificates 

Another advantage of Shodan is that it can be used to  find SSL certificates that are expired or self-signed "Dangers of Using Self-Signed Certificates").

To find self-signed certificates, the following query can be used:

`ssl.cert.issuer.cn:example.com ssl.cert.subject.cn:example.com`

To find expired SSL certificates, this query can be used:

`ssl.cert.expired:true` 

### before/after:

The ‘after’ and ‘before’ filter helps you to devices after and before a particular date.

The format allowed is dd/mm/yyyy

`nginx before:13/04/2021 after:13/04/2017` 

### Citrix:

Find Citrix Gateway.

`title:"citrix gateway"` 

### Misconfigured WordPress Sites:

The wp-config.php if accessed can give out the database credentials.

`http.html:"* The wp-config.php creation script uses this file"`

You can access the main WordPress configuration file and capture sensitive information like credentials or AUTH_KEY of misconfigured sites. 

### Jenkins:

Find for all Jenkins Unrestricted Dashboard

`x-jenkins 200`

## dorks for IoT device intelligence 

### Industrial control systems

[Industrial control systems](https://www.shodan.io/explore/category/industrial-control-systems "Shodan Industrial Control Systems")  run some of the most complex machinery seen in modern times. With uses ranging from power generation to manufacturing, control systems can be as simple as basic temperature sensors to complex machinery that controls the whole plant.

For example, to find XZERES Wind Turbines:

`title:"xzeres wind"`

And for Mitsubishi Electric, the MELSEC-Q protocol is commonly used by control system machines/networks:

`port:5006,5007 product:mitsubishi`

We can also find electric vehicle chargers on Shodan, with the following query:

`"Server: gSOAP/2.8" "Content-Length: 583"`

### Remote Desktop

Remote Desktop, commonly known as RDP, is a service used to remotely access Windows-based machines. These devices often run older or out-of-date Windows patches, allowing them to be exploitable.

To look up open Windows Remote Desktop ports, use:

`remote desktop "port:3389"`

Looking at the Linux side of things, we commonly see VNC being used. Devices with VNC available without authentication can be found with the following query:

`"authentication disabled" "RFB 003.008"` 

### NAS accesses 

NAS, or network attached storage devices, often carry or hold a lot of data. Leaving them exposed to the public internet without authentication can lead to data theft, data loss and  ransomware attacks.
Samba is a popular networking protocol which provides file and print services for Windows based devices. The following query allows us to find devices running on the Samba protocol on port 445 with authentication disabled:

`"Authentication: disabled" port:445`

For media devices, Plex is a popular media management device used to manage photos, movies and music. Plex devices can be found with the following filter:

`"X-Plex-Protocol" "200 OK" port:32400`

Some NAS devices have FTP-based services running on them. They can be found via the following query:

`"220" "230 Login successful." port:21` 

### Printers and copiers 

With nearly all modern printers and copiers having networking capabilities, and some even with WiFi abilities, it’s critical to secure them.

To find HP-powered printers, the following query can be used:

`"Serial Number:" "Built:" "Server: HP HTTP"`

Similarly, to find EPSON powered printers:

`"SERVER: EPSON_Linux UPnP" "200 OK"`

Xerox printers and copiers often seen at workplaces are easily found via the following query, which pulls identifiable information from its SSL certificate:

`ssl:"Xerox Generic Root"` 

## Shodan Command-Line Interface 

The *shodan* command-line interface (CLI) is a command-line library for the Shodan IoT search engine. You can install using this simple python’s pip command,

`$  pip install shodan`

Once the shodan tool is installed you need to initialize the environment variable with the private API key, you can get form shodan account settings.

`$  shodan init PRIVATE_API_KEY`

Now you can run just the shodan command to get the help.

### Thanks for reading