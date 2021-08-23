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
