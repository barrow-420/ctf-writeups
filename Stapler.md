# Stapler
My SetUp
- Kali : 192.168.35.150 (VMware Workstation Pro, Bridged Network)
- Stapler : 192.168.35.52 (VirtualBox, Brdiged Network)
*Somehow Stapler won't open on VMware, so I used Bridged Network to connect VMware and VirtualBox.

## Netdiscover
`sudo netdiscover -r 192.168.35.0/24`

Result:
```
7 Captured ARP Req/Rep packets, from 4 hosts.   Total size: 420                                               
 _____________________________________________________________________________
   IP            At MAC Address     Count     Len  MAC Vendor / Hostname      
 -----------------------------------------------------------------------------
 192.168.35.1    88:3c:1c:ca:7f:d9      3     180  ---------------                                         
 192.168.35.23   4c:eb:bd:9c:05:80      1      60  ---------------                        
 192.168.35.52   08:00:27:fe:7d:e0      2     120  PCS Systemtechnik GmbH                                      
 192.168.35.94   d0:ab:d5:64:09:79      1      60  ---------------
 ```
 
Target IP: **192.168.35.52**

## Nmap
`sudo nmap -vvv -sV -sT -O -A -oA stapler 192.168.35.52`

Result:
```
Scanning 192.168.35.52 [1000 ports]
Discovered open port 21/tcp on 192.168.35.52
Discovered open port 80/tcp on 192.168.35.52
Discovered open port 53/tcp on 192.168.35.52
Discovered open port 3306/tcp on 192.168.35.52
Discovered open port 139/tcp on 192.168.35.52
Discovered open port 22/tcp on 192.168.35.52
Discovered open port 666/tcp on 192.168.35.52
Completed Connect Scan at 00:38, 4.72s elapsed (1000 total ports)
Initiating Service scan at 00:38
Scanning 7 services on 192.168.35.52
Completed Service scan at 00:39, 11.04s elapsed (7 services on 1 host)
Initiating OS detection (try #1) against 192.168.35.52
NSE: Script scanning 192.168.35.52.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 00:39
NSE: [ftp-bounce 192.168.35.52:21] PORT response: 500 Illegal PORT command.
Completed NSE at 00:39, 30.07s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 00:39
Completed NSE at 00:39, 0.06s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 00:39
Completed NSE at 00:39, 0.00s elapsed
Nmap scan report for 192.168.35.52
Host is up, received arp-response (0.0011s latency).
Scanned at 2022-02-08 00:38:46 EST for 48s
Not shown: 992 filtered tcp ports (no-response)
PORT     STATE  SERVICE     REASON       VERSION
20/tcp   closed ftp-data    conn-refused
21/tcp   open   ftp         syn-ack      vsftpd 2.0.8 or later
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: PASV failed: 550 Permission denied.
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 192.168.35.150
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 4
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp   open   ssh         syn-ack      OpenSSH 7.2p2 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 81:21:ce:a1:1a:05:b1:69:4f:4d:ed:80:28:e8:99:05 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDc/xrBbi5hixT2B19dQilbbrCaRllRyNhtJcOzE8x0BM1ow9I80RcU7DtajyqiXXEwHRavQdO+/cHZMyOiMFZG59OCuIouLRNoVO58C91gzDgDZ1fKH6BDg+FaSz+iYZbHg2lzaMPbRje6oqNamPR4QGISNUpxZeAsQTLIiPcRlb5agwurovTd3p0SXe0GknFhZwHHvAZWa2J6lHE2b9K5IsSsDzX2WHQ4vPb+1DzDHV0RTRVUGviFvUX1X5tVFvVZy0TTFc0minD75CYClxLrgc+wFLPcAmE2C030ER/Z+9umbhuhCnLkLN87hlzDSRDPwUjWr+sNA3+7vc/xuZul
|   256 5b:a5:bb:67:91:1a:51:c2:d3:21:da:c0:ca:f0:db:9e (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBNQB5n5kAZPIyHb9lVx1aU0fyOXMPUblpmB8DRjnP8tVIafLIWh54wmTFVd3nCMr1n5IRWiFeX1weTBDSjjz0IY=
|   256 6d:01:b7:73:ac:b0:93:6f:fa:b9:89:e6:ae:3c:ab:d3 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIJ9wvrF4tkFMApswOmWKpTymFjkaiIoie4QD0RWOYnny
53/tcp   open   domain      syn-ack      dnsmasq 2.75
| dns-nsid: 
|_  bind.version: dnsmasq-2.75
80/tcp   open   http        syn-ack      PHP cli server 5.5 or later
|_http-title: 404 Not Found
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
139/tcp  open   netbios-ssn syn-ack      Samba smbd 4.3.9-Ubuntu (workgroup: WORKGROUP)
666/tcp  open   tcpwrapped  syn-ack
3306/tcp open   mysql       syn-ack      MySQL 5.7.12-0ubuntu1
| mysql-info: 
|   Protocol: 10
|   Version: 5.7.12-0ubuntu1
|   Thread ID: 9
|   Capabilities flags: 63487
|   Some Capabilities: InteractiveClient, ODBCClient, LongPassword, Speaks41ProtocolOld, Support41Auth, SupportsLoadDataLocal, ConnectWithDatabase, LongColumnFlag, IgnoreSigpipes, Speaks41ProtocolNew, SupportsCompression, IgnoreSpaceBeforeParenthesis, SupportsTransactions, FoundRows, DontAllowDatabaseTableColumn, SupportsMultipleStatments, SupportsAuthPlugins, SupportsMultipleResults
|   Status: Autocommit
|   Salt: Cc?l\x13\x1B\x1A9\x18}`       \x05aX\x11:%    y
|_  Auth Plugin Name: mysql_native_password
MAC Address: 08:00:27:FE:7D:E0 (Oracle VirtualBox virtual NIC)
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.9
TCP/IP fingerprint:
OS:SCAN(V=7.92%E=4%D=2/8%OT=21%CT=20%CU=32673%PV=Y%DS=1%DC=D%G=Y%M=080027%T
OS:M=62020216%P=x86_64-pc-linux-gnu)SEQ(SP=F7%GCD=1%ISR=FE%TI=Z%CI=I%TS=8)O
OS:PS(O1=M5B4ST11NW7%O2=M5B4ST11NW7%O3=M5B4NNT11NW7%O4=M5B4ST11NW7%O5=M5B4S
OS:T11NW7%O6=M5B4ST11)WIN(W1=7120%W2=7120%W3=7120%W4=7120%W5=7120%W6=7120)E
OS:CN(R=Y%DF=Y%T=40%W=7210%O=M5B4NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F
OS:=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5
OS:(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z
OS:%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=
OS:N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=N)

Uptime guess: 0.006 days (since Tue Feb  8 00:31:02 2022)
Network Distance: 1 hop
TCP Sequence Prediction: Difficulty=247 (Good luck!)
IP ID Sequence Generation: All zeros
Service Info: Host: RED; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 8h59m58s, deviation: 0s, median: 8h59m58s
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 42508/tcp): CLEAN (Timeout)
|   Check 2 (port 64290/tcp): CLEAN (Timeout)
|   Check 3 (port 48366/udp): CLEAN (Failed to receive data)
|   Check 4 (port 47903/udp): CLEAN (Failed to receive data)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
| nbstat: NetBIOS name: RED, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| Names:
|   RED<00>              Flags: <unique><active>
|   RED<03>              Flags: <unique><active>
|   RED<20>              Flags: <unique><active>
|   \x01\x02__MSBROWSE__\x02<01>  Flags: <group><active>
|   WORKGROUP<00>        Flags: <group><active>
|   WORKGROUP<1d>        Flags: <unique><active>
|   WORKGROUP<1e>        Flags: <group><active>
| Statistics:
|   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
|   00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
|_  00 00 00 00 00 00 00 00 00 00 00 00 00 00
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-time: 
|   date: 2022-02-08T14:39:03
|_  start_date: N/A
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.9-Ubuntu)
|   Computer name: red
|   NetBIOS computer name: RED\x00
|   Domain name: \x00
|   FQDN: red
|_  System time: 2022-02-08T14:39:03+00:00

TRACEROUTE
HOP RTT     ADDRESS
1   1.10 ms 192.168.35.52
```
