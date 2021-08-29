# Archetype
## hackthebox 

## Task 1: Scanning with Nmap
`nmap -vvv -sS -sV -oN initial_scan 10.10.10.27`
```
PORT     STATE SERVICE      REASON          VERSION
135/tcp  open  msrpc        syn-ack ttl 127 Microsoft Windows RPC
139/tcp  open  netbios-ssn  syn-ack ttl 127 Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds syn-ack ttl 127 Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
1433/tcp open  ms-sql-s     syn-ack ttl 127 Microsoft SQL Server 2017 14.00.1000
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows
```

## Task 2: Studying port 135
`135/tcp  open  msrpc        syn-ack ttl 127 Microsoft Windows RPC`

[handy Source for understanding the protocol](https://0xffsec.com/handbook/services/msrpc/)
[Microsoft RPC](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc738291(v=ws.10)?redirectedfrom=MSDN)

**If the Target is Windows Machine with RPC then use rpcclient to enumerate available services.**

```
You can query the RPC locator service and individual RPC endpoints to catalog interesting services running over TCP, UDP, HTTP, and SMB (via named pipes). Each IFID value gathered through this process denotes an RPC service (e.g., 5a7b91f8-ff00-11d0-a9b2-00c04fb6e6fc is the Messenger interface).
```
The Microsoft RPC mechanism uses other IPC mechanisms, such as named pipes, NetBIOS or Winsock, to establish communications between the client and the server.

We can use RPC to find out which service is running.

### Tool
- rpcdump(Windows): Find out IFID -> find out service running.
```
D:\rpctools> rpcdump [-p port] 192.168.189.1
IfId: 5a7b91f8-ff00-11d0-a9b2-00c04fb6e6fc version 1.0
Annotation: Messenger Service
UUID: 00000000-0000-0000-0000-000000000000
Binding: ncadg_ip_udp:192.168.189.1[1028]
```
### Enumeration
install [impacket](https://github.com/SecureAuthCorp/impacket#installing)

Using the .py file carry on the enumeration.

- impacket [rpcdump.py](https://0xffsec.com/handbook/services/msrpc/#fn:3)
