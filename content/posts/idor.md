---
title: IDOR Vulnerability
date: 2022-02-09
description: "Perhaps the most significant Vulnerability recorded in the top 10 of OWASP is Insecure Direct Object Reference Vulnerability (IDOR Vulnerability)"
image: images/idor/banner.jpeg
alt: IDOR Vulnerability
---

## IDOR  Vulnerability

Perhaps the most significant Vulnerability recorded in the top 10 of OWASP is Insecure Direct Object Reference Vulnerability (IDOR Vulnerability). In this article, we will examine IDOR Vulnerability. Before pushing forward, let us first talk about Authentication. 
Authentication means checking a person's identity and permitting that person to get too explicit requests assuming the client is authenticated (confirmed).Yet, if a client isn't validated and can have the option to see documents, for example, incorrectly open records as the Hackers/Attackers do?, it is called Broken Authentication.This article will focus on how an attacker utilizes Broken Authentication Vulnerabilities that might prompt IDOR.

##  What is an IDOR Vulnerability?

In a web application, at whatever point a client generates, sends or receives a request from a server, there are some HTTP parameters, for example, "id", "uid", "pid" and so forth that have a few unique qualities which the client has been appointed. An attacker see such parameter values in cookies, headers, or wifi Packet catches. Through this, an attacker could alter these qualities, leading to IDOR.


#### A portion of the examples that untrusted the data information which can be manipulated utilizing IDOR:

-  https://hacksec.in/myaccount/uid=1
-  https://hacksec.in/myaccount/uid=2
-  https://hacksec.in/myaccount/uid=3
-  https://hacksec.in/myaccount/uid=4

As you see that  uid the URL to vulnerable and can be tampered by an attacker to break the authentication.

### IDOR attack utilizing guessable IDs

The most basic IDOR situation happens when the application references objects utilizing simple to figure IDs.For example, they can be total numbers and contain predictable words like the client's email or a folder name. Sometimes, they can be ineffectively encoded. For example, a base64 encoded steady Integer or a profile picture name hash reference. Assume that an application allows you to get to your information on the following endpoint:


GET /api/users/1

You should substitute your ID 1, with another guessed value in this basic situation.

### IDOR utilizing IDOR with GUIDs


Sometimes, the application utilizes. IDs are complicated or even difficult to figure. For this situation, it will probably be a Globally Unique Identifier (GUID). You can likewise track down it under the name of Universally Unique Identifier (UUID).To progress forward with the example we gave before; the endpoint may resemble the accompanying:


GET /api/users/b0413c-6b52-410-98c-b7194e6

For this situation, you can perform more enumeration on the application. In other words, attempt to find however many elements as you can. You will probably observe endpoints that return a rundown of items; everyone referred to utilizing a freely accessible GUID. For instance, the client public profile may return its GUID.

If UUIDs are not openly accessible, you can in any case test for the IDOR vulnerability. Although the effect may be lower, I've seen many occasions where the client has acknowledged the issue as valid. In addition, if there is a CSRF issue or a CORS misconfiguration, you can exfiltrate UUIDs and manufacture your malicious requests easily.


### IDOR in REST applications

In most present-day applications, you will manage REST APIs, which follow a basic naming show. I will clarify central issues about REST APIs, which would assist you with seeing how to test for IDOR. You can get more familiar with the REST convention. However, I will clarify what you want for a successful IDOR exploit.

This doesn't mean that you won't be insecure direct object reference vulnerabilities on our Website. When you see a component working with an article reference, consistently have a go at testing for IDOR.

####  REST HTTP methods

You can likewise call them HTTP action words. These characterize the activity to execute on the API. As a general rule, the `GET` strategy permits you to understand information, the `POST` will either make or update an asset, the `PUT` and `PATCH` action words update information and `DELETE` will erase your referred to the resource(s).

#### REST convention

REST applications follow a naming show, making it simple to reveal hidden IDOR vulnerabilities.

For effortlessness, suppose an application oversees clients utilizing gradual Integers. Through your standard identification, you enumeration this endpoint, which returns your profile information:


GET /api/profile


Assuming it is a RESTful API, you can test numerous things!

Firstly, attempt to annex an ID to the endpoint. You may coincidentally find the administrator or the owner utilizing little whole numbers.


GET /api/profile/0


Then, at that point, you can test the update of a client.


PUT /api/profile/0
Host: hacksec.in
Content-Type: application/json

{"email": "attacker@gmail.com"}

You can likewise test perusing every one of the profiles


GET /api/profiles

Obviously, things are not so basic, in actuality. However, the philosophy of testing for IDOR vulnerabilities actually applies.


## IDOR attack examples

Let's start with this simple IDOR Vulnerability PoC to show you that it is so natural to track down this Vulnerability in nature. For this situation, all the hacker needed to do was to loop through the request numbers, which are incremental integers. This prompted revealing subjective clients' structure data. Notice how the endpoint follows the /USERS/2222222


![enter image description here](https://i.postimg.cc/FHPcPkPG/111.png)

Here I am just creating an account, visiting the profile, intercepting the request, and then changing the user id. Here, we got an information discloser through IDOR. 

![enter image description here](https://i.postimg.cc/XYcxngV8/222.png)

### How to test for IDOR Vulnerability? IDOR methodology and tools

Insecure direct object reference vulnerabilities are not challenging to track down. However, some of them might go under your testing radar if your tests are superficial. Besides, you will get many duplicates if you are a bug bounty hunter.

Here is an approach you can follow to amplify your possibility of finding hidden IDOR vulnerabilities:-

- Register two accounts for every role the application supports. This will assist you with testing sidelong access control measures and privilege escalation

- Find however many features as you can, ideally with the role with the highest privilege. Assuming the application gives paid enrollment, attempt to get test records or buy it.

- Gather all the endpoints found and attempt to track down a naming pattern. Then, at that point, surmise new endpoint names based on how you discovered them.

Test for every one of the endpoints against every one of the jobs you've enrolled in before. If the application is minor and the roles don't go beyond two, you can manually do that. In the opposite case, you'll require an instrument to help you. In Burp Suite, you can utilize AuthMatrix, Auto-Repeater or Authorize plugins.

### Thanks for reading
