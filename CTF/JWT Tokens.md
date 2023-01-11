# JWT Tokens

Decode tokens:
https://jwt.io/

Tokens contain Header.Payload.Signature

Header = Name, Alg

Payload = Data

Signature = Secret


<br>

## Crunch charset:
```
cat /usr/share/crunch/charset.lst
 ```

## Creating a wordlist with Crunch:
```
sudo crunch 4 4 -f charset.lst mixalpha-numeric-all -o wordlist.txt
```


## Cracking the token with wordlist:
```
hashcat -m 16500 -a 0 token.txt wordlist.txt
```