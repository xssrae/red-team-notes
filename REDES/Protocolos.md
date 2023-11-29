---
tags:
  - REDES
---
## Fundamentos das Comunicações
- **Fonte da Mensagem (remetente)** - As fontes da mensagem são pessoas ou dispositivos eletrônicos que precisam enviar uma mensagem para outras pessoas ou dispositivos.
- **Destino da mensagem (destinatário)** - O destino recebe a mensagem e a interpreta.
- **Canal** - consiste na mídia que fornece o caminho pelo qual a mensagem viaja da origem ao destino.
## Estabelecimento de Regras
Os protocolos devem ter em conta os seguintes requisitos para entregar com êxito uma mensagem compreendida pelo receptor:

- Um emissor e um receptor identificados;
- Língua e gramática comum;
- Velocidade e ritmo de transmissão;
- Requisitos de confirmação ou recepção.
## Requisitos de protocolo de rede
Os protocolos usados nas comunicações de rede compartilham muitas dessas características fundamentais. Além de identificar a origem e o destino, os protocolos de computadores e de redes definem os detalhes sobre como uma mensagem é transmitida por uma rede. Protocolos de computador comuns incluem os seguintes requisitos:

- Codificação de mensagens;
- Formatação e encapsulamento de mensagens;
- Tamanho da mensagem;
- Tempo da mensagem;
- Opções de envio de mensagem.

## Tamanho da Mensagem
As restrições de tamanho dos quadros exigem que o host origem divida uma mensagem longa em pedaços individuais que atendam aos requisitos de tamanho mínimo e máximo. A mensagem longa será enviada em quadros separados, e cada um contém uma parte da mensagem original. Cada quadro também terá suas próprias informações de endereço. No host destino, as partes individuais da mensagem são reconstruídas na mensagem original.
## Temporização de Mensagem

O tempo de mensagens também é muito importante nas comunicações de rede. A temporização da mensagem inclui o seguinte:

- **Controle de Fluxo -** Este é o processo de gerenciamento da taxa de transmissão de dados. O controle de fluxo define quanta informação pode ser enviada e a velocidade com que pode ser entregue. Por exemplo, se uma pessoa fala muito rapidamente, pode ser difícil para o receptor ouvir e entender a mensagem. Na comunicação de rede, existem protocolos de rede usados pelos dispositivos de origem e destino para negociar e gerenciar o fluxo de informações.
- **Tempo limite da resposta -** se uma pessoa fizer uma pergunta e não ouvir uma resposta dentro de um período de tempo aceitável, ela assume que nenhuma resposta está chegando e reage de acordo. A pessoa pode repetir a pergunta ou prosseguir com a conversa. Os hosts da rede usam protocolos de rede que especificam quanto tempo esperar pelas respostas e que ação executar se ocorrer um tempo limite de resposta.
- **Método de acesso -** determinar quando alguém pode enviar uma mensagem. Clique em Reproduzir na figura para ver uma animação de duas pessoas conversando ao mesmo tempo e, em seguida, ocorre uma "colisão de informações", e é necessário que as duas se afastem e iniciem novamente. Da mesma forma, quando um dispositivo deseja transmitir em uma LAN sem fio, é necessário que a placa de interface de rede (NIC) da WLAN determine se a mídia sem fio está disponível.

## Uma Nota Sobre o Ícone de Nó
![[Pasted image 20231101165347.png]]

# Protocolos

## Visão geral do protocolo de rede
|**Tipo de Protocolo**|**Descrição**|
|---|---|
|**Protocolos de comunicação em rede**|Os protocolos ==permitem que dois ou mais dispositivos se comuniquem através de um ou mais redes==. Protocolos como **IP**, **Transmission Control Protocol (TCP)**, **HyperText Protocolo de transferência (HTTP)** e muito mais.|
|**Protocolos de segurança de rede**|Protocolos ==protegem os dados para fornecer autenticação, integridade dos dados e criptografia de dados==. Esses protocolos seguros incluem o **Secure Shell (SSH)**, **SSL (Secure Sockets Layer)** e **TLS (Transport Layer Security)**.|
|**Protocolos de roteamento**|Protocolos permitem que os roteadores ==troquem informações de rota, compare caminho e, em seguida, selecionar o melhor caminho para o destino remota==. Incluem **Open Shortest Path First (OSPF)** e **Border Gateway Protocol (BGP)**.|
|**Protocolos de descoberta de serviço**|Protocolos são usados para a ==detecção automática de dispositivos ou serviços==. Exemplos de protocolos de detecção de serviços incluem **Host dinâmico Protocolo de Configuração (DHCP)** que detecta serviços para endereço IP alocação e **Sistema de Nomes de Domínio (DNS)** que é usado conversão de nome para endereço IP.|

