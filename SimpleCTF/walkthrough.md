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

If I try the "For got user password?" button on the right bottom cornor, I can find out if the user name exists or not!
If I throw in random user name, it tells me whether the user name exists or not. 

I was already guessing that the user name will be Mitch so I successfully found out the user name Mitch. 

Now it was time for me to bruteforce the password. 

I used burp intruder and used rockyou.txt to bruteforce the password. 

If you are not familiar with using Burp, I recommend learning to use it since it the most well developed and most used web hacking tool.

From the intruder result, I found out the password is ```secret```

So as a result, I haven't used CVE-2019-9053 and SQL Injection to find out the password, but tried on my own and did bruteforce to find the password. 

## Task 6&7&8
Now that I have the username and password, it is time for me to ssh.
```mitch, secret```

On terminal, I ran the following command.
```ssh mitch@<ip> -p 2222```

Remember to include ```-p 2222``` since the ssh won't work without specfiying the port number. 

Type in the password and log in. 

now type ```bash``` to make the enviroment more readable and friendly.

From the ```ls``` command, you will see the user.txt, now ```cat user.txt``` to find out what it says. 

![user](https://user-images.githubusercontent.com/76433661/125185660-0ba50000-e261-11eb-9315-5f8fddf5cc37.png)

Now head to ```/home``` folder by typing ```cd /home``` and you will find out another user sunbath.

![sub](https://user-images.githubusercontent.com/76433661/125185709-473fca00-e261-11eb-87bb-4621c5960022.png)

You won't be able to cd into sunbath folder because you don'y have enough permissin.

We have to escalted privilege to get inside. 

Now run the follwing command.

```
sudo vim -c ':!/bin/sh'
```
[Link that I used](https://gtfobins.github.io/gtfobins/vim/)

Now we have the full access!

cd to the ```/root``` folder and cat the root.txt to find the final flag and it is done. 

![ssssss](https://user-images.githubusercontent.com/76433661/125185845-0300f980-e262-11eb-9ca7-72b3c999008d.png)

## Lessons learned
I should have used virtual box Kali machine instead of my home Ubuntu Machine. 
It is much more easier to user Kali because it has all the necessay files and I can easily rebuild the virtual machine once it get corrupted. 

I have to study more about privilege escalation and how it works. 

I have to learn about using Tmux.

Study and read opther's walkthroughs about how they exploit SSH and FTP service. 

Just read lots of other CTF writeups. 

