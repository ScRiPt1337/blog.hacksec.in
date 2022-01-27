---
title: Cross Site scripting attack (XSS)
date: 2022-01-27
description: "A cross Site scripting attack is a malicious code injection executed in the victim's browser."
image: images/xss/banner.png
alt: Cross-Site Scripting attack (XSS)
---
## Introduction to XSS Vulnerability


A cross-Site Scripting attack is a malicious code injection executed in the victim's browser. Likewise, it can be performed with different strategies - with practically no saved script in the webserver.

The fundamental motivation behind this attack is to take the other client's character information - cookies, session tokens and other data. This attack is being utilized to accept the other individual's cookies. As we probably are aware, cookies assist us with signing in naturally. In this manner, we can sign in with different characters with taken cookies. What's more, this is one reason why this attack is viewed as perhaps the most dangerous attack.

An XSS attack is being performed on the client-side. This attack can be performed with various client-side programming languages. Be that as it may, most frequently, this attack is performed with Javascript and HTML.


### How is XSS Being Performed?

Cross-Site Scripting attack implies sending and injection malicious code or content. Malicious code is typically composed of client-side programming languages like Javascript, HTML, VBScript, Flash, etc. Be that as it may, Javascript and HTML are generally used to play out this attack.

This attack can be executed in various ways. Contingent on the kind of XSS attack, the destructive content might be reflected on the clint's browser or stored in database and executed without fail when the client calls the fitting capacity.

The principle justification for this attack is improper input validation approval, where malicious info can get into the result. A malicious client can enter content injected into the site's code. Then, at that point, the program can't know whether the executed code is malicious or not.

Consequently, destructive content is being executed on the casualty's program, or any faked structure is being shown for the clients. There are a few structures wherein XSS attack can happen.

#### Primary types of Cross-Site Scripting are as per the following:-

1. Cross-Site Scripting can happen on the destructive content executed at the client-side.
2. The counterfeit page or structure showed to the client (where the casualty types qualifications or snaps a malicious connection)

### Types Of XSS

There are three sorts of cross-site prearranging, specifically:-
1. Reflected XSS
2. Stored XSS
3. Dom-based XSS


### 1. What is a reflected XSS attack?

Reflected XSS attacks, otherwise called non-persistent attacks, happen when harmful content is reflected off a web application to the victim's browser.

The script is activated through a connection which sends the request to a site with a vulnerability that empowers the execution of malicious script. The vulnerability is usually an aftereffect of approaching requests not being sufficiently sanitized, which takes into the account control of a web application's capacities and the activation of the malicious script.

To disperse the malicious link, a culprit regularly inserts it into an email or third party site (e.g., in a remark area or social media).
The connection is inserted inside an anchor text that incites the client to tap on it, which starts the XSS request to take advantage of the site, reflecting the attack to the client.

####  Reflected XSS attack example

Example: Consider we have a site with a search field.