## Funções de protocolo de rede
![[Pasted image 20231101165721.png]]

|**Função**|**Descrição**|
|---|---|
|**Endereçamento**|Identifica o remetente e o destinatário pretendido da mensagem usando um esquema de endereçamento definido. Exemplos de protocolos que fornecem incluem Ethernet, IPv4 e IPv6.|
|**Confiabilidade**|Esta função fornece mecanismos de entrega garantidos em caso de mensagens são perdidos ou corrompidos em trânsito. O TCP fornece entrega garantida.|
|**Controle de fluxo**|Esta função garante que os fluxos de dados a uma taxa eficiente entre dois dispositivos de comunicação. O TCP fornece serviços de controle de fluxo.|
|**Sequenciamento**|Esta função rotula exclusivamente cada segmento de dados transmitido. A usa as informações de sequenciamento para remontar o informações corretamente. Isso é útil se os segmentos de dados forem perdido, atrasada ou recebida fora de ordem. O TCP fornece serviços de sequenciamento.|
|**Detecção de erros**|Esta função é usada para determinar se os dados foram corrompidos durante transmissão. Vários protocolos que fornecem detecção de erros incluem Ethernet, IPv4, IPv6 e TCP.|
|**Interface de aplicação**|Esta função contém informações usadas para processo a processo comunicações entre aplicações de rede. Por exemplo, ao acessar uma página da Web, protocolos HTTP ou HTTPS são usados para se comunicar entre o processos da Web do cliente e do servidor.|

## Interação de Protocolos
- **Protocolo de transferência de hipertexto (HTTP) -** ==Este protocolo controla a maneira como um *servidor da web e um cliente da web interagem*. O HTTP define o conteúdo e formatação das solicitações e respostas trocadas entre o cliente e o servidor==. Tanto o software do cliente quanto o do servidor Web implementam HTTP como parte da aplicação. O HTTP conta com outros protocolos para reger o modo como as mensagens são transportadas entre cliente e servidor.
- **Transmission Control Protocol (TCP)** - ==Este protocolo gerencia as conversas individuais. A TCP é responsável por *garantir a entrega confiável* das informações e gerenciar o controle de fluxo entre os dispositivos finais.==
- **Protocolo Internet (IP) -** ==Este protocolo é responsável por *entregar mensagens* do remetente para o receptor==. IP é usado por roteadores para encaminhar como mensagens em várias redes.
- **Ethernet** - Este protocolo é ==responsável pela entrega de *mensagens de uma NIC para outra NIC* na mesma rede loca==l (LAN) Ethernet.

# Conjuntos de protocolos

## Evolução dos conjuntos de protocolos
![[Pasted image 20231101180040.png]]

## Suíte de Protocolos TCP/IP
![[Pasted image 20231101181136.png]]

**TCP/IP** é o conjunto de protocolos usado pela internet e as redes de hoje. O TCP/IP tem dois aspectos importantes para fornecedores e fabricantes:

- **Conjunto de protocolos de padrão aberto** - Isso significa que está *disponível gratuitamente* ao público e pode ser usado por qualquer fornecedor em seu hardware ou software.
- **Conjunto de protocolos com base em padrões** - isso significa que foi endossado pela indústria de rede e *aprovado por uma organização de padrões*. Isso garante que produtos de diferentes fabricantes possam interoperar com êxito.

---
#### Camada de aplicação
##### Sistema de nomes

