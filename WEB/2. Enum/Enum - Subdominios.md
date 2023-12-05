---
tags:
  - WEB
  - Pentest
---
# google dorks
```
**-site:www.tryhackme.com  
site:*.tryhackme.com**
```
# dnsrecon
```shell
dnsrecon -t brt -d acmeitsupport.thm
```
# sublist3r
```shell
./sublist3r.py -d acmeitsupport.thm
```
# ffuf
```shell
ffuf -w /usr/share/wordlists/secLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.166.247

ffuf -w /usr/share/wordlists/secLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.166.247 -fs {size}`
```



