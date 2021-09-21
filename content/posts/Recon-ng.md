---
title: How to use Recon-ng
date: 2021-09-20
description: "Recon-ng Information gathering tool in Parrot OS"
image: images/Recon-ng/Game Youtube Channel Art.png
alt: Recon-ng
---

## Recon-ng use in bug bounty

In this recon-ng tutorial, discover open source intelligence and how to easily pivot to new results. Find targets and move to discovering vulnerabilities.

## What is Recon-ng?

[Recon-ng](https://github.com/lanmaster53/recon-ng) is a reconnaissance tool with an interface similar to Metasploit. Running recon-ng from the command line, you enter a shell like environment where you can configure options, perform recon and output results to different report types.

The interactive console provides a number of helpful features, such as command completion and contextual help.

## Features of Recon-ng

- Recon-ng is free and open source tool this means you can download and use it at free of cost.

- Recon-ng is a complete package of information gathering modules. It has so many modules that you can use for information gathering.

- Recon-ng works and acts as a web application/website scanner.

- Recon-ng is one of the easiest and useful tool for performing reconnaissance.

- Recon-ng interface is very similar to metasploitable 1 and metasploitable 2 that makes is easy to use.

- Recon-ng’s interactive console provides a number of helpful features.

- Recon-ng is used for information gathering and vulnerability assessment of web applications.

- Recon-ng uses shodan search engine to scan iot devices.

- Recon-ng can easily find loopholes in the code of web applications and websites.

- Recon-ng has following modules Geoip lookup, Banner grabbing, DNS lookup, port scanning, These modules makes this tool so powerful.

- Recon-ng can target a single domain and can found all the subdomains of that domain which makes work easy for pentesters.

## Uses of Recon-ng :

- Recon-ng is a complete package of Information gathering tools.

- Recon-ng can be used to find IP Addresses of target.

- Recon-ng can be used to look for error based SQL injections.

- Recon-ng can be used to find sensitive files such as robots.txt.

- Recon-ng can be used to find information about Geo-IP lookup, Banner grabbing, DNS lookup, port scanning, sub-domain information, reverse IP using WHOIS lookup .

- Recon-ng can be used to detects Content Management Systems (CMS) in use of a target web application,

- InfoSploit can be used for WHOIS data collection, Geo-IP lookup, Banner grabbing, DNS lookup, port scanning, sub-domain information, reverse IP, and MX records Lookup

- Recon-ng is a complete package (TOOL) for information gathering. This tool is free and Open Source.

- Recon-ng subdomain finder modules is used to find subdomains of a single domain.

- Recon-ng can be used to find robots.txt file of a website.

- Recon-ng port scanner modules find closes and open ports which can be used to maintain access to the server.

- Recon-ng has various modules that can be used to get the information about target.

## Recon-ng Installation

Often used with the Kali Linux penetration testing distribution, installing within Kali is a simple matter of apt-get update && apt-get install recon-ng. Update Kali to ensure latest dependencies installed.

For those seeking the latest code on Ubuntu, the process is nearly as simple. Make sure you have git and pip installed.

#### Step 1: On Terminal now type command.

- git clone https://github.com/lanmaster53/recon-ng.git

![install guide](https://i.postimg.cc/hPHJ0wn5/install.png)

Congratulations recon-ng has been installed on your Linux .now you just have to run recon-ng.

#### Step 2: From the console it is easy to get `help` and get started with your recon.

- help
  ![help](https://i.postimg.cc/mrSNJR2D/help.png)

#### Step 3: Now to do Reconnaissance first you have to create a workspace for that. Basically, workspaces are like separate spaces in which you can perform reconnaissance of different targets. To know about workspaces just type the following command.

- workspaces

Recon-NG uses workpaces to help organize collected information according to our workflow. The command is ‘workspaces’ and its options are list, add, select and delete.

![workspaces](https://i.postimg.cc/Df891fgn/workspaces.png)

#### Add workspace

Let’s do some reconnaissance on hacksec. We’ll first create a workspace ‘hacksec’ and the domain ’hacksec.in’.
Now type command:-

- workspaces create hacksec

![workspaces create](https://i.postimg.cc/65NTPPT2/hacksec-wrk.png)

#### Step 4. You have created workspace for you now you have to go to marketplace to install modules to initiate your Reconnaissance here we have created a workspace called hacksec. Now we will Reconnaissance within hacksec workspace. Now go to marketplace and install modules.

- marketplace search

![marketplace](https://i.postimg.cc/htvJ8dfp/markt.png)

#### Step 5: As you can now see a list of modules and so many of them are not installed so to install those modules type following command.

lets use the `hackertarget` module to gather some subdomains. This uses the [hackertarget.com](https://hackertarget.com/) API and [hostname search](https://hackertarget.com/find-dns-host-records/).

- `marketplace install hackertarget`

![marketplace install](https://i.postimg.cc/Twff9ztf/hacktrgt.png)

#### Step 6: As you can see we have installed the module names hackertarget in our workspace hacksec.

- modules load hackertarget

#### Step 7:\*\* As you can see now we are under those modules i.e hackertarget. Now to use this module we have to set the source.

- options set SOURCE hacksec.in

![set](https://i.postimg.cc/J443gtsB/scr.png)
We have set hacksec.in as a source by command options set SOURCE hacksec.in.

#### Step 8: Run the module

Type `run` to execute the module.

![run](https://i.postimg.cc/fTv0mG7f/run.png)

#### Step 9: Lets check the hosts

Now we have begun to populate our hosts. Typing `show hosts` will give you a summary of the resources discovered.

![hosts](https://i.postimg.cc/T341cfKg/show.png)
Here again the help comes in handy `marketplace help` shows commands for removing modules, how to find more info, search, refresh and install.

#### Help

The help command from within a loaded module has different options to the global 'help'.  
When you are ready to explore more modules use 'back'.

This help menu brings additional commands such as:

- goptions: Manages the global context options
- reload: Reloads the loaded module

- run: Runs the loaded module
- script: Records and executes command scripts.

#### Thanks for reading