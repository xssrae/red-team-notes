---
tags:
  - Pentest
  - WEB
---
Algumas ferramentas para utilizar *após a enumeração inicial* com **nmap** e *antes de enumeração de diretórios* com **gobuster**. por exemplo.
# ffuf
```shell
ffuf -w /usr/share/dirb/wordlists/common.txt -u http://10.10.25.119//FUZZ
```

