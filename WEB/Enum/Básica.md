---
tags:
  - Pentest
  - WEB
---
# Nmap

Comecemos com a verificação mais básica. Suponha que queremos executar um scan básico contra um alvo que reside em **10.129.42.253**. Para fazer isso, devemos digitar *nmap 10.129.42.253* e pressionar return. Nós vemos que o scan do Nmap foi completado muito rapidamente. Isso porque, se não especificarmos nenhuma opção adicional, o Nmap irá escanear apenas as *1.000* portas mais comuns por padrão. O resultado do scan revela que ==as portas 21, 22, 80, 139 e 445 estão disponíveis==.

```shell-session
$ nmap 10.129.42.253

Starting Nmap 7.80 ( https://nmap.org ) at 2021-02-25 16:07 EST
Nmap scan report for 10.129.42.253
Host is up (0.11s latency).
Not shown: 995 closed ports
PORT    STATE SERVICE
21/tcp  open  ftp
22/tcp  open  ssh
80/tcp  open  http
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds

Nmap done: 1 IP address (1 host up) scanned in 2.19 seconds
```

Por padrão, o Nmap irá efetuar um scan *TCP*, a não ser que seja especificamente pedido para efetuar um scan *UDP*.
Em *STATE*, confirmamos se a porta está aberta ou fechada. 
Em *SERVICE*, vemos que o serviço é geralmente mapeado por uma porta de número específico.

```shell-session
raekal1lvr@htb[/htb]$ nmap -sV -sC -p- 10.129.42.253

Starting Nmap 7.80 ( https://nmap.org ) at 2021-02-25 16:18 EST
Nmap scan report for 10.129.42.253
Host is up (0.11s latency).
Not shown: 65530 closed ports
PORT    STATE SERVICE     VERSION
21/tcp  open  ftp         vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_drwxr-xr-x    2 ftp      ftp          4096 Feb 25 19:25 pub
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.10.14.2
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 2
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
	22/tcp  open  ssh         OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; 
	protocol 2.0)
	80/tcp  open  http        Apache httpd 2.4.41 ((Ubuntu))
	|_http-server-header: Apache/2.4.41 (Ubuntu)
	|_http-title: PHP 7.4.3 - phpinfo()
	139/tcp open  netbios-ssn Samba smbd 4.6.2
	445/tcp open  netbios-ssn Samba smbd 4.6.2
	Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```


Esses comandos, nos retornam mais informações. As opções -*sC* e -*sV* também aumentam a duração de uma verificação, pois em vez de efetuar um simples aperto de mão TCP, efetuam mais verificações. Notamos que desta vez existe um cabeçalho *VERSION*, que informa a versão do serviço e o sistema operativo, se for possível identificá-lo. Até agora, sabemos que o sistema operativo é o Ubuntu Linux. As versões das aplicações também podem ajudar a revelar a versão do SO de destino.

# Serviços da Rede

#### Banner Grabbing

O *banner grabbing* é uma técnica útil para identificar rapidamente um serviço. O Nmap tentará pegar os banners se a sintaxe *nmap -sV --script=banner </target/ >* for especificada. Nós também podemos tentar fazer isso manualmente usando o Netcat. Vamos dar outro exemplo, usando a versão nc do Netcat:

```shell-session
$ nc -nv 10.129.42.253 21

(UNKNOWN) [10.129.42.253] 21 (ftp) open
220 (vsFTPd 3.0.3)
```

Isso revela que a versão do *vsFTPd* no servidor é *3.0.3*.

#### FTP

É importante obter familiaridade com o *FTP*, pois, é um protocolo comumente utilizado, e esse serviço frequentemente pode conter dados interessantes.

> NMAP scan:

```shell-session
nmap -sC -sV -p21 10.129.42.253

Starting Nmap 7.80 ( https://nmap.org ) at 2020-12-20 00:54 GMT
Nmap scan report for 10.129.42.253
Host is up (0.081s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_drwxr-xr-x    2 ftp      ftp          4096 Dec 19 23:50 pub
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.10.14.2
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 3
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
Service Info: OS: Unix

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 1.78 seconds
```

> FTP scan:

