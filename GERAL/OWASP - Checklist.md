---
tags:
  - GERAL
  - Relatório
---
# OWASP Web Application Security Testing Checklist
-------
# Coleta de informações
- [ ] Explorar manualmente o site
- [ ] Rastreamento para conteúdo perdido ou oculto
- [ ] Verifique se há arquivos que expõem o conteúdo, como robots.txt, sitemap.xml, .DS_Store
- [ ] Verifique os caches dos principais mecanismos de pesquisa para sites acessíveis ao público
- [ ] Verifique se há diferenças no conteúdo com base no agente do usuário (por exemplo, sites móveis, acesso como um rastreador de mecanismo de pesquisa)
- [ ] Realizar a impressão digital de aplicativos da Web
- [ ] Identificar as tecnologias usadas
- [ ] Identificar funções de usuário
- [ ] Identificar pontos de entrada do aplicativo
- [ ] Identificar o código do lado do cliente
- [ ] Identificar várias versões/canais (por exemplo, web, web móvel, aplicativo móvel, serviços da web)
- [ ] Identificar aplicativos co-hospedados e relacionados
- [ ] Identificar todos os nomes de host e portas
- [ ] Identificar conteúdo hospedado por terceiros


# Gerenciamento de configuração

- [ ] Verifique se há URLs administrativos e de aplicativos usados com frequência
- [ ] Verificar se há arquivos antigos, de backup e não referenciados
- [ ] Verificar os métodos HTTP suportados e o Cross Site Tracing (XST)
- [ ] Teste o manuseio de extensões de arquivos
- [ ] Teste os cabeçalhos HTTP de segurança (por exemplo, CSP, X-Frame-Options, HSTS)
- [ ] Teste de políticas (por exemplo, Flash, Silverlight, robôs)
- [ ] Teste de dados de não produção em um ambiente ativo e vice-versa
- [ ] Verifique se há dados confidenciais no código do lado do cliente (por exemplo, chaves de API, credenciais)


# Transmissão segura

- [ ] Verificar a versão SSL, os algoritmos e o comprimento da chave
- [ ] Verificar a validade do certificado digital (duração, assinatura e CN)
- [ ] Verificar se as credenciais são entregues somente por HTTPS
- [ ] Verificar se o formulário de login é entregue por HTTPS
- [ ] Verificar se os tokens de sessão são entregues somente por HTTPS
- [ ] Verificar se o HTTP Strict Transport Security (HSTS) está sendo usado

# Autenticação
- [ ] Teste para enumeração de usuários
- [ ] Teste de desvio de autenticação
- [ ] Teste de proteção por força bruta
- [ ] Teste de regras de qualidade de senha
- [ ] Teste a funcionalidade "lembrar de mim
- [ ] Teste de preenchimento automático em formulários/entradas de senhas
- [ ] Teste de redefinição e/ou recuperação de senha
- [ ] Teste o processo de alteração de senha
- [ ] Teste CAPTCHA
- [ ] Teste a autenticação multifatorial
- [ ] Teste a presença da funcionalidade de logout
- [ ] Teste o gerenciamento de cache em HTTP (por exemplo, Pragma, Expires, Max-age)
- [ ] Teste de logins padrão
- [ ] Teste para histórico de autenticação acessível ao usuário
- [ ] Teste para notificação fora do canal de bloqueios de conta e alterações bem-sucedidas de senha
- [ ] Teste para autenticação consistente entre aplicativos com esquema de autenticação compartilhado / SSO



### <a name="Session">Session Management</a>
- [ ] Estabeleça como o gerenciamento de sessão é tratado no aplicativo (por exemplo, tokens em cookies, token em URL)
- [ ] Verificar os tokens de sessão quanto aos sinalizadores de cookie (httpOnly e secure)
- [ ]  Verificar o escopo do cookie da sessão (caminho e domínio)
- [ ] Verificar a duração do cookie da sessão (expiração e idade máxima)
- [ ] Verificar o encerramento da sessão após um tempo máximo de vida
- [ ] Verificar o encerramento da sessão após o tempo limite relativo
- [ ] Verificar o encerramento da sessão após o logout
- [ ] Teste para ver se os usuários podem ter várias sessões simultâneas
- [ ] Testar a aleatoriedade dos cookies de sessão
- [ ] Confirmar se novos tokens de sessão são emitidos no login, na mudança de função e no logout
- [ ] Teste o gerenciamento consistente de sessões entre aplicativos com gerenciamento compartilhado de sessões
- [ ] Teste de confusão de sessões
- [ ] Teste para CSRF e clickjacking



