---
title: nmap
date: 2021-09-12
description: "Deep Dive Into Nmap Scan Techniques and Complete Guide to Nmap | Nmap Tutorial"
image: images/nmap/Green and Black Geometric Techno Technology YouTube Channel Art.png
---

### What is NMAP

Nmap is a free and open-source network scanner created by Gordon Lyon. Nmap is used to discover hosts and services on a computer network by sending packets and analyzing the responses. Nmap provides a number of features for probing computer networks, including host discovery and service and operating system detection.

### What Does Nmap Do?

Nmap (Network Mapper) is an open source and free security scanner used for network discovery and security auditing. During a scan, Nmap sends specially crafted packets to the target host and then analyzes the responses. It is capable of
Host DiscoveryPort ScanningService Name and Version DetectionOS DetectionThe typical uses of Nmap include:Security Audits Of A Firewall / HostOpen Port IdentificationNetwork Security AuditNetwork Mapping, Network Inventory, Asset ManagementVulnerability Detection & ExploitationHost / Service Uptime MonitoringNmap can work on Linux, Unix, BSDs, MacOS X and Windows.

### How To Install Nmap 

*To install NMAP on Ubuntu, run the command.*
- sudo apt-get install nmap 

*To install NMAP on Arch, run the command.*
 - sudo pacman -S nmap 
 
*Here are the steps to install Nmap on Windows:*

