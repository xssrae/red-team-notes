---
tags:
  - WEB
  - Pentest
---
# Path Transversal
Uma vulnerabilidade de segurança na Web *permite que um invasor leia recursos do sistema operacional*, como **arquivos locais no servidor** que executa um aplicativo.

O gráfico a seguir mostra como um aplicativo da Web armazena arquivos em `/var/www/app`. O caminho feliz seria o usuário solicitando o conteúdo de `userCV.pdf` de um caminho definido `/var/www/app/CVs`.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5d617515c8cd8348d0b4e68f/room-content/45d9c1baacda290c1f95858e27f740c9.png)

 Se o invasor encontrar o ponto de entrada, que, nesse caso, é `get.php?file=`, ele poderá enviar algo como o seguinte, `http://webapp.thm/get.php?file=../../../../etc/passwd`

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5d617515c8cd8348d0b4e68f/room-content/3037513935e3242f74bd0fe97833b5ac.png)

# LFI 1
Os ataques de LFI contra aplicativos da Web geralmente se devem à falta de conscientização de segurança por parte dos desenvolvedores.

1. Suponha que o aplicativo da Web ofereça dois idiomas e que o usuário possa selecionar entre *EN* e *AR*
```php
<?PHP 
	include($_GET["lang"]);
?>
```

2. Em seguida, no código a seguir, o desenvolvedor decidiu especificar o diretório dentro da função

```php
<?PHP 
	include("languages/". $_GET['lang']); 
?>
```
# LFI 2
Nesse caso, os erros são importantes para entender como os dados são transmitidos e processados no aplicativo Web.

```php
Warning: include(languages/THM.php): failed to open stream: No such file or directory in /var/www/html/THM-4/index.php on line 12
```

Além disso, a mensagem de erro revelou outra informação importante sobre o caminho completo do diretório da aplicação Web, que é ``/var/www/html/THM-4/`

A **utilização de bytes nulos** é uma técnica de injeção em que a representação codificada por URL, como *%00* ou *0x00* em hexadecimal, com dados fornecidos pelo utilizador para terminar cadeias de caracteres. Pode pensar-se nisto como uma tentativa de enganar a aplicação web para que ignore o que vem a seguir ao byte nulo.

Ao adicionar o byte nulo no final do payload, dizemos à função de inclusão para ignorar qualquer coisa após o byte nulo, que pode ter o seguinte aspeto:

`include("languages/../../../../../../etc/passwd%00").".php");` o que equivale a → `include("languages/../../../../../../etc/passwd");`

Outro tipo de payload: `....//....//....//....//....//etc/passwd`
Diretório especifico: `M-profile%/../../../../../etc/os-release`
## Etapas do teste para IFL

1. Encontrar um *ponto de entrada* que pode ser através de **GET**, **POST**, **COOKIE** ou valores de **cabeçalho HTTP**!
2. Introduzir uma **entrada válida** para ver como o servidor Web se comporta.
3. Introduza **entradas inválidas**, incluindo caracteres especiais e nomes de ficheiros comuns.
4. Não confie sempre que o que fornece nos formulários de entrada é o que pretendia! Utilize uma barra de endereços do browser ou uma ferramenta como o *Burpsuite*.
5. Procure erros ao introduzir dados inválidos para revelar o caminho atual da aplicação Web; se não houver erros, então a melhor opção poderá ser a tentativa e erro.
6. Compreender a **validação** da entrada e se existem **filtros**!
7. Tente **injetar** uma entrada válida para ler ficheiros sensíveis

# Remote File Inclusion - RFI
RFI é uma técnica para incluir ficheiros remotos numa aplicação vulnerável. Tal como a LFI, a RFI ocorre quando a entrada do utilizador não é corretamente higienizada, permitindo a um atacante injetar um URL externo na função de inclusão. Um requisito para a RFI é que a opção `allow_url_fopen` precisa estar `on.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5d617515c8cd8348d0b4e68f/room-content/b0c2659127d95a0b633e94bd00ed10e0.png)

