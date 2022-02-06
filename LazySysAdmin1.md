# LazySysAdmin1 Vulnhub
 My SetUp
 - Kali: 172.16.126.129
 - LazySysAdmin: 172.16.126.136
 - I used VMware Workstation Pro NAT for both machines.

## Nmap
`nmap -vvv -sV -sT -O -A -oA lazysysadmin 172.16.126.136'

Result:
```
PORT     STATE SERVICE     REASON  VERSION
22/tcp   open  ssh         syn-ack OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 b5:38:66:0f:a1:ee:cd:41:69:3b:82:cf:ad:a1:f7:13 (DSA)
| ssh-dss AAAAB3NzaC1kc3MAAACBAKXQVTTRKsDhYwPWdmZ2BDTjKcCtJ7SnW0BHwbBvIdUVOh7zjZ6xjkEJ4TkT/Y+lJUolKMMNDu+CNPrRNKyBfjQ5w13mO7/3mKh9p52bzHG6XFS2m7GI4cLiDbmjO9L/YhU5deFP1Bo02KxzREp/ipz/CVlRr8IZm/x7SbPXtzv1AAAAFQDorLYH3AOwt18+kzAxGO0f2SarWQAAAIEAmOm6aWDLi+a85rfIm2Llb24aPZN3OsntJKVk4iCDbKxXi7xd6K9h1t+Utrg7dn4oO/QrVv8RRYBSiuJ8sy7B2+YDM0X7v+yqIG8FdA66tFpnMiMvdhYXoLyiod71vTqmGuAVKyHc56fUtdb3gCMjO0CHhPTKg2S0gPfFOqiyGVUAAACACvwr3X/J810mevpUQokt4xBBPNiIGkbK9KbZG63vi1NvGmaOkzbo3Cf8gZ0ILFd3YlryhP6c8PHaQMWcvzMT9oTyJ4FOokv1D3Mh4APPZ1SDqCmryHmRazggnbYlbGkYiqmZHUvS1zNalJHfC/QIHQZAjeUrHl8ZVHKk5ZYktAE=
|   2048 58:5a:63:69:d0:da:dd:51:cc:c1:6e:00:fd:7e:61:d0 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDL4kUdp6Gej0kmVuGrpPSUUIqYmMsiqjbZ4PFCmji+ozLhgBlWE4+XcghV9PWTUmBdU6yZsylputJMi87GBW8s66tCnZU2lm+APerAT+euYlUgi+xoigD+g2VWthVNwvj2mg8updYtcZ3Jv2besdsohtadike0fwJAPfvl/ss9jE9AFv73DHu2EuwrP/3tM0WG7GgQQj01TFmrLYnDX9unvKcOi3kLgQ9I6JfdSC1oc+lBtkOp12hr5gIlYIlAgI+E2yl79cdk6PTQ4mgRmIEJguLbWo8mnaEI77y1Lz7xpxi89/gWjQuS+DMPbbpoJZdRkTldTr0QaJuP2i0ys8Dh
|   256 61:30:f3:55:1a:0d:de:c8:6a:59:5b:c9:9c:b4:92:04 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBBcmYC//tB7vdI00Q3Czjvzi7cao1q+PtbUHYxSk7ay3rM1LStjxRkpUZPQWpVRdU9kWJhIiYZDMPf8gOSgC2eY=
|   256 1f:65:c0:dd:15:e6:e4:21:f2:c1:9b:a3:b6:55:a0:45 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIKQXcDdFdhnLjXj6zgOcox1r7UBkTYpaOYdioJt97xdA
80/tcp   open  http        syn-ack Apache httpd 2.4.7 ((Ubuntu))
|_http-server-header: Apache/2.4.7 (Ubuntu)
| http-robots.txt: 4 disallowed entries 
|_/old/ /test/ /TR2/ /Backnode_files/
|_http-generator: Silex v2.2.7
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Backnode
139/tcp  open  netbios-ssn syn-ack Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn syn-ack Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
3306/tcp open  mysql       syn-ack MySQL (unauthorized)
6667/tcp open  irc         syn-ack InspIRCd
| irc-info: 
|   server: Admin.local
|   users: 1
|   servers: 1
|   chans: 0
|   lusers: 1
|   lservers: 0
|   source ident: nmap
|   source host: 172.16.126.129
|_  error: Closing link: (nmap@172.16.126.129) [Client exited]
MAC Address: 00:0C:29:FE:84:6C (VMware)
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.9
```
Port 22, 80, 139, 445, 3306, and 6667 are open. 

Nothing seems interesting from port 22 since it is running SSH and service is not very outdated. 
I might retrieve lowerlevel-user account and try sshing using the information later. 

At first glance, port 80 running http seems most interesting. Robots.txt shows that it has few disallwed enteries. 

`/old/ /test/ /TR2/ /Backnode_files/`

Also, it shows that Silex v2.2.7 is used as http-generator.

Searchsploit is not showing any options with silex so I moved on to googling about it and Google provided me bunch of infos. It seems liked silex v2.2.7 has a well known vuln that works together with Samba. 
