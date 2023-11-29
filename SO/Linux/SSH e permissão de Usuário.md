---
tags:
  - Linux
  - SO
---
# O que é SSH e como ele funciona?

**Secure Shell** ou **SSH** é simplesmente um protocolo entre dispositivos em um *formato criptografado*. Usando criptografia, qualquer entrada que enviamos em um formato legível por humanos é criptografada para viajar por uma rede, onde é descriptografada quando chega à máquina remota, como no diagrama abaixo.

  

![](https://lh3.googleusercontent.com/yIWaoU620B3_wDIY8pMr3cKAlVHXDCGZiOkz_T6ZAdHHk5q4PFUg2XM6T90y3evJELOI0nfKR22RcpFpbNDuxe-pDwx4B8f_Mo7OCW392IZsaxyJXBR8PBftiMHGYX-Kw5uOL7-27H22gwd_3anSRBU)

  
O SSH nos permite executar comandos remotamente em outro dispositivo.

Todos os dados enviados entre os dispositivos são criptografados quando são enviados por uma rede, como a Internet

## Introdução aos sinalizadores e comutadores

A maioria dos comandos permite o fornecimento de argumentos. Esses argumentos são identificados por um hífen e uma determinada palavra-chave conhecida como sinalizadores ou switches.

Ao usar um comando, a menos que especificado de outra forma, ele executará seu comportamento padrão. Por exemplo, ls lista o conteúdo do diretório de trabalho. Entretanto, os arquivos ocultos não são mostrados. Podemos usar sinalizadores e opções para ampliar o comportamento dos comandos.

```shell script
@linux2:~$ ls
folder1

@linux2:~$
@linux2:~$ ls -a 
.hiddenfolder folder1

@linux2:~$
```

### Interação com o sistema de arquivos Continuação
|   |   |
|---|---|
|**COMANDO**|**USO**|
|*touch*|Criar arquivo|
|*mkdir*|Criar pasta|
|*cp*|Copiar arquivos ou pastas|
|*mv*|Mover arquivos ou pastas|
|*rm*|Remover arquivos ou pastas|
|*file*|Determinar tipo|

# Permissões 101
O comando **ls**, que lista o conteúdo do diretório atual. Ao usar a opção -l, podemos ver dez colunas, como na captura de tela abaixo. No entanto, estamos interessados apenas nas três primeiras colunas:

```shell script
rae@linux2:~$ ls -lh

-rw-r--r-- 1 cmnatic cmnatic 0 Feb 19 10:37 file1

-rw-r--r-- 8 cmnatic cmnatic 0 Feb 19 10:37 file2
```

Embora intimidadoras, essas três colunas são muito importantes para determinar certas características de um arquivo ou pasta e se temos ou não acesso a ele. Um arquivo ou pasta pode ter algumas características que determinam quais ações são permitidas e qual usuário ou grupo tem a capacidade de executar determinada ação, como as seguintes:
- Leitura
- Gravar
- Executar

Usando o su para mudar para o usuário2
```shell script
rae@linux2:~$ su user2

Password:

user2@linux2:/home/tryhackme$
```

### Resumidamente: As diferenças entre usuários e grupos
A grande vantagem do Linux é que as permissões podem ser tão granulares que, embora um usuário seja tecnicamente o proprietário de um arquivo, se as permissões tiverem sido definidas, um grupo de usuários também poderá ter o mesmo conjunto de permissões ou um conjunto diferente de permissões para o mesmo arquivo sem afetar o proprietário do arquivo.

## Alternância entre usuários

Alternar entre usuários em uma instalação do Linux é uma tarefa fácil graças ao comando **su** É necessário saber duas coisas para facilitar essa transição de contas de usuário:
- O usuário para o qual desejamos mudar
- A senha do usuário

O comando **su** usa algumas opções que podem ser relevantes. Por exemplo, a execução de um comando após o login ou a especificação de um shell específico a ser usado. 

Simplesmente, ao fornecer a opção -l ao su, iniciamos um shell que é muito mais semelhante ao do usuário real que está fazendo login no sistema - herdamos muito mais propriedades do novo usuário, ou seja, variáveis de ambiente e similares.

```shell
rae@linux2:~$ su user2 Password: user2@linux2:/home/tryhackme$
```


```shell
rae@linux2:~$ su -l user2 
Password: 
user2@linux2:~$ pwd 
user2@:/home/user2$
```

# Diretórios comuns

## /etc

Este diretório **raiz** é um dos directórios raiz mais importantes do seu sistema. A pasta etc é um local comum para armazenar **ficheiros de sistema** que são utilizados pelo seu sistema operativo.

Por exemplo, o ficheiro sudoers destacado na captura de ecrã abaixo contém uma *lista dos utilizadores e grupos que têm permissão para executar o sudo ou um conjunto de comandos como o utilizador root.*

> Também destacados abaixo estão os ficheiros "passwd" e "shadow". Estes dois ficheiros são especiais para o Linux, pois mostram como o seu sistema armazena as palavras-passe de cada utilizador num formato encriptado chamado **sha512**.

```shell
rae@linux2:/etc$ ls 
shadow passwd sudoers sudoers.d
```

## /var

O diretório **"/var"** armazena **dados** que são *frequentemente acedidos ou escritos por serviços ou aplicações em execução no sistema*. Por exemplo, os ficheiros de registo dos serviços e aplicações em execução são escritos aqui (/var/log), ou outros dados que não estão necessariamente associados a um utilizador específico (i.e., bases de dados e afins).

```shell
rae@linux2:/var$ ls 
backups log opt tmp
```


## /root

Ao contrário do diretório /home, a pasta /root é na realidade a *casa do utilizador do sistema* "root". Não há mais nada a dizer sobre esta pasta para além de compreender que é o **diretório home do utilizador "root".**

```shell
root@linux2:~# ls 
myfile myfolder passwords.xlsx
```


## /tmp

O diretório /tmp é **volátil**, utilizado para armazenar dados que só precisam de ser acedidos **uma ou duas vezes**. Semelhante à **memória** do seu computador, assim que o computador é reiniciado, o conteúdo desta pasta é limpo.

O que é útil para nós do pentest é que qualquer utilizador pode escrever nesta pasta por default. Isso significa que, uma vez que temos acesso a uma máquina, ela serve como um bom lugar para armazenar coisas como nossos **scripts de enumeração**.

```shell
root@linux2:/tmp# ls 
todelete trash.txt rubbish.bin
```