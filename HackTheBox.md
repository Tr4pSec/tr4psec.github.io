# HackTheBox

Hack The Box is an online platform allowing you to test your penetration testing skills and exchange ideas and methodologies with thousands of people in the security field.

<img src="https://www.hackthebox.eu/badge/image/134841" alt="Hack The Box">

Link to HTB: \
[http://hackthebox.eu/](http://hackthebox.eu/) 

Tools I use: 
* [Kali Linux](https://www.kali.org/) (Linux distro for pentesting) 
* [Commando VM](https://github.com/fireeye/commando-vm) (Windows VM for pentesting)

Help resources: 
* [IppSec](https://www.youtube.com/channel/UCa6eh7gCkpPo5XXUDfygQQA) (Youtube walkthrough videos) 
* [The Cyber Mentor](https://www.youtube.com/channel/UC0ArlFuFYMpEewyRBzdLHiw) (Youtube tutorials)
* [Rapid7](https://www.rapid7.com/db/) (Vulnerability & Exploit Database)
* [Exploit DB](https://www.exploit-db.com/) (Exploit Database)
* [Hack the Box Forums](https://forum.hackthebox.eu/)

### Kali Linux commands

Portscanning target with nmap
```
nmap -A -T4 -p- [targetIP]
```
FTP
```
ftp [targetIP]
```
SMB Client
```
smbclient -L [targetIP] -U [username]
```
Query netbios names
```
nmblookup -A [targetIP]
```
Finding open shares
```
nbtscan [targetIP]
```
Enumerate samba shares
```
smbmap -H [targetIP]
```
Windows enumeration
```
enum4linux -a [targetIP]
```
Locate path of files
``` 
locate [string]
```
Enumerating users with impacket
```
python3 ./samrdump.py [targetIP]
```
Get password hash from user using kerberosting
```
python3 ./GetNPUsers.py DOMAIN/username -no-pass -dc-ip [dcIPaddress]
```
Crack a password hash
```
john -wordlist=/usr/share/wordlists/rockyou.txt [filewithhashes.txt]
```
Connect over winrm
```
evil-winrm -u [username] -i [targetIP]
```
