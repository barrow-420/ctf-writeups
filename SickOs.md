# Vulnhub SickOS 

**My SetUp**
- VMware Workstation Pro
- Kali: 172.16.126.129
- SickOS: 172.16.126.135

(I used NAT for both Machines)

## Nmap

`sudo nmap -vvv -sC -sV 172.16.126.135 -oA sickos`

![nmap](https://user-images.githubusercontent.com/76433661/152642864-d4d8492b-a383-4ce3-a47b-8953aae8d859.png)


Port 22, 3128, and 8080 seemed to be opened.

SSH is usually not worth it unless SSH version is severely outdated, so I decided to move one to port 3128 right away. 

## Checking out Port 3128

In order to see port 3128 on web browser, little change with the browser network setting has to be made. ( I used firefox)

![firefox_proxy_setup](https://user-images.githubusercontent.com/76433661/152642919-401787be-ea0f-4d78-be0c-928dcfb6fc74.png)

Browser has to go through proxy (port 3128) in order to access the content. 

![blehh](https://user-images.githubusercontent.com/76433661/152642953-584290dc-cdef-4845-8b82-8d76bba55bb8.png)

I could only see the ugly `blehhh` on the page so I tried looking for more directories. 

I always check out `robots.txt` first and it seemed like there is a page running `wolfcms`.

Now I moved to `172.16.126.135/wolfcms`.

![wolfcms](https://user-images.githubusercontent.com/76433661/152643029-11dd67b4-b782-499b-8248-8f34bc591b15.png)

Before searching for vulnerbilities for wolfcms, I wanted to see if there are more hidden directories, so I ran `dirb`.

Dirb needs to go through proxy so used the command below.

`dirb http://172.16.126.135/wolfcms -p 172.16.126.135:3128`

But nothing special showed up. 

After doing some researches, I decided to use exploit from [Arbitrary File Upload Vuln](https://www.exploit-db.com/exploits/38000).

I found out there is an admin page at `172.16.126.135/?/admin`.

![login](https://user-images.githubusercontent.com/76433661/152643116-c9dcd892-8369-4da1-b034-dc7e685c2816.png)

Even before trying bruteforcing, I tired `admin;admin` and it worked right away.

![main](https://user-images.githubusercontent.com/76433661/152643172-f65d45f7-c63a-46cf-bcfc-4012c788c053.png)

Now that I am inside the system, only thing I need to do is to upload arbitrary PHP file, and capture the reverse shell with the nc command. 

I used [pentestmonkey php revershell](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php) to upload my code on the system.

And my Kali machine was waiting to capture the signal with the command `nc -lvp 1234`
