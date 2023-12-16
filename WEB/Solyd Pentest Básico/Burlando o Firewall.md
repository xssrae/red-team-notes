---
tags:
  - Pentest
  - WEB
---

Para burlar o Cloudflair e conseguir mandar requisições fora do Browser, é necessário pegar o cookie da página pela **header**:

```html
GET / HTTP/1.1
Host: www.bancocn.com
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Connection: keep-alive
Cookie: PHPSESSID=q07kaq4n5hqcdr7pskp7so1jv6
```

GET / HTTP/1.1
Host: lacrei-api-sandbox.herokuapp.com
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Connection: keep-alive
Cookie: csrftoken=5O8cpqoAULmDaGYG785zG5pUSW5yPjKJD1YupDAIdtLzKTG5k8ws87xmdCFfBCnq

Depois passar como parâmetro para o **dirb** junto com a url:

```shell
dirb https://host/ -a "Header" -c "cookies"
```

Exemplo:

```shell
dirb http://www.bancocn.com/ -a "Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0" -c "PHPSESSID=q07kaq4n5hqcdr7pskp7so1jv6s"
```

#### Brute-force de diretórios ocorrendo normalmente sem o barramento do Firewall:

