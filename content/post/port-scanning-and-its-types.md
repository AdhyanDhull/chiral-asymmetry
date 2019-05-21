---
title: Port Scanning and its types
date: '2019-05-21T22:11:32+05:30'
draft: true
categories:
  - networking
autoThumbnailImage: false
---
1.	TCP Connect Scan:

•	In TCP Connect Scan , nmap completes a 3 way handshake and it creates the connection log file, which is not suitable for hackers, so it isn’t often used by them.



~# nmap –sT –Pn 192.168.202.129 (the host address)

Nmap is network mapper, -sT denotes scan TCP, and –Pn denotes ping

 

~# nmap –sT –Pn -p- 192.168.202.129 (this is to check all 65535 ports)

 

 And then check on WireShark for packet transfers.

The display filter is ip.addr == 192.168.202.129 && tcp.port == 21

This is for port 21 which is open, hence the source sends SYN request to the port of destination, the destination then returns a SYN-ACK which means the port is open. 

If the destination returns RST-ACK then the port is closed, eg: 443 (HTTPS) here.



2.	Half Open Scan (Stealth Scan):

•	This doesn’t leave log files as ACK isn’t sent from the Source to the Destination and only sends RST and hence connection isn’t established and is good for hackers.



~# nmap –sS –Pn 192.168.202.129

 

Wireshark

For port 21 we see that after destination sends SYN-ACK, the Source doesn’t send ACK and instead sends RST hence no connection is established.

For port 443 there is no change as connection isn’t established anyway.





3.	Xmas Tree Scan (not very effective):

It cannot figure out if the port is open or filtered as server doesn’t send SYN-ACK

A filtered port usually has a firewall installed.

It uses FIN(Finish), PSH(Push) and URG(Urgent) flags.

FIN: Finished, means there is no more data from the sender. Therefore, it is used in the last packet sent from the sender.

PSH: Push, similar to URG, and tells the receiver to process the packets as they are received instead of buffering them.

URG: Urgent, it is used to notify the receiver to process the urgent packets before processing all other packets. The receiver will be notified when all known urgent data has been received.



~#nmap –sX –Pn 192.168.202.129 

 

Wireshark

For port 21, the source sends flags not expected by the destination hence it doesn’t send a SYN-ACK message back, so it cannot be figured out if it is open or filtered.















For port 443, which is closed, the destination sends back RST-ACK, hence closed ports are confirmed but the open ports aren’t confirmed in this method of scanning.



4.	Version Detection (very effective):

It gives versions of technologies of protocols being used which makes a huge advantage as exploits for the technologies can be found. It is very effective.

~#nmap –sV –Pn 1992.168.202.129

These versions can be used to find exploits, for eg: OpenSSH 



WireShark

Just like TCP Contact Scan, this does that too and connects additional information too.

5.	Aggressive Scan:

It is very effective and includes various information, OS, Scripts, and Traceroutes.

~#nmap –A –Pn 192.168.202.129

 

If it reads anon-ftp, it means anyone can access the ftp, but to install ftp first, 

apt-get update, apt-get install ftp and then ftp 192.168.202.129 to get into it.

 

WireShark

6.	UDP SCAN:

~#nmap –sU –Pn 192.168.202.129

 

WireShark

Display filter: ip.addr == 192.168.202.129 && udp.port == 21