# Autorização
- [ ] Test for path traversal
- [ ] Test for bypassing authorization schema
- [ ] Test for vertical Access control problems (a.k.a. Privilege Escalation)
- [ ] Test for horizontal Access control problems (between two users at the same privilege level)
- [ ] Test for missing authorization


### <a name="Validation">Data Validation</a>
- [ ] Test for Reflected Cross Site Scripting
- [ ] Test for Stored Cross Site Scripting
- [ ] Test for DOM based Cross Site Scripting
- [ ] Test for Cross Site Flashing
- [ ] Test for HTML Injection
- [ ] Test for SQL Injection
- [ ] Test for SOQL Injection
- [ ] Test for LDAP Injection
- [ ] Test for ORM Injection
- [ ] Test for XML Injection
- [ ] Test for XXE Injection
- [ ] Test for SSI Injection
- [ ] Test for XPath Injection
- [ ] Test for XQuery Injection
- [ ] Test for IMAP/SMTP Injection
- [ ] Test for Code Injection
- [ ] Test for Expression Language Injection
- [ ] Test for Command Injection
- [ ] Test for Overflow (Stack, Heap and Integer)
- [ ] Test for Format String
- [ ] Test for incubated vulnerabilities
- [ ] Test for HTTP Splitting/Smuggling
- [ ] Test for HTTP Verb Tampering
- [ ] Test for Open Redirection
- [ ] Test for Local File Inclusion
- [ ] Test for Remote File Inclusion
- [ ] Compare client-side and server-side validation rules
- [ ] Test for NoSQL injection
- [ ] Test for HTTP parameter pollution
- [ ] Test for auto-binding
- [ ] Test for Mass Assignment
- [ ] Test for NULL/Invalid Session Cookie

### <a name="Denial">Denial of Service</a>
- [ ] Test for anti-automation
- [ ] Test for account lockout
- [ ] Test for HTTP protocol DoS
- [ ] Test for SQL wildcard DoS


### <a name="Business">Business Logic</a>
- [ ] Test for feature misuse
- [ ] Test for lack of non-repudiation
- [ ] Test for trust relationships
- [ ] Test for integrity of data
- [ ] Test segregation of duties


### <a name="Cryptography">Cryptography</a>
- [ ] Check if data which should be encrypted is not
- [ ] Check for wrong algorithms usage depending on context
- [ ] Check for weak algorithms usage
- [ ] Check for proper use of salting
- [ ] Check for randomness functions


### <a name="File">Risky Functionality - File Uploads</a>
- [ ] Test that acceptable file types are whitelisted
- [ ] Test that file size limits, upload frequency and total file counts are defined and are enforced
- [ ] Test that file contents match the defined file type
- [ ] Test that all file uploads have Anti-Virus scanning in-place.
- [ ] Test that unsafe filenames are sanitised
- [ ] Test that uploaded files are not directly accessible within the web root
- [ ] Test that uploaded files are not served on the same hostname/port
- [ ] Test that files and other media are integrated with the authentication and authorisation schemas


### <a name="Card">Risky Functionality - Card Payment</a>
- [ ] Test for known vulnerabilities and configuration issues on Web Server and Web Application
- [ ] Test for default or guessable password
- [ ] Test for non-production data in live environment, and vice-versa
- [ ] Test for Injection vulnerabilities
- [ ] Test for Buffer Overflows
- [ ] Test for Insecure Cryptographic Storage
- [ ] Test for Insufficient Transport Layer Protection
- [ ] Test for Improper Error Handling
- [ ] Test for all vulnerabilities with a CVSS v2 score > 4.0
- [ ] Test for Authentication and Authorization issues
- [ ] Test for CSRF


### <a name="HTML">HTML 5</a>
- [ ] Test Web Messaging
- [ ] Test for Web Storage SQL injection
- [ ] Check CORS implementation
- [ ] Check Offline Web Application

Source: [OWASP](https://www.owasp.org/index.php/Web_Application_Security_Testing_Cheat_Sheet)
