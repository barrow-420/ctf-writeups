# SimpleCTF
It was my first time playing CTF on tryhackme and I am a very beginner at this, so I decided to go with the easiest looking one.

SimpleCTF is a beginner level CTF but it was still very hard for me. 

To be honest, I had a peek at the walkthrough few times once I got stuck.

My walkthrough is little bit different from what others have done because I had a python version and module issue, so I had to change my point of view.


## Task 1&2
I first had to do nmap scan. 
```
nmap -vvv -sS -sV -oN initial 10.10.51.175
```
![nmap1](https://user-images.githubusercontent.com/76433661/125184976-e1514380-e25c-11eb-86db-4dafc3f7f3e6.png)

There is ssh and ftp running so answer there is 2 service running under port 1000.

```-vvv``` is for verbose mode, 
```-sS``` is for SYN scan which is default, 
```-sV``` is for version detection mode. 

and we can see the ssh is running on port 2222. (higher port)

## Task 3&4
I first thought there must be some vulnerability with ftp and ssh so I tried everything related to that. 

Logging in to ftp with anonymous login, I was able to see a file named "ForMitch.txt"

![formitch](https://user-images.githubusercontent.com/76433661/125185097-9a178280-e25d-11eb-868c-0e8406ac1ba9.png)

I sensed that password is weak and I would be able to crack it easily. 

For SSH, I had no achievement since I had no idea what the password is. 

I just assumed that I need to find out user ID and password for the ssh and I can escalated privilege from there. 


I typed the url and http port number to firefox to load up webpage
```<ip>:80```
and I found there was nothing special but an simple apache2 default page. 

Of course, I decided to do directory finding and went on to dirbuster. 

I found out there is a directory named simple,
and webpage load up showing CMS Made Simple Page, version running 2.2.8.
![ss](https://user-images.githubusercontent.com/76433661/125185296-152d6880-e25f-11eb-8a8c-eebfb3b5786b.png)

so I typed on google...
```CMS Made Simple 2.2.8 exploit```
Found out CVE-2019-9053 had a downloadable exploit. 

However, this .py file required me to run it using python2 but I was using python3 on my ubuntu machine. 

I followed all the instructions online to get my machine to use python2 and install required modules to run the script, but it wasn't working somehow and I gave up. 

I had to find out another way to solve this thing. 

So this is where my walkthrough becomes slightly different from what others have done. 

Instead of using the exploit, I decided to bruteforce the password since ForMitch.txt mentioned password is very weak.

From the gobuster result, I found a directory ```/simple/admin``` with a login page.
![login](https://user-images.githubusercontent.com/76433661/125185436-c2a07c00-e25f-11eb-93c9-5184e66a38c7.png)





## Lessons learned
I should have used virtual box Kali machine instead of my home Ubuntu Machine. 
It is much more easier to user Kali because it has all the necessay files and I can easily rebuild the virtual machine once it get corrupted. 
