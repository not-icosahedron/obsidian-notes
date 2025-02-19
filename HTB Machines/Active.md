# Initial Enumeration

All TCP port scan with Service Version enumeration.
``` bash
nmap -sS -sV -sC -T3 -p- <ip-address>
```

Some of the services found on the machine indicate that it is a Domain Controller, or as such capabilities;

```bash
53/tcp open domain Microsoft DNS 6.1.7601 (1DB15D39) (Windows Server 2008 R2 SP1) | dns-nsid: |_ bind.version: Microsoft DNS 6.1.7601 (1DB15D39) 
88/tcp open kerberos-sec Microsoft Windows Kerberos (server time: 2023-11-27 10:08:23Z) 135/tcp open msrpc Microsoft Windows RPC 
139/tcp open netbios-ssn Microsoft Windows netbios-ssn 
389/tcp open ldap Microsoft Windows Active Directory LDAP (Domain: active.htb, Site: Default-First-Site-Name) 
445/tcp open microsoft-ds? 464/tcp open kpasswd5? 
593/tcp open ncacn_http Microsoft Windows RPC over HTTP 1.0 636/tcp open tcpwrapped 
3268/tcp open ldap Microsoft Windows Active Directory LDAP (Domain: active.htb, Site: Default-First-Site-Name)
```
 DNS, LDAP and Kerberos services are active on this machine.
 