```shell-session
raekal1lvr@htb[/htb]$ ftp -p 10.129.42.253

Connected to 10.129.42.253.
220 (vsFTPd 3.0.3)
Name (10.129.42.253:user): anonymous
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.

ftp> ls
227 Entering Passive Mode (10,129,42,253,158,60).
150 Here comes the directory listing.
drwxr-xr-x    2 ftp      ftp          4096 Feb 25 19:25 pub
226 Directory send OK.

ftp> cd pub
250 Directory successfully changed.

ftp> ls
227 Entering Passive Mode (10,129,42,253,182,129).
150 Here comes the directory listing.
-rw-r--r--    1 ftp      ftp            18 Feb 25 19:25 login.txt
226 Directory send OK.

ftp> get login.txt // note que aqui o comando 'cat' não irá 
local: login.txt remote: login.txt //funcionar. use 'get'
227 Entering Passive Mode (10,129,42,253,181,53).
150 Opening BINARY mode data connection for login.txt (18 bytes).
226 Transfer complete.
18 bytes received in 0.00 secs (165.8314 kB/s)

ftp> exit
221 Goodbye.
```

#### SMB

*SMB* (Server Message Block) é um protocolo mais comum em maquinas *Windows* que permite muitos vetores para movimentos verticais e laterais de ação. **Dados sensíveis**, como credenciais, podem estar partilhados em arquivos de rede, e algumas versões de SMB podem ser vulneráveis a exploits. O Nmap tem muitos scripts para enumerar o SMB, como o [smb-os-discovery.nse](https://nmap.org/nsedoc/scripts/smb-os-discovery.html) que irá interagir com o serviço SMB para extrair a versão do sistema operacional relatada.

```shell-session
raekal1lvr@htb[/htb]$ nmap --script smb-os-discovery.nse -p445 10.10.10.40

Starting Nmap 7.91 ( https://nmap.org ) at 2020-12-27 00:59 GMT
Nmap scan report for doctors.htb (10.10.10.40)
Host is up (0.022s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-os-discovery: 
|   OS: Windows 7 Professional 7601 Service Pack 1 (Windows 7 Professional 6.1)
|   OS CPE: cpe:/o:microsoft:windows_7::sp1:professional
|   Computer name: CEO-PC
|   NetBIOS computer name: CEO-PC\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2020-12-27T00:59:46+00:00

Nmap done: 1 IP address (1 host up) scanned in 2.71 seconds
```

Neste caso, o alvo executa um sistema operativo *Windows 7* antigo e podemos efetuar uma enumeração adicional para confirmar se é vulnerável ao *EternalBlue*. O *Metasploit Framework* tem vários módulos para o EternalBlue que podem ser utilizados para validar a vulnerabilidade e explorá-la. Podemos executar um *scan* no nosso alvo para esta secção do módulo para recolher informações do serviço SMB. Podemos verificar que o host executa um kernel Linux, Samba versão 4.6.2, e o nome do host é *GS-SVCSCAN*.

```shell-session
raekal1lvr@htb[/htb]$ nmap -A -p445 10.129.42.253

Starting Nmap 7.80 ( https://nmap.org ) at 2021-02-25 16:29 EST
Nmap scan report for 10.129.42.253
Host is up (0.11s latency).

PORT    STATE SERVICE     VERSION
445/tcp open  netbios-ssn Samba smbd 4.6.2
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 2.6.32 (95%), Linux 3.1 (95%), Linux 3.2 (95%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (94%), ASUS RT-N56U WAP (Linux 3.4) (93%), Linux 3.16 (93%), Adtran 424RG FTTH gateway (92%), Linux 2.6.39 - 3.2 (92%), Linux 3.1 - 3.2 (92%), Linux 3.2 - 4.9 (92%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops

Host script results:
|_nbstat: NetBIOS name: GS-SVCSCAN, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-02-25T21:30:06
|_  start_date: N/A

TRACEROUTE (using port 445/tcp)
HOP RTT       ADDRESS
1   111.62 ms 10.10.14.1
2   111.89 ms 10.129.42.253

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.72 seconds
```


#### Shares

O *SMB* permite que os utilizadores e administradores *partilhem pastas* e as tornem *acessíveis remotamente* a outros utilizadores. Muitas vezes, estas partilhas têm ficheiros que contêm **informações sensíveis**, tais como palavras-passe. Uma ferramenta que pode enumerar e interagir com as partilhas SMB é o smbclient. O sinalizador -L especifica que queremos obter uma lista de partilhas disponíveis na máquina remota, enquanto que -N suprime o pedido de palavra-passe.

```shell-session
raekal1lvr@htb[/htb]$ smbclient -N -L \\\\10.129.42.253

	Sharename       Type      Comment
	---------       ----      -------
	print$          Disk      Printer Drivers
	users           Disk      
	IPC$            IPC       IPC Service (gs-svcscan server (Samba, Ubuntu))
SMB1 disabled -- no workgroup available
```

Isto revela os *utilizadores* de partilha não predefinidos. Vamos tentar ligar-nos como o utilizador convidado.

```shell-session
raekal1lvr@htb[/htb]$ smbclient -U bob \\\\10.129.42.253\\users

Enter WORKGROUP\bob's password: 
Try "help" to get a list of possible commands.

smb: \> ls
  .                                   D        0  Thu Feb 25 16:42:23 2021
  ..                                  D        0  Thu Feb 25 15:05:31 2021
  bob                                 D        0  Thu Feb 25 16:42:23 2021

		4062912 blocks of size 1024. 1332480 blocks available
		
smb: \> cd bob

smb: \bob\> ls
  .                                   D        0  Thu Feb 25 16:42:23 2021
  ..                                  D        0  Thu Feb 25 16:42:23 2021
  passwords.txt                       N      156  Thu Feb 25 16:42:23 2021

		4062912 blocks of size 1024. 1332480 blocks available
		
smb: \bob\> get passwords.txt 
getting file \bob\passwords.txt of size 156 as passwords.txt (0.3 KiloBytes/sec) (average 0.3 KiloBytes/sec)
```

# Gobuster 
O **GoBuster** é uma ferramenta versátil que permite a execução de força bruta de DNS, vhost e diretório. A ferramenta tem funcionalidades adicionais, como a enumeração de buckets públicos do AWS S3. Vamos executar uma verificação simples usando a lista de palavras. `dirb common.txt`.

```shell
raekal1lvr@htb[/htb]$ gobuster dir -u http://10.10.10.121/ -w /usr/share/dirb/wordlists/common.txt

===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.10.121/
[+] Threads:        10
[+] Wordlist:       /usr/share/dirb/wordlists/common.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2020/12/11 21:47:25 Starting gobuster
===============================================================
/.hta (Status: 403)
/.htpasswd (Status: 403)
/.htaccess (Status: 403)
/index.php (Status: 200)
/server-status (Status: 403)
/wordpress (Status: 301)
===============================================================
2020/12/11 21:47:46 Finished
===============================================================
```

Um código de status ``HTTP 200`` revela que a solicitação do recurso foi bem-sucedida, enquanto um código de status ``HTTP 403`` indica que estamos proibidos de acessar o recurso. Um código de status ``301`` indica que estamos sendo redirecionados, o que não é um caso de falha. 

A verificação foi concluída com êxito e identifica uma instalação do WordPress em 
``/wordpress``. Nesse caso, é possivel visitar http://10.10.10.121/wordpress em um navegador.


# Enumeração de Subdomínio

Podemos usar o **GoBuster** para enumerar os subdomínios disponíveis de um determinado domínio usando o sinalizador dns para especificar o modo DNS. Primeiro, vamos clonar o repositório SecLists do GitHub, que contém muitas listas úteis para fuzzing e exploração:

```shell
raekal1lvr@htb[/htb]$ git clone https://github.com/danielmiessler/SecLists
```

```shell
raekal1lvr@htb[/htb]$ sudo apt install seclists -y
```

Em seguida, adicione um servidor DNS, como 1.1.1.1, ao arquivo ``/etc/resolv.conf``. Vamos direcionar o domínio ``inlanefreight.com``, o site de uma empresa fictícia de frete e logística.

```shell
raekal1lvr@htb[/htb]$ gobuster dns -d inlanefreight.com -w /usr/share/SecLists/Discovery/DNS/namelist.txt

===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Domain:     inlanefreight.com
[+] Threads:    10
[+] Timeout:    1s
[+] Wordlist:   /usr/share/SecLists/Discovery/DNS/namelist.txt
===============================================================
2020/12/17 23:08:55 Starting gobuster
===============================================================
Found: blog.inlanefreight.com
Found: customer.inlanefreight.com
Found: my.inlanefreight.com
Found: ns1.inlanefreight.com
Found: ns2.inlanefreight.com
Found: ns3.inlanefreight.com
===============================================================
2020/12/17 23:10:34 Finished
===============================================================
```

# Web Enumeration Tips

### cURL
 
 Podemos usar o **cURL** para recuperar informações do cabeçalho do servidor a partir da linha de comando. O cURL é outro acréscimo essencial ao nosso kit de ferramentas de teste de penetração, e é recomendável que nos familiarizemos com suas diversas opções.

```shell
raekal1lvr@htb[/htb]$ curl -IL https://www.inlanefreight.com

HTTP/1.1 200 OK
Date: Fri, 18 Dec 2020 22:24:05 GMT
Server: Apache/2.4.29 (Ubuntu)
Link: <https://www.inlanefreight.com/index.php/wp-json/>; rel="https://api.w.org/"
Link: <https://www.inlanefreight.com/>; rel=shortlink
Content-Type: text/html; charset=UTF-8
```


#### Whatweb
Podemos extrair a versão de servidores Web, estruturas de suporte e aplicativos usando a ferramenta de linha de comando **whatweb**. Essas informações podem nos ajudar a identificar as tecnologias em uso e começar a procurar possíveis vulnerabilidades.

```shell
raekal1lvr@htb[/htb]$ whatweb 10.10.10.121

http://10.10.10.121 [200 OK] Apache[2.4.41], Country[RESERVED][ZZ], Email[license@php.net], HTTPServer[Ubuntu Linux][Apache/2.4.41 (Ubuntu)], IP[10.10.10.121], Title[PHP 7.4.3 - phpinfo()]
```

```shell
raekal1lvr@htb[/htb]$ whatweb --no-errors 10.10.10.0/24

http://10.10.10.11 [200 OK] Country[RESERVED][ZZ], HTTPServer[nginx/1.14.1], IP[10.10.10.11], PoweredBy[Red,nginx], Title[Test Page for the Nginx HTTP Server on Red Hat Enterprise Linux], nginx[1.14.1]
http://10.10.10.100 [200 OK] Apache[2.4.41], Country[RESERVED][ZZ], HTTPServer[Ubuntu Linux][Apache/2.4.41 (Ubuntu)], IP[10.10.10.100], Title[File Sharing Service]
http://10.10.10.121 [200 OK] Apache[2.4.41], Country[RESERVED][ZZ], Email[license@php.net], HTTPServer[Ubuntu Linux][Apache/2.4.41 (Ubuntu)], IP[10.10.10.121], Title[PHP 7.4.3 - phpinfo()]
http://10.10.10.247 [200 OK] Bootstrap, Country[RESERVED][ZZ], Email[contact@cross-fit.htb], Frame, HTML5, HTTPServer[OpenBSD httpd], IP[10.10.10.247], JQuery[3.3.1], PHP[7.4.12], Script, Title[Fine Wines], X-Powered-By[PHP/7.4.12], X-UA-Compatible[ie=edge]
```

### Robots.txt
É comum que os sites contenham um arquivo robots.txt, cuja finalidade é instruir os rastreadores da Web dos mecanismos de pesquisa, como o Googlebot, sobre quais recursos podem ou não ser acessados para indexação. O arquivo robots.txt pode fornecer informações valiosas, como o local de arquivos privados e páginas de administração. Nesse caso, vemos que o arquivo robots.txt contém duas entradas não permitidas.

![phpinfo](https://academy.hackthebox.com/storage/modules/77/robots.png)

Navegar para http://10.10.10.121/private em um navegador revela uma página de login de administrador do HTB.

![phpinfo](https://academy.hackthebox.com/storage/modules/77/academy.png)

### Código fonte
Também vale a pena verificar o código-fonte de todas as páginas da Web que encontrarmos. Podemos pressionar ``[CTRL + U]`` para abrir a janela do código-fonte em um navegador. Este exemplo revela um comentário de desenvolvedor contendo credenciais para uma conta de teste, que poderia ser usada para fazer login no site.
![phpinfo](https://academy.hackthebox.com/storage/modules/77/source.png)