![xss](https://i.postimg.cc/LsYQg8Ng/11.png)
Suppose the search query field is vulnerable. When the client enters any script, it will be executed.

Consider, a client enters a basic script as displayed underneath:


-  <script>alert('HackSec')</script>

![enter image description here](https://i.postimg.cc/L8fNmbXj/22.png)

Then,  after clicking the "Search" button, the entered script will be executed.

![enter image description here](https://i.postimg.cc/44S5VgHz/xss.png)

As we find in the Example, the script composed into the query field gets executed. This shows the vulnerability of the XSS attack. Notwithstanding, a more unsafe script might also be consistent.

Many analyzers stir up Cross-Site Scripting attacks with Javascript Injection, likewise performed on the client-side. In both, the malicious attacks script is being injected. Be that as it may, in the XSS attack case <script> labels are not essential to execute the script.

### How to Test Against XSS?

First, to test against XSS attacks, black box testing can be performed.
That is to say, and it very well may be tried without a code review. Notwithstanding, code review is consistently a suggested practice, and it also brings more dependable outcomes. 
From my software testing experience, I might want to add that if a decent black box testing strategy is chosen and performed precisely, this should be enough.

While beginning testing, an analyzer consider which site's parts are vulnerable against the possible XSS attack.

It is better to list them in any testing record, and this way, we will be sure that nothing will be missed. Then, at that point, the analyzer should anticipate what code or script information fields must be checked. It is critical to recall, what results mean, that application is vulnerable, and it breaks down the outcomes completely.

While testing for possible attacks, it is essential to check how it reacts to the composed scripts and if that script is executed or not etc.

## 2. What is a Stored XSS attack?

Persistent XSS attacks are an exceptionally critical danger since they can have a wide-running reach and don't need a social engineering phase (like Reflected XSS attacks.
which we'll cover in our next portion of this series) to get clients to make a particular move, like clicking a connection.


Anyway, how precisely do Stored XSS attacks work? What are the consequences of a successful attack? How treats an actual attack situation resemble? What's more, above all, how might you secure against them?

How about we work it out.

### How Do Stored XSS Attacks Work?

Persistent cross-site scripting attacks can happen when sites or web applications. Permit client input yet doesn't as properly sanitize or limit its substance. This considers malicious code to be entered as input, which is stored on the server and shown to unsuspecting site visitors.

For example, suppose a hacker can consist of a malicious script while posting a comment on a famous weblog. In that case, all of us who examine that weblog article could be exposed to the malicious script. The attacker's code is incorrectly handled as valid input by way of the website online in question and doesn't get well encoded as a result.

![enter image description here](https://i.postimg.cc/XYWsCv91/sample.png)An example of a textual content enter field that could be vulnerable to stored XSS attack.

Textual content input fields are the usual maximum area for the injection to arise; however, places that don't usually incorporate scripts (like picture tags or event attributes) are also prime goals. Any detail that isn't concerned to enter validation, encoding, or filtering can likely be taken advantage of by an attacker.

![done](https://i.postimg.cc/pXPwNxdj/done.png)

However, Stored XSS is somewhat simple for hackers to pull off. After observing a vulnerable site, all they need to do is inject their malicious code and wait for victims to visit (hackers will promote their quality through spam messages or web-based media posts). Finding the target site itself is the most complex piece of the cycle.


#### The interaction for observing a vulnerable objective typically goes as follows:-

1. An attacker observes a site that might be vulnerable.
2. They test it by storing a script on the server and taking advantage of the vulnerability.
3. They explore the page that would convey the malicious code.
4. They verify whether the script executes.


#### The Primary Targets of Stored XSS Attacks

Any site that considers the sharing of content by clients is a possible objective for a Persistent XSS attack. Think of any place with remark fields or text boxes for client inputs and destinations where that information is stored and shown to different clients. Common targets include:-

1.  Person to person communication destinations.
2.  Remark areas of sites, for example, sites or video-     sharing platforms.
3. CRM/ERP system.
4. Email server consoles.

Stored XSS attacks succeed due to the client's confidence in real sites - the site ends up having a vulnerability that can be taken advantage of through XSS.

 ##  What is DOM Based XSS?
 
As per different exploration and studies, up to half of sites are vulnerable against DOM Based XSS vulnerabilities. Security analysts detected DOM XSS issues in high profile web organizations like Google, Yahoo, and Amazon.

DOM-based XSS, also called Type-0 XSS, is an XSS attack in which the attack payload is executed by adjusting the DOM in the casualty's program. This makes the customer run code without the client's information or consent. The actual page (for example, the HTTP response) won't change, yet a malicious change in the DOM climate will cause the customer code contained in the page to execute alternately.

This varies from reflected or stored XSS attacks, which place the attack payload into the response page because of server-side vulnerabilities. DOM XSS is a weakness on the client-side.

### How Do DOM XSS Attacks Work?
 DOM XSS assaults commonly follow this cycle:-
 
 1. The victim's browser gets a connection and sends an HTTP request to hacksec.in, and receives a static HTML page.
 2. The victim's browser then, at that point, begins parsing this HTML into DOM. The DOM contains an article called document, which includes a property called URL,  this property is populated with URL of the current page as a feature of DOM creation..
 3. When the parser processes Javascript code, it executes it and changes the raw HTML of the page. For this situation, the code references document.URL, thus, a piece of this string is implanted at parsing time in the HTML.
 4. The string is then parsed, and Javascript code is executed with regards to a similar page, resulting in XSS.

The logic behind DOM XSS is that input from the client - source - goes to an execution point - sink. In the past models, our source was document.write and the sink was alert(document.cookie).

After the site executes the malicious code, attackers can steal the cookies of the client's program or change the behaviour of the page on the web application.

### How Do Attackers Exploit DOM XSS Vulnerabilities?

How about we jump a piece further to understand the potential sources or passage focuses, the attacks can perform DOM XSS attacks, and the "sinks" or DOM objects in which they can execute malicious code.

### Source

A source is a JavaScript property that contains information that an attacker might actually control:

document.URL  
document.referrer  
location  
location.href  
location.search  
location.hash  
location.pathname

### Sink

A sink is a DOM  function that permits JavaScript code execution or HTML rendering.

eval  
setTimeout  
setInterval  
document.write  
element.innerHTML

Any application is vulnerable against DOM-based cross-site scripting, assuming there is an executable way to create information from source to sink.

Various sources and sinks have different properties and behaviours that can affect exploitability and determine what strategies are utilized. Furthermore, the application's contents may execute approval or another handling of information that should be obliged when intending to take advantage of a vulnerability.

### Thanks for reading