- **DNS** - *Converte nomes de domínio*, como `cisco.com`, em *endereços IP*.
##### Configuração de hosts
- **DHCPv4** - Configuração de *Host Dinâmico para IPv4*. Um servidor DHCPv4 atribui dinamicamente informações de endereçamento IPv4 aos clientes DHCPv4 na inicialização e permite que os endereços sejam *reutilizados* quando não forem mais necessários.
- **DHCPv6** - Configuração do *Host Dinâmico para IPv6*. DHCPv6 é semelhante ao DHCPv4. Um servidor DHCPv6 *atribui dinamicamente* informações de endereçamento IPv6 aos clientes DHCPv6 na inicialização.
- **SLAAC** - Configuração automática de *endereço sem estado*. Um método que permite que um dispositivo obtenha suas informações de endereçamento IPv6 sem usar um servidor DHCPv6.
##### E-mail
- **SMTP** -Protocolo de *transferência de correio simples*. Permite que os clientes enviem e-mails para um servidor de e-mail e permite que os servidores enviem e-mails para outros servidores.
- **POP3** - Post Office Protocol versão 3. Permite que os clientes *recuperem e-mails* de um servidor de e-mail e *baixem o e-mail* para o aplicativo de e-mail local do cliente.
- **IMAP** - Protocolo de *Acesso à Mensagem na Internet*. Permite que os clientes acessem o e-mail armazenado em um servidor de e-mail e também mantenham o e-mail no servidor.
##### Transferência de arquivos
- **FTP** - Protocolo de *transferência de arquivos*. Define as regras que permitem que um usuário em um host acesse e transfira arquivos para e de outro host em uma rede. O FTP é um protocolo de *entrega de arquivos confiável*, orientado a conexão e reconhecido.
- **SFTP** - Protocolo de *transferência de arquivos SSH*. Como uma extensão do protocolo Secure Shell (SSH), o SFTP pode ser usado para estabelecer uma *sessão segura* de transferência de arquivos na qual a *transferência é criptografada*. SSH é um método para login remoto seguro que normalmente é usado para acessar a linha de comando de um dispositivo.
- **TFTP** - Protocolo de *Transferência de Arquivos Trivial*. Um protocolo de transferência de arquivos simples e sem conexão com entrega de arquivos não confirmada e de melhor esforço. Ele *usa menos sobrecarga* que o FTP.
##### Web e serviço Web
- **HTTP** - Protocolo de *transferência de hipertexto*. Um conjunto de regras para a troca de texto, imagens gráficas, som, vídeo e outros arquivos multimídia na World Wide Web.
- **HTTPS** - *HTTP seguro*. Uma forma segura de HTTP que criptografa os dados que são trocados pela World Wide Web.
- **REST** - *Representational State Transfer*. Um serviço Web que utiliza interfaces de programação de aplicações (APIs) e pedidos HTTP para criar aplicações Web.
#### Camada de transporte
##### Conexão orientada
- **TCP** - Protocolo de controle de transmissão. Permite a comunicação confiável entre processos executados em hosts separados e fornece transmissões confiáveis e reconhecidas que confirmam a entrega bem-sucedida.
##### Sem Conexão
- **UDP** - Protocolo de datagrama do usuário. Permite que um processo em execução em um host envie pacotes para um processo em execução em outro host. No entanto, o UDP não confirma a transmissão bem-sucedida do datagrama.
#### Camada de Internet
##### Protocolo IP (Internet Protocol)
- **IPv4** - Protocolo da Internet versão 4. Recebe segmentos de mensagem da camada de transporte, empacota mensagens em pacotes e endereça pacotes para entrega de ponta a ponta através de uma rede. O IPv4 usa um endereço de 32 bits.
- **IPv6** - IP versão 6. Semelhante ao IPv4, mas usa um endereço de 128 bits.
- **NAT** - Tradução de endereços de rede. Converte endereços IPv4 de uma rede privada em endereços IPv4 públicos globalmente exclusivos.
##### Mensagens
- **ICMPv4** - Protocolo de mensagens de controle da Internet para IPv4. Fornece feedback de um host de destino para um host de origem sobre erros na entrega de pacotes.
- **ICMPv6** - ICMP para IPv6. Funcionalidade semelhante ao ICMPv4, mas é usada para pacotes IPv6.
- **ICMPv6 ND** - descoberta de vizinho ICMPv6. Inclui quatro mensagens de protocolo que são usadas para resolução de endereço e detecção de endereço duplicado.
##### Protocolos de roteamento
- **OSPF** - Abrir o caminho mais curto primeiro. Protocolo de roteamento de estado de link que usa um experimento hierárquico baseado em áreas. OSPF é um protocolo de roteamento interno padrão aberto.
- **EIGRP** - Protocolo de roteamento de gateway interno aprimorado. Um protocolo de roteamento de padrão aberto desenvolvido pela Cisco que usa uma métrica composta com base na largura de banda, atraso, carga e confiabilidade.
- **BGP** - Protocolo de gateway de fronteira. Um protocolo de roteamento de gateway externo padrão aberto usado entre os Internet Service Providers (ISPs). O BGP também é comumente usado entre os ISPs e seus grandes clientes particulares para trocar informações de roteamento.
#### Camada de acesso à rede
##### Resolução de endereços
- **ARP** - Protocolo de Resolução de Endereço. Fornece mapeamento de endereço dinâmico entre um endereço IPv4 e um endereço de hardware.
    **Observação**: Você pode ver outro estado de documentação que o ARP opera na Camada da Internet (Camada OSI 3). No entanto, neste curso, afirmamos que o ARP opera na camada de Acesso à Rede (OSI Camada 2) porque seu objetivo principal é descobrir o endereço MAC do destino. Um endereço MAC é um endereço da camada 2.
