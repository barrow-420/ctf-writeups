# Vulnhub SickOS 

## Enumeration

Kali: 172.16.126.129

SickOS: 172.16.126.135

I used NAT for both Machines. 
nmap

`sudo nmap -vvv -sC -sV 172.16.126.135 -oA sickos`

Port 3128 seems to be running wolfcms and it seemed interesting to me.

## Checking out Port 3128
In order to see port 3128 on web browser, little change on the network setting has to be made. ( I use firefox)
