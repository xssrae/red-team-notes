---
tags:
  - Pentest
  - WEB
---
Web Enumeration

# Analyse Technics

- [OSINT/_Websites Analytics](https://notes.secure77.de/?link=%2FOFFSEC%20Notes%2FOSINT%2F_Websites%20Analytics)
- Checar extensões de arquivos: .php, jsp, .do, .html., txt, config, aspx, pdf, txt
- Checar tecnologias com `whatweb http://192.168.1.1`
- Checar e HTTP Headers, como x-Powered-By
- Checar o `robots.txt` e `sitemap.xml`
- Verifique os locais padrão do console, identificados na documentação do software do servidor de aplicativos (ou dar FUZZ neles)
- [BASIC Tool Set/Web Fuzzer](https://notes.secure77.de/?link=%2FOFFSEC%20Notes%2FBASIC%20Tool%20Set%2FWeb%20Fuzzer)
- Web Vuln. Scanner: [BASIC Tool Set/Nikto](https://notes.secure77.de/?link=%2FOFFSEC%20Notes%2FBASIC%20Tool%20Set%2FNikto)

# Headers

- [https://gist.github.com/iustin24/92a5ba76ee436c85716f003dda8eecc6](https://gist.github.com/iustin24/92a5ba76ee436c85716f003dda8eecc6)
- [https://securityheaders.com/](https://securityheaders.com/)

## Bypass 404

Alterar HTTP para 1.0 sem nenhum outro cabeçalho

[https://infosecwriteups.com/403-bypass-lyncdiscover-microsoft-com-db2778458c33](https://infosecwriteups.com/403-bypass-lyncdiscover-microsoft-com-db2778458c33)

## Bypass Proxy

[Network Services/Reverse Proxys](https://notes.secure77.de/?link=%2FOFFSEC%20Notes%2FNetwork%20Services%2FReverse%20Proxys)

# Methods

Verifique quais métodos de solicitação o servidor suporta (procure por PUT, o que significa que você pode fazer upload de arquivos)

```bash
$ curl -v -X OPTIONS <IP address>
```

Fazer upload de um arquivo usando curl

```bash
$ curl http://<IP address> --upload-file test.txt
```

## Go buster

```bash
gobuster dir -u http://192.168.162.120 -w /usr/share/wordlists/dirb/common.txt -x txt,pdf,config
```

# VHOST Discovery

## Go Buster

```bash
gobuster vhost -u love.htb -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```

## FFUF

```bash
ffuf -u http://earlyaccess.htb -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -H "Host: FUZZ.earlyaccess.htb" -fw 20
```


### via Proxy

```bash
gobuster vhost -u love.htb -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt --proxy http://127.0.0.1:8080
```

Defina também o Redirecionamento no ouvinte do Proxy!  


![[Pasted image 20231122020828.png]]

# Useful Links
## Enpoints
Crie um ponto de extremidade de endpoint público :
[https://beeceptor.com/](https://beeceptor.com/)

# OWASP Top 10 Checklist

2017 Version: [https://owasp.org/www-pdf-archive/OWASP_Top_10-2017_%28en%29.pdf.pdf](https://owasp.org/www-pdf-archive/OWASP_Top_10-2017_%28en%29.pdf.pdf)  
Checklist: [https://github.com/tanprathan/OWASP-Testing-Checklist](https://github.com/tanprathan/OWASP-Testing-Checklist)  
Reference PDF: [https://owasp.org/www-project-web-security-testing-guide/assets/archive/OWASP_Testing_Guide_v4.pdf](https://owasp.org/www-project-web-security-testing-guide/assets/archive/OWASP_Testing_Guide_v4.pdf)

## Broken Authentication
[Broken Authentication](https://notes.secure77.de/?link=%2FOFFSEC%20Notes%2FOWASP%20and%20Web%20Attacks%2FBroken%20Authentication)

## Sensitive Data Exposure
Procure por:
- Backups
- Arquivos Log 
- PDFs, Words, Excel, txt etc.

## Broken Access
verificar se você pode

- contornar os controles de acesso e postar como outro usuário etc.
- interceptar redirecionamentos de sites que normalmente precisam de autenticação.
# Security Misconfiguration

- Stack Traces e tratamento de erros
- Contas padrão etc.

[docs/OWASP_Testing_Guide_v4.pdf](https://notes.secure77.de/_Notes/OFFSEC Notes/OWASP and Web Attacks/docs/OWASP_Testing_Guide_v4.pdf)