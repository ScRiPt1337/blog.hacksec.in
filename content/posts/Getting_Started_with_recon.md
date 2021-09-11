---
title: Recon
date: 2021-09-11
description: "Hello guys today we will learn about reconnaissance"
image: images/recon/Pink and Maroon Neon Noir  Vaporwave Action  Adventure YouTube Channel Art.png
---

## Reconnaissance

So here is our another article regarding recon... 

Reconnaissance attacks are general knowledge gathering attacks


### Google dork
 
 A Google query, sometimes just referred to as a dork, is a search string that uses advanced search operators to find information that is not readily available on a website

#### Some google dork example

- site:".uk" intitle:"admin login" [Pages Containing Login Portals]

- "Not for Public Release" + "Confidential" ext:pdf | ext:doc | ext:xlsx [Files Containing Juicy Info]

- intitle:"index of" "contacts.txt" [text
Files Containing Juicy Info]

- Here you can check out more google dork list https://www.exploit-db.com/google-hacking-database 

### History of dorking

Google dorking has been documented since the early 2000s.

Johnny Long,  was a pioneer of dorking. He first posted his definition of the newly coined term, google Dork, in 2002. Since then, its meaning has evolved to include other usages.

A dork refines that query, by combining technical and semantic elements, in order to take full advantage of the fact that web content is being constantly scanned and indexed by machines.

