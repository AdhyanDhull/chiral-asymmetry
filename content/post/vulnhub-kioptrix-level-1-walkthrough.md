---
title: 'Vulnhub: Kioptrix Level 1 - Walkthrough'
date: '2019-06-06T20:39:15+05:30'
draft: true
categories:
  - walkthrough
autoThumbnailImage: false
---


Today I tried another vulnerable machine which can be found at https://www.vulnhub.com/entry/kioptrix-level-1-1,22/ and is often the beginner’s first choice for an OSCP lab type environment.

This is how the vulnerable machine looks like in VMware

![]()

Now I started with discovering the target IP on the discoverable network, but I couldn’t find anything other than the default gateway and broadcast IP addresses.

After changing the network settings from the VMware from Bridged to NAT, I tried rebooting and still couldn’t discover the machine, I checked again and figured out the machine was configured to start in Bridged mode only.

After doing some research I found a simple available solution, I just had to edit the .vmx file and change a few defaults.

![]()

![]()

The highlighted parts are changed from “Bridged” to “NAT” or “bridged” to “nat”

Now upon running the arp-scan command again, I could successfully discover the target IP address and this solved the issue.

arp-scan –l 	or 	netdiscover –i eth0

![]()

Now that we know the IP address of the target machine is 192.168.192.132, we can do enumeration on the target.

We start with Network-Mapper to do the port scanning and scavenge all the services running on all/most important ports.

nmap –A –Pn <target IP address>

![]()

Below is the complete output highlighting the ports and services running on them:

```
Starting Nmap 7.60 ( https://nmap.org ) at 2019-06-05 23:19 EDT Nmap scan report for 192.168.192.132 Host is up (0.00026s latency).Not shown: 994 closed portsPORT     STATE SERVICE     VERSION22/tcp   open  ssh         OpenSSH 2.9p2 (protocol 1.99)| ssh-hostkey: |   1024 b8:74:6c:db:fd:8b:e6:66:e9:2a:2b:df:5e:6f:64:86 (RSA1)|   1024 8f:8e:5b:81:ed:21:ab:c1:80:e1:57:a3:3c:85:c4:71 (DSA)|_  1024 ed:4e:a9:4a:06:14:ff:15:14:ce:da:3a:80:db:e2:81 (RSA)|_sshv1: Server supports SSHv180/tcp   open  http        Apache httpd 1.3.20 ((Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b)| http-methods: |_  Potentially risky methods: TRACE|_http-server-header: Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b|_http-title: Test Page for the Apache Web Server on Red Hat Linux111/tcp  open  rpcbind     2 (RPC #100000)| rpcinfo: |   program version   port/proto  service|   100000  2            111/tcp  rpcbind|   100000  2            111/udp  rpcbind|   100024  1           1024/tcp  status|_  100024  1           1024/udp  status139/tcp  open  netbios-ssn Samba smbd (workgroup: MYGROUP)443/tcp  open  ssl/https   Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b|_http-server-header: Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b|_http-title: 400 Bad Request|_ssl-date: 2019-06-05T18:43:31+00:00; -8h36m43s from scanner time.| sslv2: |   SSLv2 supported|   ciphers: |     SSL2_RC4_64_WITH_MD5|     SSL2_RC4_128_WITH_MD5|     SSL2_RC4_128_EXPORT40_WITH_MD5|     SSL2_RC2_128_CBC_EXPORT40_WITH_MD5|     SSL2_RC2_128_CBC_WITH_MD5|     SSL2_DES_192_EDE3_CBC_WITH_MD5|_    SSL2_DES_64_CBC_WITH_MD51024/tcp open  status      1 (RPC #100024)MAC Address: 00:0C:29:6E:E6:DE (VMware)Device type: general purposeRunning: Linux 2.4.XOS CPE: cpe:/o:linux:linux_kernel:2.4OS details: Linux 2.4.9 - 2.4.18 (likely embedded)Network Distance: 1 hopHost script results:|_clock-skew: mean: -8h36m43s, deviation: 0s, median: -8h36m43s|_nbstat: NetBIOS name: KIOPTRIX, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)|_smb2-time: Protocol negotiation failed (SMB2)TRACEROUTEHOP RTT     ADDRESS1   0.26 ms 192.168.192.132OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .Nmap done: 1 IP address (1 host up) scanned in 278.29 seconds
```

Now that the port scanning is done, we will try to see if we can find vulnerabilities in the services running on these ports using https://exploit-db.com or searchscploit tool or metasploit framework in KALI.

As I saw HTTP and HTTPS is working on their default ports only, I tried accessing the probable webpages on the server hosting but there was nothing except the page below and a link which seemed intriguing

Clicking on the DocumentRoot hyperlink, I am forwarded to a 404 page, but it gives me away two of the directory names, upon further inspection I find nothing of use there.

Now that I’ve checked port 80 and 443, I checked and found that SSH login wasn’t working. The only two interesting services I could try to find exploits for were, rpcbind on port 111 and Samba on port 139.

Now after some research I found out that open rpcbind port can be used for Denial of Service attacks only, so I then came to Samba. Using a script in Metasploit framework, to determine the Samba version being used on the target machine I wrote the following commands:

msfconsole

use auxiliary/scanner/smb/smb_version 

show options

set RHOSTS <target IP>

exploit

Now from this I concluded that the version of Samba that is being used here is 2.2.1a, and searched for an exploit on https://exploit-db.com and the search parameter being “samba 2.2.x” 

Using this I tried a few exploits present here and I got my first success from the highlighted exploit, so I’ll just show how to use it here.

First of all I’ll download the exploit from the exploit, this can be done manually or using terminal

wget <file url> 

Now the file I downloaded was named “22469.c”

We now have to compile the exploit to be executable using

gcc –o <output filename> <exploit code filename>

To execute it, we simply use 

./<executable name>

Now this exploit needs some parameters to function and attack the correct target,

./samba-exploit –t <target address>

This directly gave us root access, and boom we’re in. I also rechecked, using the linux commands whoami and id.
