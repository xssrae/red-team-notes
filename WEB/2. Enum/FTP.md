---
tags:
  - Pentest
  - WEB
  - REDES
---
# Localizando a porta FTP

Localize qual porta o protocolo FTP está rodando e qual versão do FTP

```shell
$ nmap -vn 172.16.1.0/24 21 
```

# Logar via Anonymous
![[Pasted image 20231122022913.png]]

Caso não esteja habilidado o Anonymous, com a versão anteriormente localizada conseguimos dar bypass por meio de exploits.

# FTP com Python