In a 2011  **[interview](http://www.techrepublic.com/blog/it-security/google-hacking-its-all-about-the-dorks/)**, Johnny Long said:

> “In the years I’ve spent as a professional hacker, I’ve learned that the simplest approach is usually the best. As hackers, we tend to get down into the weeds, focusing on technology, not realising there may be non-technical methods at our disposal that work as well or better than their high-tech counterparts. I always kept an eye out for the simplest solution to advanced challenges.”

### How dorking works

In everyday use, search engines like Google, Bing, DuckDuckGo and Yahoo accept a search term (a word).
But most search engines are programmed to accept more advanced “filters” as well. A filter is a keyword or phrase that has particular meaning for the search engine. This includes terms like 

-    `cache`: this dork will show you the cached version of any website, e.g.  `cache:hacksec.in`

-    `allintext`: searches for specific text contained on any web page, e.g.  `allintext: hacking tools`

-   `allintitle`: exactly the same as allintext, but will show pages that contain titles with X characters, e.g.  `allintitle:"Security Companies"`

-   `allinurl`: it can be used to fetch results whose URL contains all the specified characters, e.g:  `allinurl: security`

-   `filetype`: used to search for any kind of file extensions, for example, if you want to search for pdf files you can use:  `email security filetype: pdf`

-   `inurl`: this is exactly the same as  `allinurl`, but it is only useful for one single keyword, e.g.  `inurl: security`

-   `intext`: useful to locate pages that contain certain characters or strings inside their text, e.g.  `intext:"bug bounty"`

-   `site`: will show you the full list of all indexed URLs for the specified domain and subdomain, e.g.  `site:hacksec.in`

-   `inanchor`: this is useful when you need to search for an exact anchor text used on any links, e.g.  `inanchor:"cyber security"`

### Example
How we can find backdoor's in websites using dorks 
![google_dork](/images/recon/1.png)
![google result](/images/recon/2.png)
![webshell](/images/recon/3.jpg)

### NMAP

[Nmap](https://nmap.org/)  is one of the most popular and widely used security auditing tools, its name means "Network Mapper". Is a free and open source utility utilized for security auditing and network exploration across local and remote hosts.

Some of the main features include:

-   Host detection: Nmap has the ability to identify hosts inside any network that have certain ports open, or that can send a response to ICMP and TCP packets.
-   IP and DNS information detection: including device type, Mac addresses and even reverse DNS names.
-   Port detection: Nmap can detect any port open on the target network, and let you know the possible running services on it.
-   OS detection: get full OS version detection and hardware specifications of any host connected. 
-   Version detection: Nmap is also able to get application name and version number.

### Shodan

[Shodan](https://www.shodan.io/)  is a network security monitor and search engine focused on the deep web & the internet of things. It was created by John Matherly in 2009 to keep track of publicly accessible computers inside any network.

It is often called the 'search engine for hackers', as it lets you find and explore a different kind of devices connected to a network like servers, routers, webcams, and more.

Shodan is pretty much like Google, but instead of showing you fancy images and rich content / informative websites, it will show you things that are more related to the interest of IT security researchers like SSH, FTP, SNMP, Telnet, RTSP, IMAP and HTTP server banners and public information. Results will be shown ordered by country, operating system, network, and ports.

Shodan users are not only able to reach servers, webcams, and routers. It can be used to scan almost anything that is connected to the internet, including but not limited to traffic lights systems, home heating systems, water park control panels, water plants, nuclear power plants, and much more.

### Fuzz Faster U Fool (ffuf)
[ffuf](https://github.com/ffuf/ffuf)  is a Fast web fuzzer written in Go. it's very useful to find the hidden directory.

### AWSBucketDump

[AWSBucketDump](https://github.com/jordanpotti/AWSBucketDump) is a tool to quickly enumerate AWS S3 buckets to look for loot. It's similar to a subdomain bruteforcer but is made specifically for S3 buckets and also has some extra features that allow you to grep for delicious files as well as download interesting files if you're not afraid to quickly fill up your hard drive.

### Aquatone
[Aquatone](https://github.com/michenriksen/aquatone) is a tool for visual inspection of websites across a large amount of hosts and is convenient for quickly gaining an overview of HTTP-based attack surface.

### Enum4linux-ng

[Enum4linux-ng](https://github.com/cddmp/enum4linux-ng) is a tool for enumerating information from Windows and Samba systems, aimed for security professionals and CTF players. The tool is mainly a wrapper around the Samba tools nmblookup, net, rpcclient and smbclient.

### Recon-Ng

[Recon-ng](https://github.com/lanmaster53/recon-ng)  comes already built in the Kali Linux distribution and is another great tool used to perform quickly and thoroughly reconnaissance on remote targets.

This web reconnaissance framework was written in Python and includes many modules, convenience functions and interactive help to guide you on how to use it properly.

The simple command-based interface allows you to run common operations like interacting with a database, run web requests, manage API keys or standardizing output content.

Fetching information about any target is pretty easy and can be done within seconds after installing. It includes interesting modules like google_site_web and bing_domain_web that can be used to find valuable information about the target domains.

While some recon-ng modules are pretty passive as they never hit the target network, others can launch interesting stuff right against the remote host. 

### BuiltWith

[BuiltWith](https://builtwith.com/)  is a cool way to detect which technologies are used at any website on the internet.

It includes full detailed information about CMS used like Wordpress, Joomla, Drupal, etc, as well as full depth Javascript and CSS libraries like jquery, bootstrap/foundation, external fonts, web server type (Nginx, Apache, IIS, etc), SSL provider as well as web hosting provider used.

BuiltWith also lets you find which are the most popular technologies running right now, or which ones are becoming trending.

Without any doubt, it is a very good open source intelligence tool to gather all the possible technical details about any website. 

### Censys

[Censys](https://censys.io/)  is a wonderful search engine used to get the latest and most accurate information about any device connected to the internet, it can be servers or domain names.

You will be able to find full geographic and technical details about 80 and 443 ports running on any server, as well as HTTP/S body content & GET response of the target website, Chrome TLS Handshake, full SSL Certificate Chain information, and WHOIS information. 

### Fierce

[Fierce](https://github.com/mschwager/fierce)  is an IP and DNS recon tool written in PERL, famous for helping IT sec professionals to find target IPs associated with domain names.

It was written originally by RSnake along with other members of the old http://ha.ckers.org/. It's used mostly targetting local and remote corporate networks.

Once you have defined your target network, it will launch several scans against the selected domains and then it will try to find misconfigured networks and vulnerable points that can later leak private and valuable data.

The results will be ready within a few minutes, a little bit more than when you perform any other scan with similar tools like Nessus, "Nikto: a Practical Website Vulnerability Scanner"), Unicornscan, etc. 

### Wappalyzer

[Wappalyzer](https://www.wappalyzer.com/)  is a highly useful service that allows security researchers to quickly identify technologies on websites. With it, you can find a complete list of details for any technology stack running on any website. It also allows you to build lists of websites that use certain technologies, letting you add phone numbers and email addresses as well.

Their free plan includes instant results and up to 50 free monthly lookups. It’s perfect for tracking website technologies, discovering old/vulnerable software, finding organic data about your competitors, and last but not least, can be quickly triggered from the web browser with their Chrome/Firefox extensions.

If that isn’t enough, they also offer a handy API to automate technology lookups, and you can even set up website alerts to monitor your competition

### Metagoofil

[Metagoofil](https://tools.kali.org/information-gathering/metagoofil)  is another great intel-reconnaissance tool that aims to help infosec researchers, IT managers, and red teams to extract metadata from different types of files, such as:

-   doc
-   docx
-   pdf
-   xls
-   xlsx
-   ppt
-   pptx

How does it work? This app performs a deep search on search engines like Google, focusing on these types of files. Once it detects such a file, it will download it to your local storage, then proceed to extract all of its valuable data.

Once the extraction is complete, you'll see a full report with usernames, software banners, app versions, hostnames and more, a valuable resource for your recon phase.

Metagoofil also includes a number of options to help you filter the types of files to search for, refine the results and tweak the output, among many other useful features. 

### Exiftool

While a lot of OSINT tools focus on data found on public files such as PDF, .DOC, HTML, .SQL, etc., there are other tools that are specifically designed to extract critical Open Source Intelligence data from image, video and audio files.

[Exiftool](https://exiftool.org/)  reads, writes and extracts metadata from the following types of files:

-   EXIF
-   IPTC
-   GPS
-   XMP
-   JFIF
-   [And many others](https://exiftool.org/#supported?rel=nofollow,noopener,noreferrer&target=_blank)

It also supports native files from a wide range of cameras, such as: Canon, Casio, FujiFilm, Kodak, Sony, and many others. It's also conveniently available on multiple platforms including Linux, Windows and MacOS. 

### BigBountyRecon

[BigBountyRecon](https://github.com/Viralmaniar/BigBountyRecon) tool utilises 58 different techniques using various Google dorks and open source tools to expedite the process of initial reconnaissance on the target organisation. Reconnaissance is the most important step in any penetration testing or a bug hunting process. It provides an attacker with some preliminary knowledge on the target organisation. Furthermore, it will be useful to gain insights into what controls are in place as well as some rough estimations on the security maturity level of the target organisation.

This tool can be used in addition to your usual approach for bug hunting. The idea is to quickly check and gather information about your target organisation without investing time and remembering these syntaxes. In addition, it can help you define an approach towards finding some quick wins on the target. 

1.  Directory Listing: Finding open directories using Google Dork on your target organisation helps one to understand the directory structure on the webserver. It may reveal sensitive information or it may lead to information disclosure.
    
2.  Configuration Files: Often times configuration files contains sensitive information such as hardcoded passwords, sensitive drive locations or API tokens which can help you gain privilege access to the internal resources.
    
3.  Database Files: Database Files are data files that are used to store the contents of the database in a structured format into a file in separate tables and fields. Depending on the nature of the web application these files could provide access to sensitive information.
    
4.  WordPress: WordPress is an open-source CMS written in PHP. WordPress has thousands of plugins to build, customise and enhance the websites. There are numerous vulnerabilities in these plugins. Finding WordPress related
    
5.  Log Files: Log files sometimes provide detailed information of the users' activities in a particular application. These files are good to look at session cookies or other types of tokens.
    
6.  Backup and Old Files: Backup files are original copies of the critical systems. These provide access to PII or access to sensitive records.
    
7.  Login Pages: It is extremely important to identify login pages of your target organisation to perform bruteforce attempts or trying default credentials to gain further access to organisation resources.
    
8.  SQL Errors: SQL errors leaks sensitive information about the backend systems. This can help one to perform enumeration on the database types and see if the application is vulnerable to input validation related attacks such as SQL Injection.
    
9.  Apache Config Files: Apache HTTP Server is configured by placing directives in plain text configuration files. The main configuration file is usually called httpd.conf. In addition, other configuration files may be added using the Include directive, and wildcards can be used to include many configuration files. Any directive may be placed in any of these configuration files. Depending on the entries in these config files it may reveal database connection strings, username and passwords, the internal workings, used and referenced libraries and business logic of application.
    
10.  Robots.txt File: Robots.txt file instructs web robots how to crawl pages on their website. Depending on the content of the file, an attacker might discover hidden directories and files.
    
11.  DomainEye: DomainEye is a domain/host investigation tool that has the largest domain databases. They provide services such as reverse Whois, reverse IP lookup, as well as reverse NS and MX.
    
12.  Publicly Exposed Documents: Such documents can be used to extract metadata information.
    
13.  phpinfo(): Exposing phpinfo() on its own isn't necessarily a risk, but in combination with other vulnerabilities could lead to your site becoming compromised. Additionally, module versions could make attackers life easier when targeting application using newly discovered exploits.
    
14.  Finding Backdoors: This can help one to identify website defacements or server hijacking related issues. By exploiting the open redirect vulnerability on the trusted web application, the attacker can redirect victims to a phishing page.
    
15.  Install/Setup Files: Such files allows an attacker to perform enumeration on the target organisation. Information gathered using these files can help discover version details which can then be used to perform the targeted exploit.
    
16.  Open Redirects: With these, we look at various known parameters vulnerable to open redirect related issues.
    
17.  Apache Struts RCE: Successfully exploiting an RCE vulnerability could allow the attacker to run arbitrary programs. Here, we are looking for files with extensions of ".action" or ".do".
    
18.  3rd Party Exposure: Here we are looking for exposure of information on third party sites such as Codebeautify, Codeshare and Codepen.
    
19.  Check Security Headers: Identify quickly if the target site is using security related headers in the server response.
    
20.  GitLab: Quickly look for sensitive information on the GitLab.
    
21.  Find Pastebin Entries: Shows you the results related to the target organisation on the Pastebin site. This could be passwords or any other sensitive information related to the target organisation.
    
22.  Employees on LINKEDIN: Identifying employee names on LinkedIn can help you build a username list when it comes to password spraying attack.
    
23.  .HTACCESS / Sensitive Files: Look for sensitive file exposure. This may indicate a server misconfiguration.
    
24.  Find Subdomains: Subdomain helps you expand the attack surface on the target organisation. There are numerous tools available to automate the process of subdomain enumeration.
    
25.  Find Sub-Subdomains: Identify sub-sub domains on the target organisation using Google Dork,
    
26.  Find WordPress related exposure: WordPress related exposure helps you gain access to sensitive files and folders.
    
27.  BitBucket & Atlassian: Source code leakage, hardcoded credentials and access to cloud infrastructure.
    
28.  PassiveTotal: PassiveTotal is a great tool to perform threat investigation. Using BigBountyRecon we will use PassiveTotal to identify subdomains on the target information.
    
29.  Stackoverflow: Source code exposure or any technology-specific questions mentioned on the Stackoverflow.
    
30.  Find WordPress related exposure using Wayback Machine: Look for archieved WordPress files using WaybackMachine.
    
31.  GitHub: Quickly look for sensitive information on the GitHub.
    
32.  OpenBugBounty: Look for publicly exposed security issues on the OpenBugBounty website.
    
33.  Reddit: Information about the particular organisation on the Reddit platform.
    
34.  Crossdomain.xml: Look for misconfigured crossdomain.xml files on the target organisation.
    
35.  ThreatCrowd: Search engine for threats, however, we are going to use this to identify additional sub-domains.
    
36.  .git Folder: Source code exposure. it's possible to download the entire repository content if accessible.
    
37.  YouTube: Look for any recent news on Youtube.
    
38.  Digitalocean Spaces: Spaces is an S3-compatible object storage service that lets you store and serve large amounts of data. We will look for any data exposures.
    
39.  .SWF File (Google): Flash is dead. We are going to use Google Dorks to look for older versions of flash .swf's which contain vulnerabilities.
    
40.  .SWF File (Yandex): Flash is dead. We are going to use Yandex to look for older versions of flash .swf's which contain vulnerabilities.
    
41.  .SWF File (Wayback Machine): Flash is dead. We are going to use WaybackMachine to look for older versions of flash .swf's which contain vulnerabilities.
    
42.  Wayback Machine: Look for archived files to access old files.
    
43.  Reverse IP Lookup: Reverse IP Lookup lets you discover all the domain names hosted on any given IP address. This will help you to explore the attack surface for a target organisation.
    
44.  Traefik: Look for an open-source Edge Router for an unauthenticated interface which exposes internal services.
    
45.  Cloud Storage and Buckets: Google CSE for various cloud storages - aws, digitalocean, backblaze, wasabi, rackspace, dropbox, ibm, azure, dreamhost, linode, gcp, box, mailru
    
46.  s3 Buckets: Open s3 buckets.
    
47.  PublicWWW: Source code search engine indexes the content of over 200 million web sites and provides a query interface that lets the caller find any alphanumeric snippet, signature or keyword in the web pages ‘HTML’, ‘JavaScript’ and ‘CSS’ style sheet code.
    
48.  Censys (IPv4, Domains & Certs): Search engine for finding internet devices. We will use this to look for additional sub-domains using various endpoints on Censys.
    
49.  Shodan: Search engine for Internet-connected devices
    
50.  SharePoint RCE: Look for CVE-2020-0646 SharePoint RCE related endpoint.
    
51.  API Endpoints: Find WSDL files.
    
52.  Gist Searches: Quickly look for sensitive information on the Gist pastes.
    
53.  CT Logs: Certificate Transparency (CT) is an Internet security standard and open-source framework for monitoring and auditing digital certificates. We will use to look for additional sub-domains for a targeted organisation.
    
54.  Password Leak: Look for plaintext passwords of internal employees exposed in various leaks.
    
55.  What CMS: Identify the version and type of CMS used by a target organisation for targeted enumeration and exploit research.

### Thanks for reading
