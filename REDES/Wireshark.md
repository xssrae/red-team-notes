---
tags:
  - REDES
---
# Casos de uso

O **Wireshark** é uma das ferramentas de análise de tráfego mais potentes disponíveis no mercado. Há várias finalidades para seu uso:

- Detectar e solucionar problemas de rede, como pontos de falha e congestionamento da carga da rede.
- Detectar anomalias de segurança, como hosts desonestos, uso anormal de portas e tráfego suspeito.
- Investigar e aprender detalhes do protocolo, como códigos de resposta e dados de carga útil.

# GUI e dados

A **GUI** do Wireshark abre com uma única página tudo em um, que ajuda os usuários a investigar o tráfego de várias maneiras. À primeira vista, cinco seções se destacam.

|                                    |                                                                                                                                                                                                                                        |     |     |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --- | --- |
| **Toolbar**                        | A barra de ferramentas principal contém vários menus e atalhos para detecção e processamento de pacotes, incluindo filtragem, classificação, resumo, exportação e mesclagem.                                                           |     |     |
| **Exibir barra de filtro**         | A seção principal de consulta e filtragem                                                                                                                                                                                              |     |     |
| **Arquivos recentes**              | List of the recently investigated files. You can recall listed files with a double-click.                                                                                                                                              |     |     |
| **Filtro de captura e interfaces** | Filtros de captura e pontos de sniffing disponíveis (interfaces de rede).  A interface de rede é o ponto de conexão entre um computador e uma rede. A conexão de software (por exemplo, lo, eth0 e ens33) habilita o hardware de rede. |     |     |
|                                    |                                                                                                                                                                                                                                        |     |     |
|                                    |                                                                                                                                                                                                                                        |     |     |

![Wireshark - GUI](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/0a96b128d88d49f28e4b537b63bcfd3b.png)

## Carregando arquivos PCAP

A imagem acima mostra a interface vazia do Wireshark. A única informação disponível é o arquivo "http1.cap" processado recentemente. Vamos carregar esse arquivo e ver a apresentação detalhada dos pacotes do Wireshark. Observe que você também pode usar o menu "File" (Arquivo), arrastar e soltar o arquivo ou clicar duas vezes no arquivo para carregar um pcap

![Wireshark - load pcaps](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/409e59f9a93d6a027b0041b968aae7a4.png)  

Agora, podemos ver o nome do arquivo processado, o número detalhado de pacotes e os detalhes do pacote. Os detalhes do pacote são mostrados em três painéis diferentes, o que nos permite descobri-los em diferentes formatos. 


|   |   |
|---|---|
|Packet List Pane|Resumo de cada pacote (endereços de origem e destino, protocolo e informações do pacote). Você pode clicar na lista para escolher um pacote para investigação adicional. Depois que você selecionar um pacote, os detalhes serão exibidos nos outros painéis.
|Packet Details Pane|Análise detalhada do protocolo do pacote selecionado.|
|Packet Bytes Pane|Representação hexadecimal e ASCII decodificada do pacote selecionado. Ele destaca o campo do pacote dependendo da seção clicada no painel de detalhes.


## Packets Coloridos

O Wireshark tem dois tipos de métodos de coloração de pacotes: 
- **Regras temporárias** que só estão disponíveis durante uma sessão do programa e regras permanentes que são salvas no arquivo de preferências (perfil) e estão disponíveis para a próxima sessão do programa. Você pode usar o "**menu do botão direito do mouse**" ou o menu "**View --> Coloring Rules**" para criar regras de coloração permanentes. O menu "Colourise Packet List" ativa/desativa as regras de coloração. 
- A coloração temporária de pacotes é feita com o "menu do botão direito do mouse" ou com o menu "View --> Conversation Filter", que é abordado na TAREFA-5.
  

![Wireshark - packet colours](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/782c1d38f4502636cb2a8228e7675c9f.png)


## Detecção de tráfego

Você pode usar o "**botão tubarão**" azul para iniciar a detecção de rede (captura de tráfego), o botão vermelho interromperá a detecção e o botão verde reiniciará o processo de detecção. A barra de status também fornecerá a interface de detecção usada e o número de pacotes coletados.

![Wireshark - traffic sniffing](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/a9ccd9cd2acd72480a4674ca576a4a51.png)


## Mesclar arquivos PCAP

O Wireshark pode combinar dois arquivos pcap em um único arquivo. Você pode usar o caminho de menu "File --> Merge" (Arquivo --> Mesclar) para mesclar um pcap com o processado. Quando você escolher o segundo arquivo, o Wireshark mostrará o número total de pacotes no arquivo selecionado. Quando você clicar em "abrir", o arquivo pcap existente será mesclado com o arquivo escolhido e será criado um novo arquivo pcap. Observe que você precisa salvar o arquivo pcap "mesclado" antes de trabalhar nele.

![Wireshark - merge pcaps](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/bbc3f7938f8d3086953d5b0342422019.png)

## Exibir detalhes do arquivo

