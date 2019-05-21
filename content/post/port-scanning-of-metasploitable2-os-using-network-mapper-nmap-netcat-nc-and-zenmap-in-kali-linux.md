---
title: >-
  Port Scanning of Metasploitable2 OS using Network Mapper(nmap), NetCat (nc)
  and Zenmap in Kali Linux
date: '2019-05-21T21:03:32+05:30'
draft: true
categories:
  - networking
tags:
  - ''
autoThumbnailImage: false
---




## Finding the IP address of Metasploitable2 on the network using 

```
arp-scan -l
```

 

![]()

This command shows all the current available IP addresses on the local network (-l), here we can see that there are 4 usable IP addresses showing up. 



192.168.183.1 is the Default Gateway of the router

192.168.183.2 is the Default Gateway for VMware 

192.168.183.254 is the Broadcast Channel which broadcasts on the whole network

192.168.183.132 is the target IP address, Metasploitable2 here.



Commonly used ports with the respective protocols:

•	20 – FTP Data Transfer 

•	21 – FTP Command Control

•	22 – SSH 

•	23 – TELNET 

•	25 – SMTP

•	53 – DNS 

•	67, 68 – DHCP 

•	80 – HTTP

•	110 – POP3 

•	143 – IMAP 

•	443 – HTTPS





## Port Scanning using Network Mapper (nmap):

## 

```
nmap -sV <target IP>
```



Nmap (“Network Mapper”) is an open source tool for network exploration and security auditing. It was designed to rapidly scan large networks, although it works fine against single hosts. Nmap uses raw IP packets in novel ways to determine what hosts are available on the network, what services (application name and version) those hosts are offering, what operating systems (and OS versions) they are running, what type of packet filters/firewalls are in use, and dozens of other characteristics. While Nmap is commonly used for security audits, many systems and network administrators find it useful for routine tasks such as network inventory, managing service upgrade schedules, and monitoring host or service uptime.



The switch used here is -sV , using nmap -h : 

```
-sV: Probe open ports to determine service/version info
```

 

It automatically checks for the most commonly used ports using TCP method by default.





## Port Scanning using NetCat (nc):



nc -z -v <target IP> <range of ports> 		(1-1023 are the server end and most used ports)























Netcat is a simple unix utility which reads and writes data across network connections, using TCP or UDP protocol. It is designed to be a reliable "back-end” tool that can be used directly or easily driven by other programs and scripts.  At the same time, it is a feature-rich network debugging and exploration tool, since it can create almost any kind of connection you would need and has several interesting built-in capabilities.  Netcat, or "nc" as the actual program is named, should have been supplied long ago as another one of those cryptic but standard Unix tools.





The switches used here are -z and -v : 

```
 -z			zero-I/O mode [used for scanning]
```

```
-v			verbose [use twice to be more verbose
```

Now unlike nmap, we need to define the range of the port here, and since 1-1023 are the server end and most used ports, we used them only.



## Port Scanning using Zenmap:

 

![]()

Zenmap is a multi-platform graphical Nmap frontend and results viewer. Zenmap aims to make Nmap easy for beginners to use while giving experienced Nmap users advanced features.

Switches used here are -T4 , -A and -v

```
-T<0-5>: Set timing template (higher is faster)
```

```
-A: Enable OS detection, version detection, script scanning, and traceroute
```

```
 -v: Increase verbosity level (use -vv or more for greater effect)
```
