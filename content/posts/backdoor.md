---
title: BACKDOOR writeup
date: 2021-10-30
description: "Hello guys script is here and today we will learn in this post how we can own backdoor web-lab"
image: images/backdoor/Green Modern Technology & Gaming Logo.png
alt: Find me
---

## Web-Lab information

### BACKDOOR

|              |                                                     |
| ------------ | --------------------------------------------------- |
| Point:       | 20+                                                 |
| Level:       | EASY                                                |
| Target:      | http://machine10.hacksec.in                         |
| First ownby: | NONE                                                |
| Created by:  | [SCRIPT1337X](https://www.app.hacksec.in/profile/1) |

## let's start


First of all, let's see what we have to work on by opening the URL.
![HomePage](/images/backdoor/2021-10-30-231640_1366x768_scrot.png)

## Reconnaissance

Ok so now we start our reconnaissance, first, we try to find all the hidden files of the website. Here we will need a little bit of guessing.The box name is backdoor so we can try PHP backdoor's names.
When we try to visit http://machine10.hacksec.in/wso.php we get a login page so it's a wso web shell.
![LoginPage](/images/backdoor/2021-10-30-232355_1366x768_scrot.png)

and web shell's source code is also given https://gist.github.com/ScRiPt1337/0137d1a115d2055ecbefefc46a462ec8.
![SourceCode](/images/backdoor/2021-10-30-233010_1366x768_scrot.png)

### Finding vulnerabilities in web shell
We need to bypass this login page this is the vulnerable function
![vulnerableCode](/images/backdoor/2021-10-30-233128_1366x768_scrot.png)
```php
if(!empty($auth_pass)) {
    if(isset($_POST['pass']) && (md5($_POST['pass']) == $auth_pass))
        WSOsetcookie(md5($_SERVER['HTTP_HOST']), $auth_pass);

    if (!isset($_COOKIE[md5($_SERVER['HTTP_HOST'])]) || ($_COOKIE[md5($_SERVER['HTTP_HOST'])] != $auth_pass))
        wsoLogin();
}
```
#### What this code is doing?

if the password is not empty it will check if the password hash in ==  to $authpass
then it will set cookies with key and value
the key is the domain name's md5 value and the value will be $authpass

### let's exploit this
so let's set this values by our self and refresh the webpage

when we create an MD5 hash of machine10.hacksec.in  we got 7c49dcdf7703c31eacb2b6f730ffcb48

|    key       |        value                                        |
| ------------ | --------------------------------------------------- |
| 7c49dcdf7703c31eacb2b6f730ffcb48| 5c43208be18a43f4b3dd3f5b162d881a |

![cookies](/images/backdoor/2021-10-30-234357_1366x768_scrot.png)

#### BINGO 
We get access to the webshell 
![cookies](/images/backdoor/2021-10-30-234627_1366x768_scrot.png)

## Read hash.txt
Hash.txt is at /var/www/hash.txt
![hash](/images/backdoor/2021-10-30-234754_1366x768_scrot.png)

### Thanks for reading