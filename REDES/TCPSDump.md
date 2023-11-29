---
tags:
  - REDES
---
O **TCPdump** é uma ferramenta de linha de comando que, como Wireshark , pode ser usada para capturar tráfego de rede e exibir e analisar arquivos de captura PCAP. O **TCPDUmp** tem o benefício de não precisar de acesso de GUI a um host para usá-lo — esta propriedade é muito útil quando você tem acesso remoto à shell, por exemplo, durante um teste de penetração, e precisa ter uma ideia do tráfego de rede. Além disso, de algumas maneiras, o TCPDUmp fornece recursos de filtragem e análise ainda mais granulares, com a capacidade de ter a saída canalizada para outros comandos.

Você pode ver as opções disponíveis com `tcpdump -h` ou ler o manual com `man tcpdump`.

Você pode instalar o TCPDUmp através do gerenciador de pacotes do seu sistema operacional ou pode usar **o clone git** no repositório do Github em [https://github.com/the-tcpdump-group/tcpdump](https://github.com/the-tcpdump-group/tcpdump). 

Tenha em atenção que **terá de anexar `sudo` antes de cada comando TCPDUmp se não for o utilizador root**!

# Capturando tráfego em tempo real
A maioria dos recursos de captura em Wireshark também estão disponíveis no TCPDump. 

- **Especificar um alvo** para a captura aplicando a filtragem do trafego e salvando em um arquivo `.pcap`. Para começar, aplique o comando `tcpdump`.

- Para **exibir a lista de interfaces disponíveis** nas quais o TCPdump pode capturar tráfego: `tcpdump -D`. 
- Para iniciar a captura em uma **interface específica**, use a _interface_ `tcpdump -i`, por exemplo, `tcpdump -i en0`.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/59efd45bfcf5d678d65edbb79750ee0822a27dec229037f08d89184e4b112cc60f8413dbdb85638a5ef0882a33af.png)

- **Aplicar filtros** por host de origem ou destino:
 `tcpdump src _ip-address_` ou `tcpdump dst _ip-address_`.

- **Filtrar por porta**:
	`tcpdump dst port 25`

- **Filtrar por protocolo**:
 `tcpdump ftp`
 
- **Operadores lógicos**, como **e** & **ou** podem ser usados para termos em cadeia. Por último, para fazer com que o TCPDUmp saia depois de capturar _x_ número de pacotes
   use `-c`.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/858912eb30af5a56513980784a4ba007266465db840a64193ea6b4c5898fbc7590c28ff8afb8fadf7c0ae4a19b08.png)

Às vezes, ter endereços e portas resolvidos para nomes pode ser irritante se você estiver processando o arquivo de captura através de um script ou de uma série de comandos — para desativá-lo, use a opção `-n`. Por fim, você pode salvar sua captura em um arquivo PCAP com o _nome de arquivo_ `-w`

# Analisando PCAPs

Você pode obter uma filtragem de pacotes de nível com TCPdump ao ler e analisar arquivos PCAP. Para ler um arquivo de captura salvo com as configurações padrão, use o _nome de arquivo_ `tcpdump -r`. Para uma saída mais verbosa, as opções `-v`, `-vv` ou `-vvv` podem ser usadas, com cada uma aumentando em verbosidade.

  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/361860e5c27f379a72ef65b537b37b5d71672caa41f5edc61ecbcc8c86199f0f2c78f1534c964fe8b652f78819aa.png)

 - Na 1º linha de cada pacote TCP, as **informações do cabeçalho IP são exibidas**, incluindo o **TTL**, **sinalizadores**, **protocolo de camada 4**, **comprimento e deslocamento de fragmentação**. 
 - Na 2º linha de cada pacote TCP, você pode ver o **endereço IP de origem e a porta**, o **endereço IP de destino e a porta**, **o sinalizador TCP** (**S = SYN,  P= PSH,  F= FIN, R = RST, U = URG e A for = ACK**), soma de verificação, números de sequência e confirmação, tamanho da janela, quaisquer opções e comprimento do cabeçalho.

#### aplicar filtros: 
especificando campos e valores específicos no cabeçalho do pacote. Algumas das mais úteis incluem:

