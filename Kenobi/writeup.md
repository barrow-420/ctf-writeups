# Kenobi
## Little Behind Story
I was doing tryhackme basic pentesting.

I got up to 50% on the progress. But got stuck at SMB.

I was able to find out the user name. But got stuck with finding out password using brute force. 

I decided I need more understanding on SMB system, and how it works. 

## Task 1
Scan for open ports

```sudo nmap -vvv -sS -sV <ip> -oN sssv_scan```

## Task 2
Read the instruction carefully.

command for enumerating shares.

```nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse <ip>```

Now connect to the smb server.

```smbclient //<ip>/anonymous```

Recursively download the file.

```smbget -R smb://<ip>/anonymous```