##### Protocolos de link de dados
- **Ethernet** - define as regras para os padrões de fiação e sinalização da camada de acesso à rede.
- **WLAN** - Rede local sem fio. Define as regras para sinalização sem fio nas frequências de rádio de 2,4 GHz e 5 GHz.

# Modelos de Referência

## O Modelo OSI
|**Camada de modelo OSI**|**Descrição**|
|---|---|
|**7 - Aplicação**|A camada de aplicação contém protocolos usados para processo a processo comunicações.|
|**6 - Apresentação**|A camada de apresentação fornece uma representação comum dos dados transferidos entre serviços de camada de aplicativo.|
|**5 - Sessão**|A camada de sessão fornece serviços para a camada de apresentação para organizar seu diálogo e gerenciar o intercâmbio de dados.|
|**4 - Transporte**|A camada de transporte define serviços para segmentar, transferir e remontar os dados para comunicações individuais entre o fim dispositivos.|
|**3 - Rede**|A camada de rede fornece serviços para trocar as partes individuais de dados através da rede entre dispositivos finais identificados.|
|**2 - Enlace de dados**|Os protocolos da camada de enlace descrevem métodos para troca de dados quadros entre dispositivos em uma mídia comum|
|**1 - Físico**|Os protocolos da camada física descrevem o mecânico, elétrico, meios funcionais e processuais para ativar, manter e desativar conexões físicas para uma transmissão de bits de e para uma rede dispositivo.|

## Comparação de modelos OSI e TCP / IP
![[Pasted image 20231101183133.png]]

- ==**A Camada OSI 3**, a camada de rede, é mapeada diretamente para a camada de **Internet TCP / IP**==. Essa camada é usada para descrever os protocolos que endereçam e encaminham mensagens em uma rede interconectada.
- ==**A Camada OSI 4**, a camada de transporte, mapeia diretamente para a camada de **Transporte TCP / IP**==. Essa camada descreve os serviços e as funções gerais que fornecem uma entrega ordenada e confiável de dados entre os hosts origem e destino.
- ==**A camada de aplicativos TCP / IP** inclui vários protocolos que fornecem funcionalidade específica para uma variedade de aplicativos do usuário final. **As camadas 5, 6 e 7== do modelo OSI** são usadas como referências para desenvolvedores e fornecedores de software de aplicação para produzir aplicações que operam em redes.
- Ambos os modelos TCP/IP e OSI são usados geralmente para referenciar protocolos em várias camadas. Como o modelo OSI separa a camada de enlace de dados da camada física, geralmente é usado para referenciar as camadas inferiores.

