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



#### NFS

Network File System (NFS) allows a user on a client computer to access files on a remote computer, like accessing a local storage. It uses Remote Procedure Calls (RPC) to route requests between client and server.

#### Portmapper

The RPC Portmapper (also called portmap or rpcbind) is a service which makes sure that the client ends up at the right port, which means that it maps the client RPC requests to the correct services. It keeps track of what services are running on which ports. E.g. a client contacts portmap on the server machine to determine the port number where the RPC requests should be send to. The Portmapper listens on a static port 111, on which an inital connection is made.

the rpcinfo -p <Target IP> can be helfpul for determining if the portmapper services are available from outside. 

```nmap -sV -script=nfs* <IP Remote Server>```    
    
[source](https://medium.com/@sebnemK/how-to-bypass-filtered-portmapper-port-111-27cee52416bc)

## Task 3

```netcat 10.10.69.224 21```
Version is 1.3.5

