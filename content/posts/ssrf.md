---
title: Server-side request forgery (SSRF)
date: 2022-02-23
description: "SSRF is a class of vulnerability that allows you to make requests from a backend server to internal or external systems."
image: images/ssrf/banner.png
alt: Server-side request forgery (SSRF)
---

## Server-side request forgery (SSRF)


Web applications have become perhaps the main resources for organizations of all sizes. What's more, they have also turned into a target because of this. Web applications are getting more complicated and more extraordinary in scope. This increases the attack for a hacker. Hackers are growing more capable consistently, and they utilize various tools and methods to hack web applications. Here, we'll focus on one attack that has been rising in popularity: server-side request forgery (SSRF) attacks.


## What is SSRF?


Current web applications have a perplexing design, and it's normal to have different administrations that comprise a web application. For example, you could have a service to deal with instalments, a service for backend and administrator activities, and a client-facing service. 

SSRF is a class of vulnerability that allows you to make requests from a backend server to internal or external systems.

Here is an example of a web application that has three services. The first is for dealing with sensitive information and its transactions, the second for administrator activities, and the third for client activities. Administrators ordinarily approach sensitive data and can perform actions like reviewing, editing or deleting said information. So when an administrator needs to play out some activity on sensitive information, the administrator server sends a request to the server dealing with sensitive data through APIs. The server will play out those activities and send the result to the administrator server. These servers have ACLs and authorization rules designed to lay out the trust between them. Also, just believed entities are permitted to perform activities.

Hackers can abuse this "trust" to craft queries to accomplish something malicious in a vulnerable setup. You can create input on the admin service and send a request to the server on localhost or 127.0.0.1. Furthermore, because the request comes from the actual server, there's trust by default, and the request is executed. A critical high-risk example of this is assuming that the HTTP request to the administrator server is utilized to fetch the  /passwd file. On the off chance that the contents are returned, hackers can brute-force the hashed passwords. 

Another model is the Redis data set, whose HTTP API can be [abused](https://maxchadwick.xyz/blog/ssrf-exploits-against-redis) to query information, update the design, and even reason remote code execution (RCE).

Presently we should comprehend inside and out how SSRF works.

## How SSRF works

### SSRF on localhost

Suppose you have an e-commerce site that has various servers on the backend. The application has multiple classes with different items in every classification, and the specifications for an item are stored on another service. In this way, when you click on an item, the current server (where the application is hosted) sends a request to the next server to get details for the item. For simplicity, how about we consider that the request is as per the following:

`https://www.ravagedband.com/index.php?page=releases/scream.php`

![enter image description here](https://i.postimg.cc/44hYTHpJ/home.png)
So the server is sending a request to the product specs server to send details for the item with releases/scream.php. When this request is made, the product specs server will track down details for that item and send it to the main server. Also, the main server will show the contents. This arrangement is vulnerable to SSRF.

For example, hackers can control the URL boundary to make malicious requests for an example of a request. For instance, suppose the hacker modifies the request as follows:

`https://www.ravagedband.com/index.php?page=file:///etc/passwd`

![enter image description here](https://i.postimg.cc/ZKJFKhZs/ssrf2.png)

If there's no protection from SSRF and assuming this request is executed, the contents of the /etc/passwd document would be shown. Here SSRF is on the server making the request. In any case, SSRF can be involved on different servers also.

## SSRF for port scanning

Most internal servers aren't open to external networks in many network designs. I just believed internal servers could get to them. In such cases, to hack the limited internal servers, they need to figure out how to track down data about them from inside the internal organization. SSRF can be utilized for port examining of such internal servers. Hackers can create requests to various ports on the server, and given the response, they can close whether or not there's a service running on that specific port.

EXAMPLE:-

`https://www.ravagedband.com/index.php?page=Burp Collaborator link:21`

Based on the response from the server, a hacker can comprehend whether the server 192.168.1.10 has an FTP administration on port 21 or not. They can send numerous requests to servers by changing the port number. What's more, from the results, they'd get a rundown of which ports are open and can comprehend which administrations are running on that server.

We can continue to give models. However, at that point, this post could go on forever. Your creative mind is the breaking point on how a hacker can request an SSRF attack. You can discover a few additional models in this [SSRF cheatsheet](https://highon.coffee/blog/ssrf-cheat-sheet/).

## Types of SSRF

Based on how the casualty server responds to the request, SSRF can be divided into two types:

### 1. Basic SSRF

This is the sort of SSRF where the victim server returns information to the hacker. A hacker requests a victim server whenever they play out an SSRF attack. Essential SSRF is the point at which the victim server sends back certain information after the created request is made. A hacker would utilize Basic SSRF to get information from the server or get to unauthorized features.

### 2. Blind SSRF


As the name demonstrates, in this kind of SSRF, hackers don't get information back from the server. You see this generally when the request is to set off some activity on the victim server without getting anything to the mentioning server. Hackers utilize this kind of SSRF to roll out specific improvements using the victim server since they shouldn't even need to get results for the movement.

Since we've covered what SSRF is and the way that it works.

## Possible Parameters

>**dest
redirect
uri
path
continue
url
window
next
data
reference
site
html
val
validate
domain
callback
return
page
feed
host
port
to
out
view
dir
show
navigation
open**

### Thanks for reading