— **Especificando sinalizadores TCP**:  
Para fazer a correspondência de todos os pacotes com um único sinalizador TCP especificado, adicione a opção tcp [tcpflags] == tcp-ack /tcp-syn/tcp-fin/tcp-push/**tcp-urg**/**tcp-rst**. 

Por exemplo, `tcp [tcpflags] == tcp-push` exibe pacotes com apenas o sinalizador PSH definido.

Para fazer a correspondência de pacotes com vários sinalizadores TCP, você deve primeiro calcular o valor decimal da seção do sinalizador do cabeçalho TCP. As 8 bandeiras são ordenadas como mostrado abaixo.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/44865c4cda2679047739c6b38873318a7725280d53ec383568cb1af73cd76bb332585273ec900832494e079c6614.png)

Se desejar fazer a correspondência de pacotes com vários bits sinalizadores ativados, converta os sinalizadores em um valor decimal e use esse número em `tcp [tcpflags] == x.` Por exemplo, para pacotes com os sinalizadores PSH e ACK definidos, o valor decimal torna-se 00011000 = 24 e a expressão se torna `tcp [tcpflags] == 24`, como mostrado abaixo.

  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/76579d1b8bc82200e86097e500d8c42b4e453a0a27600c76c40de1ec9aa643bd07e27b959344ad122d9e1fe71c81.png)

— **Especificação dos bytes do cabeçalho do pacote**:  
Você pode especificar qualquer byte no cabeçalho do pacote usando seu índice.

`icmp [0] == 8`. O mesmo se aplica a outros cabeçalhos e valores de protocolo, como `ip [8]` para o TTL.

Observe que, às vezes, você pode substituir o índice de bytes pelo nome do campo que está especificando. Por exemplo, `icmp [0]` poderia ser substituído por `icmp [icmptype]`.

Existem muitos outros recursos úteis no TCPdump, tais como:

- `-A` para exibir o conteúdo do pacote em ASCII
- `-x` para imprimir o despejo de cânhamo do pacote
- `-X` para imprimir ambos os itens acima e
- `t`, `-tt`, `-ttt`, `-tttt`, `-ttttt` para gerenciar carimbos de data/hora


#### outros comandos do shell:
— **corte -d “**_delimitador_**” -f** _não._ : **cut** é uma ferramenta útil que pode extrair determinados campos dentro de cada linha com o uso de delimitadores. Os delimitadores são caracteres únicos que separam cada campo, podendo cada campo ser especificado com um número.

  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/b086e121714f475a605eadc26642ab6c9160d40f9b7fac9bf663dd725ec3abe677b0b850ae43c4895f7d589c1e7c.png)

Podemos usar o símbolo 'maior que' como nosso delimitador e especificar o 1º campo a ser exibido com o `corte -d “>” -f 1`.

Você pode especificar mais de um campo a ser exibido, como `corte -d “:” -f 1,2,3` para imprimir até o endereço de destino e a porta.

— **awk '{impressão $** _não._ **} '**: O **awk** é uma ferramenta muito poderosa no que toca à manipulação de texto e um caso de uso é imprimir um campo específico dentro de cada linha. Cada campo é separado por espaços.

  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/ced919b9da3093354cce6b3ba8b1f0327d77b41f205453dafe613b14d72b436e74b583eb8d8ed841c22b072ecccf.png)

#### extração de um único campo em todos os pacotes:
`awk`. 

Pode também utilizar `$NF` para o último campo e `$ (NF-x)` para o _(x+1)_ th field do final, tal como `awk '{print $ (NF-2)}'` para o terceiro último campo.

— **grep** _palavra-chave_:  `grep` é o comando go-to para encontrar linhas dentro de **arquivos que correspondem a uma determinada palavra-chave**. Por exemplo, para localizar todos os pacotes FTP relacionados a um arquivo .zip, você pode usar `grep zip`, como mostrado abaixo.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/64a88e8a20305bf85f48a6dd43a2970f2d217e622f031b09f8dcaad5dffb923af07e0246353c42d1fd4c5ca072ed.png)

