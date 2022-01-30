# Vulnhub Simple

## Enumeration
`nmap -sC -sV -Pn <ip>`

Sc : default scripts

sV : Default Versions

Pn : Skip Host discovery

Result: 

```
80/tcp open  http    syn-ack Apache httpd 2.4.7 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.7 (Ubuntu)
|_http-favicon: Unknown favicon MD5: 759585A56089DB516D1FBBBE5A8EEA57
|_http-title: Please Login / CuteNews
```

## CuteNews

It seems like there is an Apache server running. 

There was a login form and it was running on Cutenews 2.0.3
  
I ran dirb just in case, but nothing special was found. 
  
So, I searched for known vulnerabilities with cutenews 2.0.3
  
`searchsploit cutenews`
  
Result:
  
`CuteNews 2.0.3 - Arbitrary File Upload                            | php/webapps/37474.txt`

[exploit database](https://www.exploit-db.com/exploits/37474)

  
I found out cutenews 2.0.3 has a file upload vulnerability that can lead to reverse shell.

First, attacker upload malicious file through file upload function. Then, execute the malicious file with the listener pre-running. Lastly, attacker has a shell opened. 
  
This known exploit was pretty old, and "tamper data" add on from firefox was not working well for me. 
  
I decided to work with Burpsuite instead.
  
## Creating PHP backdoor
  
I got help from [hackingarticles](https://www.hackingarticles.in/web-penetration-testing-tamper-data-firefox-add/) when writing the code. 

Basically, it is about creating php shell code using msfvenom and multi handler. I should study more about this area. 
  
After creating the file `payload.php.jpg` ,turn burpsuite on.
  
From the avatar change page, select the `payload.php.jpg` file and click submit button with the burp intercept on.
  
Burp will intercept and now change the `payload.php.jpg` into `payload.php`.
  

  
  ## sd
  Open the ph file from the <ip>uploads. 
  
  Have the msfconsole pre-ready for connection. 
  
  ``use ecploit/multi/handler
  set payload php/meterpreter/reverse_tcp
  set ...
  run
  ``
