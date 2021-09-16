---
title: AWS Bucket Dump
date: 2021-09-16
description: "Deep Dive Into AWSBucketDump | AWSBucketDump Tutorial"
image: images/awsbucketdump/Pink and Maroon Neon Noir  Vaporwave Action  Adventure YouTube Channel Art.png
---

# AWS Bucket Dump

### Why this tool?

AWSBucketDump is a security tool to find interesting files in AWS S3 buckets that are part of Amazon cloud services. These storage containers may have interesting files, which a tool like AWSBucketDump can discover.

### How it works

AWSBucketDump is using a Python script to parse a list of names. Using that list it tries to guess valid bucket names. Using a keywords list the most interesting items can be filtered from the results.

### Usage and audience

AWSBucketDump is commonly used for **configuration audit**, **discovery of sensitive information**, or **security assessment**. Target users for this tool are security professionals.

#### AWSBucketDump is a tool to quickly enumerate AWS S3 buckets to look for loot. It's similar to a subdomain bruteforcer but is made specifically for S3 buckets and also has some extra features that allow you to grep for delicious files as well as download interesting files if you're not afraid to quickly fill up your hard drive.

This is a tool that enumerates Amazon S3 buckets and looks for interesting files.
I have example wordlists but I haven't put much time into refining them.
[https://github.com/danielmiessler/SecLists](https://github.com/danielmiessler/SecLists) will have all the word lists you need. If you are targeting a specific company, you will likely want to use jhaddix's enumall tool which leverages recon-ng and Alt-DNS.
[https://github.com/jhaddix/domain](https://github.com/jhaddix/domain) && [https://github.com/infosec-au/altdns](https://github.com/infosec-au/altdns)
As far as word lists for grepping interesting files, that is completely up to you. The one I provided has some basics and yes, those word lists are based on files that I personally have found with this tool.
Using the download feature might fill your hard drive up, you can provide a max file size for each download at the command line when you run the tool. Keep in mind that it is in bytes.
I honestly don't know if Amazon rate limits this, I am guessing they do to some point but I haven't gotten around to figuring out what that limit is. By default there are two threads for checking buckets and two buckets for downloading.

### AWSBucketDump use install

#### Step 1:- Go to the AWSBucketDump [github] and clone the repo.

- git clone https://github.com/jordanpotti/AWSBucketDump
  ![aws](https://i.postimg.cc/tRMjxBMM/aws11.png)

#### Step 2:- Now go to the folder name AWSBucketDump and run cmd below:-

- python AWSBucketDump.py -h
  ![help](https://i.postimg.cc/T1Dfwmfw/aws2222.png)

#### Step 3:- after check all the cmnd of awsbucketdup now run the cmnd given below:-

-python AWSBucketDump.py -l BucketNames.txt -g interesting_Keywords.txt -D -m 500000 -d 1

### Some dork for find aws delicious files

-site:s3.amazonaws.com filetype:txt username
![username](https://i.postimg.cc/rwJHnVdb/log.png)

- site:s3.amazonaws.com password filetype:xls
  ![pass](https://i.postimg.cc/QdQDXZFk/2.png)
- site:s3.amazonaws.com logs filetype:txt
  ![logss](https://i.postimg.cc/yNJ8sbzV/loggg.png)

### Thanks for reading
