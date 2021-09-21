---
title: Find me writeup
date: 2021-09-06
description: "Hello guys script is here and today we will learn in this post how we can own find me web-lab"
image: images/find_me/Yellow Magenta Black White Neon Scifi YouTube Channel Art (2).png
alt: Find me
---

## Web-Lab information

### Find ME

|              |                                                     |
| ------------ | --------------------------------------------------- |
| Point:       | 30+                                                 |
| Level:       | MEDIUM                                              |
| Target:      | http://machine4.hacksec.in                          |
| First ownby: | [H3X1337](https://www.app.hacksec.in/profile/63)    |
| Created by:  | [SCRIPT1337X](https://www.app.hacksec.in/profile/1) |

## let's start

First of all, let's see what we have to work on by opening the URL.
![HomePage](/images/find_me/Home.PNG)

## Reconnaissance

Ok so now we start our reconnaissance, first we try to find all the hidden folders of the website using Dirb with default wordlist common.txt

![Dirb_result](/images/find_me/Dirb.PNG)

We get .git/HEAD shortly after we run dirb but it only had ref: refs/heads/main in the file: .git/HEAD . But it means there is a git repo in the root directory of this website. Inside the .git folder, there is a file named config in which the url of the git repo is given.So let's try to access the .git/config file of Find_me server repo.
![config](/images/find_me/config.PNG)

We got the URL of the repo of GitHub from the .git/config file inside the repo.

### Finding vulnerabilities in repo

So in this repo, there is a fast API application that is running on port 8000 according to the comments and this application contains some interesting endpoint like /playlist/upload/ and /playlist/load. pickle.load() is used to load python objects from pickle file and its vulnerable to deserialization attack. you can google to know more about this.

![config](/images/find_me/Source_code.PNG)

## Write exploit

![example_code](/images/find_me/example_code.PNG)

okay now we can run shell command using pickle exploit but still, we can't get the output of the command.
so what we can do we will send the command output to https://webhook.site.

![exploit](/images/find_me/exploit.PNG)

## Read hash.txt

it's a fast API application and documentation is not disabled thats means we can access the doc at http://machine4.hacksec.in:8000/docs. Upload the exploit at http://machine4.hacksec.in:8000/playlist/load

![exploit](/images/find_me/upload_exploit.PNG)

![exploit](/images/find_me/hash.PNG)

and we got the hash

### Thanks for reading
