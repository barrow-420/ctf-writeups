# Ultimate CTF Guide
## Just for me

## Port Scanning
### TCP Scanning
`sudo nmap -v -sV -sC -O -T4 -n -Pn -oA nmap_scan 10.0.0.3`

Scans the most common 1000 ports with service information (-sV), default scripts (-sC), and OS detection.

`sudo nmap -v -sV -sC -O -T4 -n -Pn -p- -oA nmap_fullscan 10.0.0.3`

Similar scan but scans all ports, from 1 through 65535.

### UDP Scanning
`sudo nmap -sU -sV --version-intensity 0 -n 10.0.0.0/24`

## Searching Exploit
Search vulnerabilities based on a Nmap’s XML result.

`searchsploit --nmap nmap.xml`

### Bruteforcing
[Resource Link](https://0xffsec.com/handbook/brute-forcing/)
