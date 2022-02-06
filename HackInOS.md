# HackInOS
My SetUp
- HackinOS (192.168.35.226) VirtualBox Bridged Network
- Kali (192.168.35.58) VMware Workstation Brdiged Network

*I don't know why, but .ova file won't open in VMware, so I opened HackInOS with VirtualBox.*

## Nmap

`nmap -vvv -sV -sT -O -A -p- -oA hackinos 192.168.35.226`

Result:
```
PORT     STATE SERVICE REASON         VERSION
22/tcp   open  ssh     syn-ack ttl 64 OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 d9:c1:5c:20:9a:77:54:f8:a3:41:18:92:1b:1e:e5:35 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDG784LvNaNbACbq+WDUkIlEEMYCDyMkV+nCvnQG/acqhU2pj/DdyduoK3AE3RyPCjnp2Tj5TIYZOjRNXqdiAgix45+f/8uQSAXzMkehTgpRgAkRfcz9tY80G6Jc/0fglUjPuh+pa8W/2Zom9FoNkQlFlQNTAG5KXj7aNrdBTyznsxHBvxpdXOS+e1k4l4l8ecIhdV9fInbWgzx6HfzRl7P8ghYWW+7MN9rmyFkno8TwL0dH14BCtz+qM9trQ3OclpEAFHzZRcKKCT5lgyZRoWOi5hwP4ciR5omPlSIFri9spD7/VYlnHtOTq5VErkDXD7GLb85r12WPLFswPObxABl
|   256 df:d4:f2:61:89:61:ac:e0:ee:3b:5d:07:0d:3f:0c:87 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBCflFRiixnKHKZ6H/VbctPSyorJLf9d1+TGw4mZdB6tfB4KnuiXuZyc5PWXkYDtkgn5BhZCjgjW5EIFizhPMBsE=
|   256 8b:e4:45:ab:af:c8:0e:7e:2a:e4:47:e7:52:f9:bc:71 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIN7nLDN7p/roJG7o7AEKF3C5IgV3HhMGJmBt9gC+wxci
8000/tcp open  http    syn-ack ttl 63 Apache httpd 2.4.25 ((Debian))
| http-robots.txt: 2 disallowed entries 
|_/upload.php /uploads
|_http-generator: WordPress 5.0.3
|_http-title: Blog &#8211; Just another WordPress site
|_http-open-proxy: Proxy might be redirecting requests
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.25 (Debian)
MAC Address: 08:00:27:20:A9:BC (Oracle VirtualBox virtual NIC)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

SSH is usually hard to exploit unless the version is really oudated, so I moved on to Port 8000.

I went to firefox to open `192.168.35.226:8000`.

![index](https://user-images.githubusercontent.com/76433661/152665945-f6f83e59-6915-4cca-a46b-1c6e48834b60.png)

Page seemed to be broken, so I tried editing the /etc/hosts file to add <ip> as localhost. However, it was not working. 
  
I moved on to `dirb`.
  
`dirb http://192.168.35.226:8000/ /usr/share/wordlists/dirb/big.txt`
  
Result:
```
  -----------------
DIRB v2.22    
By The Dark Raver
-----------------

START_TIME: Sat Feb  5 21:39:27 2022
URL_BASE: http://192.168.35.226:8000/
WORDLIST_FILES: /usr/share/wordlists/dirb/big.txt

-----------------

GENERATED WORDS: 20458                                                         

---- Scanning URL: http://192.168.35.226:8000/ ----
+ http://192.168.35.226:8000/robots.txt (CODE:200|SIZE:52)                                     
+ http://192.168.35.226:8000/server-status (CODE:403|SIZE:304)                                 
==> DIRECTORY: http://192.168.35.226:8000/uploads/                                             
==> DIRECTORY: http://192.168.35.226:8000/wp-admin/                                            
==> DIRECTORY: http://192.168.35.226:8000/wp-content/                                          
==> DIRECTORY: http://192.168.35.226:8000/wp-includes/                                         
                                                                                               
---- Entering directory: http://192.168.35.226:8000/uploads/ ----
                                                                                               
---- Entering directory: http://192.168.35.226:8000/wp-admin/ ----
==> DIRECTORY: http://192.168.35.226:8000/wp-admin/css/                                        
==> DIRECTORY: http://192.168.35.226:8000/wp-admin/images/                                     
==> DIRECTORY: http://192.168.35.226:8000/wp-admin/includes/                                   
==> DIRECTORY: http://192.168.35.226:8000/wp-admin/js/                                         
==> DIRECTORY: http://192.168.35.226:8000/wp-admin/maint/                                      
==> DIRECTORY: http://192.168.35.226:8000/wp-admin/network/                                    
==> DIRECTORY: http://192.168.35.226:8000/wp-admin/user/
  ```
  There are some interesting pages.
  - robots.txt
  - uploads
  - upload.php
  - wp-admin

I though of trying bruteforce against the `wp-login` page, but in order to do that, I first need to fix the website's funky look.

After researching for a while, I found out I need to set up a `invisible proxy`.[reference](https://trelis24.github.io/2017/11/27/Invisible-Proxy/)

