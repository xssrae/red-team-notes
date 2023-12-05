# Processos
Quando o sistema é inicializado, muitos processos são secretamente iniciados, quase sempre desconhecidos para o usuário. Por exemplo, um processo pode ser inicializado para esperar pela chegada de e-mails. *Outro pode ser executado em prol do programa antivírus para conferir periodicamente se há novas definições de vírus disponíveis*. Além disso, ==processos explícitos de usuários podem ser executados, imprimindo arquivos e salvando as fotos do usuário em um pen-drive,== tudo isso enquanto o usuário está navegando na Web. Toda essa atividade tem de ser gerenciada, e um sistema de multiprogramação que dê suporte a múltiplos processos é muito útil nesse caso.

- Em qualquer sistema de multiprogramação, a CPU muda de um processo para outro rapidamente, executando cada um por dezenas ou centenas de milissegundos.
- Quando um sistema operacional é inicializado, em geral uma série de processos é criada.

Em sistemas interativos, os usuários podem começar um programa digitando um comando ou clicando duas vezes sobre um ícone.

# Threads
 Em muitas situações, é desejável ter múltiplos threads de controle no mesmo espaço de en-
dereçamento executando em quase paralelo, como se eles
fossem (quase) processos separados (exceto pelo espaço
de endereçamento compartilhado