# Encapsulamento de dados

## Segmentando Mensagens
Uma melhor abordagem é *dividir* os dados em pedaços menores e mais gerenciáveis para o envio pela rede. **Segmentação** é o ==processo de *dividir um fluxo de dados em unidades menores* para transmissões através da rede==.

- **Aumenta a velocidade** - Como um fluxo de dados grande é segmentado em pacotes, grandes quantidades de dados podem ser enviadas pela rede sem amarrar um link de comunicação. Isso permite que muitas conversas diferentes sejam intercaladas na rede chamada multiplexação.
- **Aumenta a eficiência** -Se um único segmento não conseguir alcançar seu destino devido a uma falha na rede ou no congestionamento da rede, somente esse segmento precisa ser retransmitido em vez de reenviar todo o fluxo de dados.

## Sequenciamento
Nas comunicações em rede, cada segmento da mensagem deve passar por um processo semelhante para garantir que ==chegue ao destino correto e possa ser remontado no conteúdo da mensagem original==, conforme mostrado na figura. O TCP é responsável por sequenciar os segmentos individuais.

## Unidades de Dados de Protocolo
- **Dados** - o termo genérico para a PDU usada na camada de aplicação;
- **Segmento** - PDU da camada de transporte;
- **Pacote** - PDU da camada de rede;
- **Quadro** - PDU da camada de enlace de dados
- **Bits** - PDU da camada física usada ao transmitir dados fisicamente pela mídia.

# Acesso a dados

## Endereços
==As camadas de **rede** e de **enlace de dados** são responsáveis por entregar os dados do dispositivo origem para o dispositivo destino==. Conforme mostrado na figura, os protocolos nas duas camadas contêm um endereço de origem e de destino, mas seus endereços têm finalidades diferentes:

- **Endereços de origem e destino da camada de rede** - Responsável por *entregar o pacote IP da origem original ao destino final*, que pode estar na mesma rede ou em uma rede remota.
- **Endereços de origem e destino da camada de enlace de dados** - Responsável por *fornecer o quadro de enlace de dados* de uma placa de interface de rede (NIC) para outra NIC na mesma rede.

![[Pasted image 20231101184224.png]]

## Endereço Lógico da Camada 3
Um **==endereço IP** é o *endereço lógico* da camada de rede==, ou camada 3, usado para entregar o pacote IP da origem original ao destino final.

O pacote IP contém dois endereços IP:

- **Endereço IP de origem** 
- **Endereço IP de destino** 

Um endereço IP contém duas partes:

- **Parte da rede** - A parte mais à esquerda do endereço que indica a ==*rede* na qual o endereço IP é um membro==. Todos os dispositivos na mesma rede terão a mesma parte da rede no endereço.
- **Parte do host** - A parte ==restante do endereço que identifica um *dispositivo específico* na rede==. Essa parte é exclusiva para cada dispositivo ou interface na rede.

**Observação**: A máscara de sub-rede (IPv4) ou comprimento do prefixo (IPv6) é usada para ==identificar a parte da rede de um endereço IP da parte do host==.

![[Pasted image 20231101184511.png]]

## Endereços de Enlace de Dados
O endereço físico da Camada 2 do link de dados tem uma função diferente.

A Camada 2, o protocolo de enlace de dados só é usado para entregar o pacote de NIC para NIC na mesma rede. O roteador remove as informações da Camada 2 conforme é recebido na NIC e adiciona novas informações de enlace de dados antes de encaminhar a NIC de saída em seu caminho para o destino final.

O pacote IP é encapsulado em um quadro de link de dados que contém as seguintes informações de link de dados:

- **Endereço de link de dados de origem** - O endereço físico da NIC que está enviando o quadro de link de dados.
- **Endereço de link de dados de destino** - O endereço físico da NIC que está recebendo o quadro de link de dados. Esse endereço é o roteador do próximo salto ou o endereço do dispositivo de destino final.