# Ch 1
## Connecting to Kali VM through ssh 

remove current SSH host keys: ```rm /etc/ssh/ssh_host_*```

reconfigure SSH host keys: ```dpkg-reconfigure openssh-server```

SSH automatic boot: ```systemctl enable ssh```

connect to kali VM: ```ssh <root>@<vm_ip>```

## PostgreSQL

```systemctl start postgresql```

```msfdb status```

```msfdb init```

edit database config file: ```cat /usr/share/metasploit-framework/config/database.yml```

```db_status```

## Workspace

```workspace```
```workspace -h```

## Using the database

```db_import <file1>```

ex) do the nmap scan and import the result

tip: ```db_nmap``` automatically imports the nmap result. Functions the same. 

## Hosts command

```hosts```

Scanned targets appear

## services command

services running on the targets appear

```services -h```

```services -s ftp```

```services -p 22```






This notes are taken from "Metasploit Penetration Testing Cookbook Third Edition" by "Daniel Teixeira, Abhinav Singh, Monika Agarwal"

Teixeria, D., Singh, A., &amp; Agarwal, M. (n.d.). Metasploit Penetration Testing Cookbook Third Edition. 

Push a commit if any issue noticed. 
