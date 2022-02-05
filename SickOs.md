# Vulnhub SickOS 

**My SetUp**
- VMware Workstation Pro
- Kali: 172.16.126.129
- SickOS: 172.16.126.135
(I used NAT for both Machines)

## Nmap

`sudo nmap -vvv -sC -sV 172.16.126.135 -oA sickos`

* pic

Port 3128 seems to be running wolfcms and it seemed interesting to me.

## Checking out Port 3128

In order to see port 3128 on web browser, little change with the browser network setting has to be made. ( I used firefox)

* pic

go to `172.16.126.135/robots.txt`. It says wolfcms is disallowed.

Now go to `172.16.126.135/wolfcms`.

Before searching for vulnerbilities for wolfcms, I wanted to see if there is more hidden directories, so I ran `dirb`.

Dirb needs to go through proxy so used the command below.

`dirb http://172.16.126.135/wolfcms -p 172.16.126.135:3128`

But nothing special showed up. 

## Vulnerability

[Arbitrary File Upload Vuln](https://www.exploit-db.com/exploits/38000)

From the above exploit-db document, I found out there is an admin page at `172.16.126.135/?/admin`.

* pic

## Exploitation

Now I have to figure out way to go through the login page, in order to gain access to upload features. 

I decided to use Hydra to bruteforce. 