Conhecer os detalhes do arquivo é útil. Especialmente ao trabalhar com vários arquivos pcap, às vezes você precisará conhecer e lembrar os detalhes do arquivo (hash do arquivo, hora da captura, comentários do arquivo de captura, interface e estatísticas) para identificar o arquivo, classificá-lo e priorizá-lo. Você pode visualizar os detalhes seguindo "**Estatísticas --> Propriedades do arquivo de captura**" ou clicando no "**ícone pcap localizado na parte inferior esquerda**" da janela.

![Wireshark - file details](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/1ccc88dc2b66e935f2f382387ce3c0ec.png)

# Análise de Pacote

A dissecação de pacotes também é conhecida como dissecação de protocolo, que investiga os detalhes do pacote decodificando os protocolos e campos disponíveis. O Wireshark suporta uma longa lista de protocolos para dissecação, e você também pode escrever seus próprios scripts de dissecação. Você pode encontrar mais detalhes sobre dissecação [**aqui**](https://github.com/boundary/wireshark/blob/master/doc/README.dissector).

## Detalhes do Pacote

Você pode clicar em um pacote no painel da lista de pacotes para abrir seus detalhes (o clique duplo abrirá os detalhes em uma nova janela). Os pacotes **consistem em 5 a 7 camadas com base no modelo OSI**. Examinaremos todas elas em um pacote HTTP de uma captura de amostra. A imagem abaixo mostra a visualização do pacote número 27.

![Wireshark - packet details](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/a09f80da3fd63b32e47842d93ead7db5.png)

Cada vez que você clicar em um detalhe, ele destacará a parte correspondente no painel de bytes do pacote.

![Wireshark - packet bytes](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/31f45c8e0e06d874d3826752839270df.png)

Vamos ver mais de perto o painel de detalhes.

![Wireshark - packet details](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/22a21052465fedc91fc4d1ec3beb6bd6.png)

Podemos ver sete camadas distintas no pacote: quadro/pacote, origem [MAC], origem [IP], protocolo, erros de protocolo, protocolo de aplicativo e dados de aplicativo. A seguir, examinaremos as camadas em mais detalhes.

#### O quadro (camada 1): 
Isso mostrará qual quadro/pacote você está vendo e os detalhes específicos da **camada física** do modelo OSI.
![Wireshark - layer 1](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/9d23e2081fa68e7d6f602aa8b0d316d9.png)

#### Source MAC (Camada 2): 
Isso lhe mostrará os **endereços MAC** de origem e destino, da camada de **Data Link** do modelo OSI.

![Wireshark - layer 2](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/cd06b372ae6338348ff521afb4c7243f.png)

#### Source IP (Camada 3):
Isso lhe mostrará os **endereços IPv4** de origem e destino, da **camada de rede** do modelo OSI.
![Wireshark - layer 3](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/d71eb4efc8d48a968a3e078045bd1511.png)

#### Protocolo (Camada 4): 
Isso mostrará detalhes do protocolo usado **(UDP/TCP)** e das **portas de origem e destino**; da **camada de transporte** do modelo OSI.

![Wireshark - layer 4](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/c373f8492470524a8f01fded43856a27.png)

##### Erros de protocolo: 
Essa **continuação da 4ª camada** mostra segmentos específicos do **TCP** que precisaram ser **remontados**.

![Wireshark - protocol error](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/23bbe6ae6e8168cd0662998ff444b067.png)

#### Protocolo de aplicativo (camada 5): 
Mostrará detalhes específicos do protocolo usado, como **HTTP**, **FTP** e **SMB**. Da **camada de aplicativos** do modelo OSI.

![Wireshark - layer 5](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/879aea2816018d27769fc8490e4af51b.png)

##### Dados do aplicativo:
Essa extensão da 5ª camada pode mostrar os dados específicos do aplicativo.

![Wireshark - application data](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/c2d9c3ce498c6f9044413b68df287c14.png)

Essa é a maneira mais básica de filtrar o tráfego. Ao investigar um arquivo de captura, você pode clicar no campo que deseja filtrar e usar o "menu do botão direito do mouse" ou o menu "**Analisar --> Aplicar como filtro**" para filtrar o valor específico.
Observe que o **número total de pacotes** e os pacotes exibidos são sempre mostrados na barra de status.

![Wireshark - apply as filter](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/463abd0a5cad55831b54a37c17092505.png)

## Filtro de Conversação
Ao usar a opção "**Apply as a Filter"**, você filtrará apenas *uma única entidade do pacote*. Essa opção é uma boa maneira de investigar um valor específico nos pacotes. No entanto, suponha que você queira investigar um **número de pacote específico e todos os pacotes vinculados**, concentrando-se em endereços IP e números de porta. Nesse caso, a opção "**Conversation Filter**" o ajuda a visualizar somente os pacotes **relacionados** e a ocultar facilmente o restante dos pacotes. Você pode usar o "menu do botão direito do mouse" ou o menu "**Analyse --> Conversation Filter**" para filtrar as conversas.

![Wireshark - conversation filter](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/6b31a8581e560286aee74fb9a608dfc9.png)

## Conversação colorida

Essa opção **destaca os pacotes vinculados sem aplicar um filtro de exibição e diminuindo o número de pacotes visualizados**. Essa opção funciona com a opção "Regras de coloração" e altera as cores dos pacotes sem considerar a regra de cor aplicada anteriormente. 
Você pode usar o "menu do botão direito do mouse" ou o menu **"View --> Colourise Conversation**" para colorir um pacote vinculado com um único clique. Observe que você pode usar o menu "**View --> Colourise Conversation --> Colourisation Colourisation**" para desfazer essa operação.

![Wireshark - colourise conversation](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/b7a7ce6afa9c421e6bfaebac719d348c.png)


# Navegação

## Números do Pacote

O Wireshark **calcula o número de pacotes investigados** e atribui um **número exclusivo** para cada pacote. Isso ajuda o processo de análise de grandes capturas e facilita o retorno a um ponto específico de um evento.

![Wireshark - packet numbers](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/d52507e87088deb1597042d50900eef0.png)

## Ir para o pacote

Você pode usar o menu "**Go**" e a barra de ferramentas para visualizar pacotes específicos.

![Wireshark - go to packet](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/cdb1e1d12c63fc831c7d94db634bbe0d.png)

## Localizar pacotes

Além do número do pacote, o Wireshark pode **localizar pacotes pelo conteúdo**. Você pode usar o menu **Edit --> Find Packet** (Editar --> Localizar pacote) para fazer uma pesquisa dentro dos pacotes para um evento específico de interesse.

Há dois pontos cruciais na localização de pacotes:
	O primeiro é saber o **tipo de entrada**. Essa funcionalidade aceita quatro tipos de entrada (filtro de exibição, Hex, String e Regex). As pesquisas não diferenciam maiúsculas de minúsculas, mas você pode definir a diferenciação de maiúsculas e minúsculas na sua pesquisa clicando no botão de opção.

O segundo ponto é **escolher o campo de pesquisa**:
	Você pode realizar pesquisas nos três **painéis** (**lista de pacotes, detalhes de pacotes e bytes de pacotes**). Por exemplo, se você tentar encontrar as informações disponíveis no painel de detalhes do pacote e realizar a pesquisa no painel de lista de pacotes, o Wireshark não as encontrará, mesmo que elas existam.

![Wireshark - find packets](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/c8811df8ea0fa2b70fa90831d1ec9278.png)

## Marcar pacotes

Você pode usar o menu "**Editar**" ou **clicar com o botão direito do mouse** para marcar/desmarcar pacotes.

Os pacotes marcados serão mostrados em **preto**, independentemente da cor original que representa o tipo de conexão. Observe que as informações dos pacotes marcados são renovadas a cada sessão de arquivo, portanto, os pacotes marcados serão perdidos após o fechamento do arquivo de captura.

![Wireshark - mark packets](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/2c290f2f3c7b07223c86cd066751d19b.png)

## Comentar nos pacotes

Você pode adicionar comentários a determinados pacotes que ajudarão na investigação posterior ou lembrar e apontar pontos importantes/suspeitos para outros analistas de camada. Ao contrário da marcação de pacotes, os comentários podem permanecer no arquivo de captura até que o operador os remova.

![Wireshark - packet comments](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/844bedc49bdd7dcaf26861a9cd2658fd.png)


## Exportação de pacotes

Essa funcionalidade ajuda os analistas a compartilhar os únicos pacotes suspeitos (escopo decidido). Assim, informações redundantes não são incluídas no processo de análise. Você pode usar o menu "File" (Arquivo) para exportar pacotes.

![Wireshark - export packets](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/86daa70b6cb8b93cb11535787222fb26.png)


## Exportar objetos (arquivos)

O Wireshark pode extrair arquivos transferidos pela rede.  A exportação de objetos está disponível apenas para fluxos de protocolos selecionados (DICOM, HTTP, IMF, SMB e TFTP).

![Wireshark - export objects](https://tryhackme-images.s3.amazonaws.com/user-uploads/6131132af49360005df01ae3/room-content/16c22447c36bff2e415ea75a764854c8.png)



## Informação de Experts

O Wireshark também detecta **estados específicos** de protocolos para ajudar os analistas a identificar facilmente possíveis anomalias e problemas. Observe que essas são apenas sugestões, e sempre há uma chance de haver falsos positivos/negativos. As informações de especialistas podem fornecer um grupo de categorias em três gravidades diferentes. Os detalhes são mostrados na tabela abaixo.

|   |   |   |
|---|---|---|
|**Severity**|**Colour**|**Info**|
|**Chat**|**Azul**|Informações sobre o fluxo de trabalho usual.|
|**Note**|**Ciano**|Eventos notáveis, como códigos de erro de aplicativos.|
|**Warn**|**Amarelo**|Avisos como códigos de erro incomuns ou declarações de problemas.|
|**Error**|**Vermelho**|Problemas como pacotes malformados.|

Frequently encountered information groups are listed in the table below. You can refer to Wireshark's official documentation for more information on the expert information entries.

|   |   |   |   |
|---|---|---|---|
|**Group**|**Info**|**Group**|**Info**|
|**Checksum**|Checksum errors.|**Deprecated**|Deprecated protocol usage.|
|**Comment**|Packet comment detection.|**Malformed**|Malformed packet detection.|



