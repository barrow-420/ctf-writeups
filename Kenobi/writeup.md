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

From the log.txt we downloaded, we can see that...

    Information generated for Kenobi when generating an SSH key for the user
    Information about the ProFTPD server.
    
Your earlier nmap port scan will have shown port 111 running the service rpcbind. 

This is just a server that converts remote procedure call (RPC) program number into universal addresses. 

When an RPC service is started, it tells rpcbind the address at which it is listening and the RPC program number its prepared to serve. 

So from what I have understood, rpcbind asks RPC for the available port number.

RPC gives the available port number to the rpcbind, and using that port, service is connected.

This thing, goes along with NFS. 

```nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount 10.10.69.224```

## Task 3

```netcat 10.10.69.224 21```
Version is 1.3.5

