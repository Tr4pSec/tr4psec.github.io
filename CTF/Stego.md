# Stego

https://fareedfauzi.gitbook.io/ctf-checklist-for-beginner/steganography

Cracking steg:
https://github.com/Paradoxis/StegCracker

Install:
```
$ pip3 install stegcracker
```

```
$ stegcracker <file> [<wordlist>]
```
FASTER: https://github.com/RickdeJager/stegseek
```
stegseek [stegofile.jpg] [wordlist.txt]
```
```
stegseek --seed [stegofile.jpg]
```



Extracting hidden files with StegHide:
``` 
steghide extract -sf file.jpg -p "password" 
```

Extracting strings:
``` 
strings file.wav | awk 'length($0)>8' 
```

