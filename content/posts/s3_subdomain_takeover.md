---
title: Subdomain Takeover on AWS S3
date: 2021-09-16
description: "Subdomain Takeover on AWS S3 using Subdover Tutorial"
image: images/s3_subdomain_takeover/Green and Black Geometric Techno Technology YouTube Channel Art.png
---

# Subdomain Takeover on AWS S3

#### What Is Sub domain Takeover:

When an attacker is able to gain control of a company’s subdomain hosted on a cloud service such as AWS, github etc. because of the DNS entries pointing to that service is not being removed. This allows attacker to set up a phishing page on that sub-domain or serve malicious content.
**Disadvantage:**
· Attacker can misuse company’s reputation by send phishing emails from the legitimate domain, perform XSS, phishing, stealing cookies and more.
**What is S3(Simple Storage Service):** S3 buckets are scalable , high speed , data availability web based cloud storage service designed to use read private, public content or upload content to the buckets. You can also host your webpage on it and can render the contents of this on any of your subdomain using the CNAME DNS entry

#### Subdomain takeover in amazon s3:

Each bucket pointing to a specific domain or subdomain. So sometimes, when s3 buckets is no longer in use customer delete them from their Amazon account, but forgets to remove the DNS entry pointing to that subdomain it may escalate to a subdomain takeover because amazon allow non existing bucket names to be claimed again on any other account.

## What is a DNS CNAME record?

The ‘canonical name’ (CNAME) record is used in lieu of an A record, when a domain or subdomain is an alias of another domain. All CNAME records must point to a domain, never to an IP address. Imagine a scavenger hunt where each clue points to another clue, and the final clue points to the treasure. A domain with a CNAME record is like a clue that can point you to another clue (another domain with a CNAME record) or to the treasure (a domain with an A record).
For example, suppose blog.example.com has a CNAME record with a value of ‘example.com’ (without the ‘blog’). This means when a DNS server hits the DNS records for blog.example.com, it actually triggers another DNS lookup to example.com, returning example.com’s IP address via its A record. In this case we would say that example.com is the canonical name (or true name) of blog.example.com.
Oftentimes, when sites have subdomains such as blog.example.com or shop.example.com, those subdomains will have CNAME records that point to a root domain (example.com). This way if the IP address of the host changes, only the DNS A record for the root domain needs to be updated and all the CNAME records will follow along with whatever changes are made to the root.
A frequent misconception is that a CNAME record must always resolve to the same website as the domain it points to, but this is not the case. The CNAME record only points the client to the same IP address as the root domain. Once the client hits that IP address, the web server will still handle the URL accordingly. So for instance, blog.example.com might have a CNAME that points to example.com, directing the client to example.com’s IP address. But when the client actually connects to that IP address, the web server will look at the URL, see that it is blog.example.com, and deliver the blog page rather than the home page.

## Exploitation:

I am using Subdover tool for takeover the subdomain
**Subdover** is a _MultiThreaded_ Subdomain Takeover Vulnerability Scanner _Written In Python3_, Which has more than _70+ Fingerprints_ of potentially vulnerable services. Uses _CNAME record_ for verification of findings.

- ### Features
- More than 70+ Fingerprints of potentially vulnerable services
- Uses CNAME record for verification of findings
- Built-in Subdomain Enumeration Method [**Used findomain for Subdomain Enum**]
- Can Scan targets from subdomain list
- Can Test Single Target for Subdomain Takeover
- MultiThread, Extermely Fast Scanner [**Default Threads: 10**]
- You can choose number of threads
- You can save result in TXT file
- Extremely Clean Output
- OS Independent [**Can be used on any OS which supports Python3**]
- Auto Command Line Updater

#### How To Install subdover

Step 1:- Before installing the subdover you need to install [Findomain](https://github.com/Findomain/Findomain) and [Httpx](https://github.com/projectdiscovery/httpx)

Step 2:- After installing Findomain and Httpx git clone subdover:-

- git clone https://github.com/PushpenderIndia/subdover.git

Step 3: after that run the cmd given below:-
  > sudo python3 subdover.py -d target.com
  > ![takeover](https://i.postimg.cc/43HZfqZG/subdover.jpg)
  > Step 3:- Since the CNAME record is not deleted from
  > target.com DNS zone, anyone who registers _anotherdomain.com_ has full control over sub.example.com until the DNS record is present.
  > ![found](https://i.postimg.cc/Ls0XvwBg/found.jpg) 
  > ![not found](https://i.postimg.cc/mrbcD7VV/not-found.jpg)

Step 4:- Now go to the aws to create the s3 bucket by filling bucket name and AWS region.
  > ![bucket](https://i.postimg.cc/449stmKg/cr-bucket.jpg)
  
Step 5:- Now its time to upload the index file.
  > ![index](https://i.postimg.cc/pXdNCrrr/upload-in.jpg)
  > Lets check the sub domain after uploading index file
  > ![poc](https://i.postimg.cc/gcQySBkh/poc.jpg)

### Thanks for reading