1. Browse to  [https://nmap.org/download.html](https://nmap.org/download.html)  and download the latest self-installer:
2. Run the downloaded *.exe* file. In the window that opens, accept the license terms:
3. Choose the components to install. By default, the *Zenmap GUI* will be installed:
4. Select the install location and click *Install*:
5. The installation should be completed in a couple of minutes.

Done! You can now use  `nmap`.


### How to use NMAP 

*NMAP Target Selection* 


-  Scan a single IP  **nmap 192.168.1.1**
- Scan a host **nmap www.hacksec.in**
- Scan a range of IPs **nmap 192.168.1.1-20**
- Scan a subnet **nmap 192.168.1.0/24** 
- Scan targets from a text file **nmap -iL list-of-ips.txt**

These are all default scans, which will scan 1000 TCP ports. Host discovery will take place. 


*NMAP Port Selection*


- Scan a single Port **nmap -p 22 192.168.1.1**
- Scan a range of ports **nmap -p 1-100 192.168.1.1**
- Scan 100 most common ports (Fast) **nmap -F 192.168.1.1**
- Scan all 65535 ports **nmap -p- 192.168.1.1** 


*Nmap Port Scan types*


- Scan using TCP connect **nmap -sT 192.168.1.1**
- Scan using TCP SYN scan (default) **nmap -sS 192.168.1.1**
- Scan UDP ports **nmap -sU -p 123,161,162 192.168.1.1**
- Scan selected ports - ignore discovery **nmap -Pn -F 192.168.1.1**

Privileged access is required to perform the default  `SYN`  scans. If privileges are insufficient a TCP connect scan will be used. A TCP connect requires a full TCP connection to be established and therefore is a slower scan. Ignoring discovery is often required as many firewalls or hosts will not respond to  `PING`, so could be missed unless you select the  `-Pn`  parameter. Of course this can make scan times much longer as you could end up sending scan probes to hosts that are not there.

*Service and OS Detection* 

- Detect OS and Services **nmap -A 192.168.1.1** 
- Standard service detection **nmap -sV 192.168.1.1**
- More aggressive Service Detection **nmap -sV --version-intensity 5 192.168.1.1**
- Lighter banner grabbing detection **nmap -sV --version-intensity 0 192.168.1.1** 

Service and OS detection rely on different methods to determine the operating system or service running on a particular port. The more aggressive service detection is often helpful if there are services running on unusual ports. On the other hand the lighter version of the service will be much faster as it does not really attempt to detect the service simply grabbing the banner of the open service. 

*Nmap Output Formats*  

- Save default output to file **nmap -oN outputfile.txt 192.168.1.1** 
- Save results as XML **nmap -oX outputfile.xml 192.168.1.1** 
- Save results in a format for grep **nmap -oG outputfile.txt 192.168.1.1** 
- Save in all formats **nmap-oA outputfile 192.168.1.1** 

The default format could also be saved to a file using a simple file redirect `command > file`. Using the `-oN` option allows the results to be saved but also can be monitored in the terminal as the scan is under way. 

*Deeper  scan with NSE Scripts*

- Scan using default safe scripts **nmap -sV -sC 192.168.1.1** 
- Get help for a script **nmap --script-help=ssl-heartbleed**
- Scan using a specific NSE script **nmap -sV -p 443 –script=ssl-heartbleed.nse 192.168.1.1** 
- Scan with a set of scripts **nmap -sV --script=smb 192.168.1.1*** 

According to my Nmap install there are currently  *581 NSE scripts*. The scripts are able to perform a wide range of security related testing and discovery functions. If you are serious about your network scanning you really should take the time to get familiar with some of them.

The option  `--script-help=$scriptname`  will display help for the individual scripts. To get an easy list of the installed scripts try  `locate nse | grep script`.

You will notice I have used the  `-sV`  service detection parameter. Generally most NSE scripts will be more effective and you will get better coverage by including service detection.

 *A scan to search for DDOS reflection UDP services*
 
 - Scan for UDP DDOS reflectors  **nmap –sU –A –PN –n –pU:19,53,123,161 –script=ntp-monlist,dns-recursion,snmp-sysdescr 192.168.1.0/24**
 
UDP based DDOS reflection attacks are a common problem that network defenders come up against. This is a handy Nmap command that will scan a target list for systems with open UDP services that allow these attacks to take place

*HTTP Service Information*

- Gather page titles from HTTP services **nmap --script=http-title 192.168.1.0/24**
- Get HTTP headers of web services **nmap --script=http-headers 192.168.1.0/24**
- Find web apps from known paths **nmap --script=http-enum 192.168.1.0/24**

There are many HTTP information gathering scripts, here are a few that are simple but helpful when examining larger networks. Helps in quickly identifying what the HTTP service that is running on the open port. Note the `http-enum` script is particularly noisy. It is similar to Nikto in that it will attempt to enumerate known paths of web applications and scripts. This will inevitably generated hundreds of `404 HTTP responses` in the web server error and access logs.

*Detect Heartbleed SSL Vulnerability*

- Heartbleed Testing **nmap -sV -p 443 --script=ssl-heartbleed 192.168.1.0/24** 

Heartbleed detection is one of the available SSL scripts. It will detect the presence of the well known Heartbleed vulnerability in SSL services. Specify alternative ports to test SSL on mail and other protocols. 

*IP Address information*

Find Information about IP address
**nmap --script=asn-query,whois,ip-geolocation-maxmind 192.168.1.0/24**

Gather information related to the IP address and netblock owner of the IP address. Uses ASN, whois and geoip location lookups. 

### Remote Scanning

Testing your network perimeter from an external perspective is key when you wish to get the most accurate results. By assessing your exposure from the attackers perspective you can validate firewall rule audits and understand exactly what is allowed into your network. To enable remote scanning easily and effectively because anyone who has played with  `shodan.io`  knows very well how badly people test their perimeter networks. 

*NMAP ping sweep*

Nmap “ping sweep”  is a method to discover connected devices in a network using the nmap security scanner, for a device to be discovered we only need it to be turned on and connected to the network. We can tell nmap to discover all devices in the network or define ranges. In contrast to other types of scanning ping sweep is not an aggressive scan as these we previously explained on LinuxHint to scan for services and vulnerabilities using nmap, for ping sweep we can skip some of nmap’s regular stages in order to discover hosts only and make harder for the target to detect the scan.

*Getting started with ping sweep* 

First of all let’s know about our network by typing *ifconfig*:

- ifconfig enp2s0

Now let’s say we want to discover all hosts available after 172.31.X.X, nmap allows us to define IP ranges and to define sub ranges within each octet. For this we’ll use nmap’s old flag (parameter) -sP, the parameter is still useful but was replaced for *-sn* which will be explained later.

- nmap  -sP 172.31.1-255.1-255 

*-sP*: tells nmap no to do a port scan after host discovery.

As you can see nmap returns the available hosts and their IP and MAC addresses but no information on ports.

We can also try it with the last octet:

- nmap  -sP 172.31.1.1-255

The flag *-sn* (No port scan) replaces the *-sP* you just tried. 

- nmap -sn 172.31.1.1-255

As you can see the output is similar to the previous scan, no information on ports.

The parameter  *-Pn* (no ping) will scan ports of the network or provided range without checking if the device is online, it wont ping and won’t wait for replies. This shouldn’t be called ping sweep but it is useful to discover hosts, In the terminal type: 

- nmap -Pn 172.31.1.1-255 

*Note:*  if you want nmap to scan the whole range of an octet you can replace 1-255 for wildcard (*).

The parameter -sL (List scan) is the less offensive one, it enumerates the IP addresses in the network and tries to resolve through reverse-DNS lookup (resolve from ip to host) to know the hosts are there. This command is useful to print a list of hosts, In the terminal type: 

- nmap -sL 172.31.1.1-255 

Now let’s assume we want to scan the whole network with *NO PORT SCAN* excluding a specific device, run:

- nmap  -sn 172.31.1.1-255  --exclude 172.31.124.141 

In this network we have only two devices with IP 172.31.124.X, nmap scanned the whole network finding only one and excluding the second according to the passed instruction *–exclude. As you see with the ping response the IP *172.31.124.142** is available despite being undetected by nmap. 

## Discovery Options

*TCP SYN Ping*

Short for synchronize, SYN is *a TCP packet sent to another computer requesting that a connection be established between them*. If the SYN is received by the second machine, an SYN/ACK is sent back to the address requested by the SYN.

- TCP SYN Ping **nmap -PS 192.168.0.1** 

*TCP ACK Ping*

Similar to the TCP SYN ping scan, the TCP ACK ping scan is *used to determine if a host is responding*. It can be used to detect hosts that block SYN packets or ICMP echo requests, but it will most likely be blocked by modern firewalls that track connection states. 

- TCP ACK ping **nmap -PA 192.168.0.1** 

*UDP Ping*

Ping scans are used to determine if a host is responding and can be considered online. UDP ping scans have the advantage of being capable of detecting systems behind firewalls with strict TCP filtering leaving the UDP traffic forgotten. 

- UDP ping **nmap -PU 192.168.0.1** 

*SCTP INIT Ping* 

SCTP packets can be used to determine if a host is online by sending SCTP INIT packets and looking for ABORT or INIT ACK responses. Nmap implements this effective technique named SCTP INIT ping scan. 

- SCTP INIT Ping **nmap -PY 192.168.0.1** 

*ICMP Echo Ping*

Ping works by *sending an Internet Control Message Protocol (ICMP) Echo Request to a specified interface on the network and waiting for a reply*. When a ping command is issued, a ping signal is sent to a specified address. When the target host receives the echo request, it responds by sending an echo reply packet.

- IMCP echo ping **nmap -PE 192.168.0.1** 

*ICMP Timestamp Ping*

Ping sends ICMP *Echo Request messages once a second*. A ping packet also includes a timestamp from the sending host. When an Echo Reply is received the round-trip time is calculated and displayed. Ping is your first tool to determine if a network layer path exists between two hosts.

- ICMP Timestamp Ping **nmap -PP 192.168.0.1** 

*IP Protocol Ping*

Ping is a computer network administration software utility used to test the reachability of a host on an Internet Protocol (IP) network.Ping measures the *round-trip time for messages* sent from the originating host to a destination computer that are echoed back to the source.

- IP Protocol Ping **nmap -PO 192.168.0.1** 

*ARP Ping*

ARP stands for *Address Resolution Protocol*. When you try to ping an IP address on your local network, say 192.168. 1.1, your system has to turn the IP address 192.168. 1.1 into a MAC address. This involves using ARP to resolve the address, hence its name. 

- ARP Ping **nmap -PR 192.168.0.1** 

*Traceroute*

The option –traceroute is *used to trace all hops or intermediating routers*. The column RTT (Round Trip Time or latency) shows the speed in milliseconds for each hop including return from that HOP, this is especially useful to diagnose connection issues.

- Traceroute **nmap –traceroute 192.168.0.1** 

*Force Reverse DNS Resolution* 

In computer networks, a reverse DNS lookup or reverse DNS resolution (rDNS) is *the querying technique of the Domain Name System (DNS) to determine the domain name associated with an IP address* – the reverse of the usual "forward" DNS lookup of an IP address from a domain name.

- Force Reverse DNS Resolution **nmap -R 192.168.0.1** 

*Alternative DNS Lookup*

The *–system-dns* option instructs Nmap to use the host system’s DNS resolver instead of its own internal method.

- Alternative DNS Lookup **nmap –system-dns 192.168.0.1** 

*Manually Specify DNS Server(s)*

The *–dns-servers* option is used to manually specify DNS servers to be queried when scanning.
The *–dns-servers* option allows you to specify one or more alternative servers for Nmap to query. This can be useful for systems that do not have DNS configured or if you want to prevent your scan lookups from appearing in your locally configured DNS server’s log file.

- Manually Specify DNS Server **nmap –dns-servers 201.56.212.54 192.168.0.1**

*Create a Host List*

The *-sL* option will display a list and performs a reverse DNS lookup of the specified IP addresses. 

- Create a Host List **nmap -sL 192.168.0.1/24** 

## Advanced Scanning Options 

*TCP SYN Scan*

For scan advanced TCP SYN scan you can use cmnd given below:-

- TCP SYN scan **nmap -sS 192.168.0.1** 

*TCP Connect Scan*

For advanced use of TCP Connect Scan cmnd given below:- 

- TCP Connect Scan **nmap -sT 192.168.0.1** 

*UDP Scan*

For advanced use for UDP scan cmnd given below:-

- UDP scan **nmap -sU 192.168.0.1**

*TCP NULL Scan* 

Description. An adversary uses a TCP NULL scan *to determine if ports are closed on the target machine*. This scan type is accomplished by sending TCP segments with no flags in the packet header, generating packets that are illegal based on RFC 793. 

- TCP Null Scan **nmap -sN 192.168.0.1**

*TCP FIN Scan*

An adversary uses a TCP FIN scan to determine if ports are closed on the target machine. This scan type is accomplished by sending TCP segments with the FIN bit set in the packet header. The RFC 793 expected behavior is that any TCP segment with an out-of-state Flag sent to an open port is discarded, whereas segments with out-of-state flags sent to closed ports should be handled with a RST in response.

- TCP FIN Scan **nmap -sF 192.168.0.1** 

*Xmas Scan*

Xmas scans derive *their name from the set of flags that are turned on within a packet*. These scans are designed to manipulate the PSH, URG and FIN flags of the TCP header. 

- Xmas Scan **nmap -sX 192.168.0.1** 

*TCP ACK Scan* 

This type of scanning is rarely useful alone, but when combined with SYN scanning, gives a more complete picture of the type of firewall rules that are present. When a TCP ACK segment is sent to a closed port, or sent out-of-sync to a listening port, the RFC 793 expected behavior is for the device to respond with a RST. 

- TCP ACK Scan **nmap -sA 192.168.0.1** 

*Custom TCP Scan*

Truly advanced Nmap users need not limit themselves to the canned scanned types. The `--scanflags` option allows you to design your own scan by specifying arbitrary TCP flags. 

- Custom TCP Scan **nmap –scanflags SYNFIN 192.168.0.1** 

*IP Protocol Scan* 

Internet Protocol Scan – *a process of probing a server or host looking for any open ports*. IP scans are typically precursors to attacks, as they identify which hosts are running which services that may be vulnerable to attacks. 

- IP Protocol Scan **nmap -sO 192.168.0.1** 

*Send Raw Ethernet Packets* 

A raw socket is used to receive raw packets. This means *packets received at the Ethernet layer will directly pass to the raw socket*. Stating it precisely, a raw socket bypasses the normal TCP/IP processing and sends the packets to the specific user application.

- Send Raw Ethernet Packets **nmap –send-eth 192.168.0.1** 

*Send IP Packets*

A network packet is a small amount of data sent over *Transmission Control Protocol/Internet Protocol* (TCP/IP) networks. A packet is the unit of data routed between an origin and a destination on the internet or other packet-switched network -- or networks that ship data around in small packets. 

- Send Ip Packets **nmap –send-ip 192.168.0.1** 

## Port Scanning Options 

*Perform a Fast Scan*

Nmap can reveal open services and ports by IP address as well as by domain name. If you need to perform a scan quickly, you can use *the “-F” flag*. The “-F” flag will list ports on the nmap-services files. Because the -F “Fast Scan” flag does not scan as many ports, it isn't as thorough. 

- Perform a fast scan **nmap -F 192.168.0.1**

*Scan Specific Ports*

command given below will initiate a default scan against the target host and look for port 80-25,80,139,8080

- Scan Specific Ports **nmap -p 80-25,80,139,8080 192.168.1.1** 

*Scan Ports by Name*  

Command given below will initiate a scan against the target host looking for ports associated with specified service names. 

- Scan ports by name **nmap -p ftp,http 192.168.0.1***

*Scan Ports by Protocol*

In computer networking, a protocol *defines a standard way for computers to exchange information*. ... Network clients use different ports (or channels) to transfer this data. Generally one port is used to send data and another to receive it, so packets don't collide.
 
 - Scan ports by protocol **nmap -sU -sT -p U:53,111,137,T:21- 25,80,139,8080 192.168.0.1**
 
 *Scan All Ports*
 
The command given below will initiate a scan against the target host looking for all ports (1-65535). 

- Scan all posts **nmap -p ‘’ 192.168.0.1***

*Scan Top Ports*

The –top-ports option lets you specify the number of ports you wish to scan in each protocol, and will pick the most popular ports for you based on the new frequency data. For both TCP and UDP, the top 10 ports gets you roughly half of the open ports.

- Scan top ports **nmap –top-ports 10 192.168.0.1**

*Perform a Sequential Port Scan*

By default, Nmap randomizes the scanned port order (except that certain commonly accessible ports are moved near the beginning for efficiency reasons). This randomization is normally desirable, but you can specify `-r` for sequential (sorted from lowest to highest) port scanning instead.

- Perform a Sequential Port Scan **nmap -r 192.168.0.1** 

## Version Detection 

*Operating System Detection*

One of Nmap's best-known features is remote OS detection using TCP/IP stack fingerprinting. Nmap sends a series of TCP and UDP packets to the remote host and examines practically every bit in the responses. After performing dozens of tests such as TCP ISN sampling, TCP options support and ordering, IP ID sampling, and the initial window size check, Nmap compares the results to its `nmap-os-db` database of more than 2,600 known OS fingerprints and prints out the OS details if there is a match. 

- Operating System Detection **nmap -O 192.168.0.1**  

*Attempt to Guess an Unknown OS* 

If Nmap says there are no matches close enough to print, something is probably wrong. Maybe a firewall or NAT box in the way is modifying the probe or response packets. This can cause a hybrid situation where one group of tests look like they are from one OS, while another set look completely different. Adding the `--osscan-guess` may give more clues as to what is running.

- Attempt to Guess an Unknown OS **nmap -O –osscan-guess 192.168.0.1**

*Service Version Detection*

Version detection is enabled and controlled with the following options:

`-sV`  (Version detection)

- Version detection **nmap -sV 192.168.0.1** 

*Troubleshooting Version Scans*

This causes Nmap to print out extensive debugging info about what version scanning is doing. It is a subset of what you get with.

- Troubleshooting Version Scans **nmap -sV –version-trace 192.168.0.1** 

*Perform a RPC Scan*

An adversary scans for RPC services listing on a Unix/Linux host. This type of scan can be obtained via native operating system utilities or via port scanners like nmap. When performed by a scanner, an RPC datagram is sent to a list of UDP ports and the response is recorded. Particular types of responses can be indicative of well-known RPC services running on a UDP port. Direct RPC scans that bypass portmapper/sunrpc are typically slow compare to other scan types, are easily detected by IPS/IDS systems, and can only detect open ports when an RPC service responds.

- Perform a RPC Scan **nmap -sR 192.168.0.1** 

## Firewall Evasion Techniques 

*Augment Packets* 

The `-f` option causes the requested scan (including host discovery scans) to use tiny fragmented IP packets. The idea is to split up the TCP header over several packets to make it harder for packet filters, intrusion detection systems, and other annoyances to detect what you are doing. Be careful with this! Some programs have trouble handling these tiny packets.

- Augment Packets **nmap -f 192.168.0.1**

*Pacify a Specific MTU*

Don't also specify `-f` if you use `--mtu`. The offset must be a multiple of eight. While fragmented packets won't get by packet filters and firewalls that queue all IP fragments, such as the `CONFIG_IP_ALWAYS_DEFRAG` option in the Linux kernel, some networks can't afford the performance hit this causes and thus leave it disabled. Others can't enable this because fragments may take different routes into their networks. Some source systems defragment outgoing packets in the kernel. 

- Pacify a Specific MTU **nmap –mtu 32 192.168.0.1**

*Use a Decoy* 


Causes a decoy scan to be performed, which makes it appear to the remote host that the host(s) you specify as decoys are scanning the target network too. Thus their IDS might report 5–10 port scans from unique IP addresses, but they won't know which IP was scanning them and which were innocent decoys. While this can be defeated through router path tracing, response-dropping, and other active mechanisms, it is generally an effective technique for hiding your IP address.

- Use a decoy **nmap -D RND:10 192.168.0.1**

*Zombie Scan*

Attackers can actually scan a target without sending a single packet to the target from their own IP address! Instead, a clever side-channel attack allows for the scan to be bounced off a dumb “zombie host”. Intrusion detection system (IDS) reports will finger the innocent zombie as the attacker. Besides being extraordinarily stealthy, this scan type permits discovery of IP-based trust relationships between machines. 

- Zombie scan **nmap -sI 192.168.0.38**

*Manually Specify a Source Port*

Nmap offers the -g and --source-port options (they are equivalent) to exploit these weaknesses. Simply provide a port number, and Nmap will send packets from that port where possible. Nmap must use different port numbers for certain OS detection tests to work properly. Most TCP scans, including SYN scan, support the option completely, as does UDP scan.

- Manually Specify a Source Port **nmap –source-port 10 192.168.0.1**

*Randomize Target Scan Order*

Nmap offers the --randomize-hosts option which *splits up the target networks into blocks of 16384 IPs*, then randomizes the hosts in each block. If you are scanning a huge network, such as class B or larger, you may get better (more stealthy) results by randomizing larger blocks.

- Randomize Target Scan Order **nmap –randomize-hosts 192.168.0.1-20** 

*Spoof MAC Address*

MAC spoofing can allow us to fake the origin of our connections and can be helpful to evade IDS systems. It is possible to spoof your MAC address while performing an ARP ping scan. Use --spoof-mac to set a new MAC address:

- Spoof MAC address **nmap -sn -PR --spoof-mac <mac address> 192.168.0.1** 

*Send Bad Checksums*

Asks Nmap to use an invalid TCP, UDP or SCTP checksum for packets sent to target hosts. Since virtually all host IP stacks properly drop these packets, any responses received are likely coming from a firewall or IDS that didn't bother to verify the checksum.

- Send bad checksums **nmap –badsum 192.168.0.1** 

## Troubleshooting And Debugging

*Display Nmap Version*

Increases the verbosity level, causing Nping to print more information during its execution. There are 9 levels of verbosity (-4 to 4). Every instance of  `-v`  increments the verbosity level by one (from its default value, level 0). Every instance of option  `-q`  decrements the verbosity level by one. Alternatively you can specify the level directly, as in  `-v3`  or  `-v-1`. These are the available levels:

Level -4

No output at all. In some circumstances you may not want Nping to produce any output (like when one of your work mates is watching over your shoulder). In that case level -4 can be useful because although you won't see any response packets, probes will still be sent.

Level -3

Like level -4 but displays fatal error messages so you can actually see if Nping is running or it failed due to some error.

Level -2

Like level -3 but also displays warnings and recoverable errors.

Level -1

Displays traditional run-time information (version, start time, statistics, etc.) but does not display sent or received packets.

Level 0

This is the default verbosity level. It behaves like level -1 but also displays sent and received packets and some other important information.

Level 1

Like level 0 but it displays detailed information about timing, flags, protocol details, etc.

Level 2

Like level 1 but displays very detailed information about sent and received packets and other interesting information.

Level 3

Like level 2 but also displays the raw hexadecimal dump of sent and received packets.

Level 4 and higher

Same as level 3.

- Nmap Version **nmap -V**

*Debugging*

When even verbose mode doesn't provide sufficient data for you, debugging is available to flood you with much more! As with the `-v`, debugging is enabled with a command-line flag `-d` and the debug level can be increased by specifying it multiple times. There are 7 debugging levels (0 to 6). Every instance of `-d` increments debugging level by one. Provide an argument to `-d` to set the level directly; for example `-d4`.

- Debugging nmap -d 192.168.0.1

*Only Display Open Ports*

Nmap has the option *--open* , which will filter out all the other potential states. If you are scanning under Linux, you could also use grep to achieve a very similar result.

- Nmap display open ports **nmap –open 192.168.0.1**

*Trace Packets*

Technique Involves in packet-tracing via nmap

The nmap module is an interface with nmap's internal functions and data structures. The API offers target host information such as port states and version detection results. It also provides an interface to the Nsock library for effective network I/O.

- Trace Packets **nmap –packet-trace 192.168.0.1** 

## NMAP Scripting Engine 

*Execute Individual Scripts*

While NSE has a complex implementation for efficiency, it is strikingly easy to use. Simply specify `-sC` to enable the most common scripts. Or specify the `--script` option to choose your own scripts to execute by providing categories, script file names, or the name of directories full of scripts you wish to execute. 

- Individual Scripts **nmap –script banner.nse 192.168.0.1**

*Execute Multiple Scripts* 

Loads all scripts whose name starts with `http-`, such as `http-auth` and `http-open-proxy`. The argument to `--script` had to be in quotes to protect the wildcard from the shell. 

- Nmap multiple script **nmap –script ‘http-’ 192.168.0.1*** 

*Script Categories*

NSE scripts define a list of categories they belong to. Currently defined categories are `auth`, `broadcast`, `brute`, `default`. `discovery`, `dos`, `exploit`, `external`, `fuzzer`, `intrusive`, `malware`, `safe`, `version`, and `vuln`. Category names are not case sensitive. 

- Execute Scripts by Category **nmap –script ‘not intrusive’ 192.168.0.1**

*Execute Multiple Script Categories*

Nmap Execute more than one script in same time

- Multiple Script Categories **nmap –script ‘default or safe’ 192.168.0.1**

*Troubleshoot Scripts*

This option is similar to `--packet-trace`, but works at the application level rather than packet by packet. If this option is specified, all incoming and outgoing communication performed by scripts is printed. The displayed information includes the communication protocol, source and target addresses, and the transmitted data. If more than 5% of transmitted data is unprintable, hex dumps are given instead. Specifying `--packet-trace` enables script tracing too

- Troubleshoot Scripts **nmap –script banner.nse –script-trace 192.168.0.1**

*Update the Script Database*

This option updates the script database found in `scripts/script.db` which is used by Nmap to determine the available default scripts and categories. It is only necessary to update the database if you have added or removed NSE scripts from the default `scripts` directory or if you have changed the categories of any script. This option is used by itself without arguments: 

- *nmap --script-updatedb*.

### Thanks for reading