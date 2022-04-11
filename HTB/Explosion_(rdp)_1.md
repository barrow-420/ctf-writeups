# Explosion
## RDP Vulnerability
[Hackingarticles](https://www.hackingarticles.in/remote-desktop-penetration-testing-port-3389/)
## nmap
`sudo nmap -vvv -sV 10.129.1.13 -oN explosion`

```
PORT     STATE SERVICE       REASON          VERSION
135/tcp  open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp  open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds? syn-ack ttl 127
3389/tcp open  ms-wbt-server syn-ack ttl 127 Microsoft Terminal Services
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

## xfreerdp
I tried bruteforcing with the Login: Explosion but it never worked, so I checked the walkthrough and they were just using `Administrator` as a Login.

`xfreerdp /v:10.129.1.13 /u:Administrator`

### RDP Exploitation
Enumeration -> Bruteforce 

If the Admin has set the Account lockout policy on Windows server, it would be almost impossible to bruteforce. 

