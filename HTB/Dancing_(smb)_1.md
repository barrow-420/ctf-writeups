# Dancing

## nmap
`nmap -vvv -sV -oA dancing <ip>`

```
# Nmap 7.92 scan initiated Wed Apr  6 04:42:43 2022 as: nmap -vvv -sV -oA dancing 10.129.54.45
Nmap scan report for 10.129.54.45
Host is up, received reset ttl 127 (0.28s latency).
Scanned at 2022-04-06 04:42:43 EDT for 28s
Not shown: 997 closed tcp ports (reset)
PORT    STATE SERVICE       REASON          VERSION
135/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
139/tcp open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
445/tcp open  microsoft-ds? syn-ack ttl 127
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Wed Apr  6 04:43:11 2022 -- 1 IP address (1 host up) scanned in 27.73 seconds
```

Port 135, 139, 445 is open.

## smbclient
`smbclient -L <ip>`
  
List the servers
  
  ```
  Enter WORKGROUP\user's password: 

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        C$              Disk      Default share
        IPC$            IPC       Remote IPC
        WorkShares      Disk      
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to 10.129.54.45 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available
```
Tried connecting to all the servers but every servers except for WorkShares requires credentials which I don't have. 

`smbclient \\\\<ip>\\WorkShares`

```
smb: \> ls
  .                                   D        0  Mon Mar 29 04:22:01 2021
  ..                                  D        0  Mon Mar 29 04:22:01 2021
  Amy.J                               D        0  Mon Mar 29 05:08:24 2021
  James.P                             D        0  Thu Jun  3 04:38:03 2021

                5114111 blocks of size 4096. 1752789 blocks available
```

`cd James.p`
`get flag.txt`

This was the basic CTF using smbclient command. 
