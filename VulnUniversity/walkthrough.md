# VulnUniversity

I was checking on easy looking CTF? Challenges? on Tryhackme and decided to go with Vulnuniversity.

According to the description, ```Learn about active recon, web app attacks and privilege escalation.```
I can learn about recon, web attack, and privilege escalation. 

## Task 1
Deploy the machine and connect to openvpn.

## Task 2
Do the nmap scan. 
```nmap -vv -sS -Pn -oN pn_scan <ip>```

![vuln scan](https://user-images.githubusercontent.com/76433661/125239745-12487b80-e324-11eb-870e-20ce58ed2b12.png)

6 ports are open. Web server running on port 3333.

Nothing special or hard.

## Task 3
Run the gobuster command for searching hidden directories.

```gobuster -u http://<ip>:3333 -w ../wordlist/discovery_webcontent_commom.txt```

I have downloaded web directory wordlist online and stored in so I can often use it.

![aainternal](https://user-images.githubusercontent.com/76433661/125240175-b7fbea80-e324-11eb-9d0e-12cb1a20f712.png)

 You can check out that internal page has upload form.
 
 ## Task 4
 To solve task 4, you need knowledge with using Burpsuite.
 
 Luckily, from my past bug bounty experience, I had experience using burp, and carried on with no problem.
 
 First, go to file upload internal and page and intercept the moment you upload any file. 
 
 Send the intercepted moment to burp intruder and try out different extensions as a payload.
 
 From what I have found out, most of the extensions are blocked, but php is always the most interesting file upload extension.
 
 Now, using the same method, we can know that only ```.phtml``` is allowed to be uploaded. 
 
 Next, follow the guideline from the tryhackeme page to finish the task. 
 
 ## Task 5
 For, me Task 5 was the hardest one. I had to look up writeups by others to solve the task.
 
 Honestly, I still do not undestand the SUID privilege escalation code clearly, so I will be studying as I write the writeup.
 
 To find the SUID file, I used the following command.
 
 ```find / -perm -u=s -type f 2>/dev/null```
 
 The command that was on tryhackme was not very clear for me, so I used another one that I have found online.
 
 tryhackme command: ```find / -user root -perm -4000 -exec ls -ldb {} \;```
 
 
