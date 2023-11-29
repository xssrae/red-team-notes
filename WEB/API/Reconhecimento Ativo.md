## **Reconnaissance da API Ativo**

O reconhecimento ativo envolve a interação direta com o alvo, predominantemente por meio de digitalização. Nesse processo, a busca por APIs e informações relevantes é priorizada. Durante a digitalização, ocorre a enumeração de portas abertas, identificação de serviços utilizando HTTP e investigação de aplicativos da Web hospedados nos sistemas encontrados. A exploração aprofundada pode revelar APIs anunciadas para usuários finais, exigindo a análise detalhada do aplicativo da Web em busca de diretórios relacionados à API. Ferramentas como nmap, OWASP Amass, gobuster, kiterunner e DevTools são utilizadas nesse processo.

O Nmap, em particular, é uma ferramenta essencial, capaz de verificar portas, identificar vulnerabilidades, enumerar serviços e encontrar hosts ativos. No contexto da descoberta de API, são recomendadas duas verificações específicas: detecção geral, que utiliza scripts padrão e enumeração de serviço, e varredura de todas as portas. A saída dessas verificações pode ser salva em vários formatos para revisão posterior, como XML, Nmap, greppable ou uma combinação de todos esses formatos.

```shell
$  nmap -sC -sV
```


A verificação de todas as portas do Nmap verificará rapidamente todas as 65.535 portas TCP para executar serviços, versões de aplicativos e sistema operacional host em uso:

```shell
$  nmap -p-
```

Assim que a varredura de detecção geral começar a retornar os resultados, avante a varredura de todas as portas. Em seguida, comece sua análise prática dos resultados. Depois de descobrir um servidor web, você pode executar a enumeração HTTP usando um script Nmap NSE (use -p para especificar quais portas você gostaria de testar).
```shell
$ nmap -sV --script=http-enum <target> -p 80,443,8000,8080
```

**OWASP Amass**

OWASP Amass é uma ferramenta de linha de comando que pode mapear a rede externa de um alvo coletando OSINT de mais de 55 fontes diferentes. Você pode criá-lo para realizar varreduras passivas ou ativas. Se você escolher a opção ativa, a Amass coletará informações diretamente do destino solicitando suas informações de certificado. Caso contrário, ele coleta dados de mecanismos de pesquisa (como Google, Bing e HackerOne), fontes de certificado SSL (como GoogleCT, Censys e FacebookCT), APIs de pesquisa (como Shodan, AlienVault, Cloudflare e GitHub) e o arquivo da web Wayback.
### Aproveitando ao máximo o Amass com as chaves da API

Antes de mergulhar no uso do Amass, devemos aproveitar ao máximo adicionando chaves de API a ele. Vamos obter algumas chaves de API gratuitas para melhorar nossas varreduras Amass.

Primeiro, podemos ver quais fontes de dados estão disponíveis para Amass (pago e gratuito) executando:  

```shell
$ amass enum -list  
```

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/eex0psZsSx2Zyd9ekGIl_ActiveDiscovery1.PNG)

Em seguida, precisaremos criar um arquivo de configuração para adicionar nossas chaves de API.
```shell
$ sudo curl https://raw.githubusercontent.com/OWASP/Amass/master/examples/config.ini >~/.config/amass/config.ini
```

Agora podemos atualizar o config.ini. Eu vou demonstrar o processo para adicionar chaves API com Censys. Basta visitar [https://censys.](https://censys.io/register)io/registre-se e inscrever-se para uma conta gratuita. Certifique-se de usar um e-mail válido, porque você terá que verificar o acesso à sua conta gratuita.

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/ZMWysMVxSPp9CREpENjU_ActiveDiscovery2.PNG)

Depois de obter seu ID de API e Secret, edite o arquivo config.ini e adicione as credenciais ao arquivo.

```shell
$ sudo nano ~/.config/amass/config.ini
```


![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/XYQwwA4JTwWOF7CH0d3T_ActiveDiscovery3.PNG)

Além disso, como com qualquer credencial, certifique-se de não compartilhá-los como eu fiz. Se você os compartilhou, basta usar o botão "Redefinir minha API Secret" de volta no Censys.io. Você pode repetir esse processo com muitas contas gratuitas e chaves de API, então você fará o OWASP Amass em uma potência para o reconhecimento de API.

```shell
$ amass enum -active -d target-name.com |grep api

legacy-api.target-nome.com (es)

api1-backup.target-nome.com

api3-backup.target-nome.com
```

Essa varredura pode revelar muitos subdomínios exclusivos da API, incluindo  legacy-api.target-name.com. Um endpoint de API chamado  legado  pode ser de particular interesse porque parece indicar uma vulnerabilidade inadequada de gerenciamento de ativos.

O Amass tem várias opções úteis de linha de comando. Use o   comando de inteligência para coletar certificados SSL, pesquisar registros Whois reverso e encontrar IDs ASN associados ao seu destino. Comece fornecendo o comando com endereços IP de destino

```shell
$  amass intel -addr
```

Se esta verificação for bem sucedida, fornecerá nomes de domínio. Esses domínios podem então ser passados para  a informação  com a   opção para realizar uma olhada Whois reversa:

```shell
$  amass intel -d
```

Isso pode lhe dar uma tonelada de resultados. Concentre-se nos resultados interessantes que se relacionam com sua organização alvo. Depois de ter uma lista de domínios interessantes, atualize para o   subcomando do enum para começar a enumerar os subdomínios. Se você especificar a   opção , o Amass abster-se-á de interagir diretamente com o seu alvo:

```shell
$  amass enum -passive -d
```

A   varredura enum ativa realizará grande parte da mesma digitalização que a passiva, mas adicionará a resolução do nome de domínio, tentará transferências de zona DNS e obterá informações de certificado SSL:
```shell
$  amass enum -active -d
```

Para aumentar o seu jogo, adicione a   opção -brute para subdomínios de força bruta,  -w  para especificar a lista de palavras API_superlist e, em seguida, a  opção para enviar a saída para o diretório de sua escolha:
```shell
$  amass enum -active -brute -w /usr/share/wordlists/API_superlist -d [alvo domain]
```
## **Diretório Força bruta com Gobuster**

O exemplo a seguir usa uma lista de palavras específica da API para encontrar os diretórios em um endereço IP:

```shell
$  gobuster dir -u target-name.com :8000 -w /home/hapihahacker/api/wordlists/common_apis_160
```

Depois   de encontrar diretórios de API como o diretório /api mostrado nesta saída, seja por rastreamento ou força bruta, você pode usar Burp para investigá-los mais. Gobuster tem opções adicionais, e você pode listá-los usando a   opção

```shell
$  gobuster dir -h - não é compatível
```


Se você quiser ignorar certos códigos de status de resposta, use a opção  -b. Se você gostaria de ver códigos de status adicionais, use  -x. Você pode melhorar uma pesquisa de Gobuster com o seguinte:


$  gobuster dir -u ://targetaddress/ -w /usr/share/wordlists/api_list/common_apis_160 -x 200,202,301 -b 302

O Gobuster fornece uma maneira rápida de enumerar URLs ativos que encontram caminhos de API.
## **Kiterunner de corridas**

Kiterunner é uma excelente ferramenta que foi desenvolvida e lançada pela Assetnote. Atualmente, o Kiterunner é a melhor ferramenta disponível para descobrir endpoints e recursos da API. Embora ferramentas de força bruta de diretório como Gobuster/Dirbuster/ trabalhem para descobrir caminhos de URL, ela normalmente depende de solicitações padrão de GET HTTP. O Kiterunner não apenas usará todos os métodos de solicitação HTTP comuns com APIs (GET, POST, PUT e DELETE), mas também imitará estruturas comuns de caminho de API. Em outras palavras, em vez de solicitar  GET /api/v1/user/create, o Kiterunner tentará  POST /api/v1/user/create, imitando uma solicitação mais realista.

Você pode executar uma verificação rápida do URL ou endereço IP do seu alvo como este:

$  kr scan HTTP://127.0.0.1

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/nXzTsPZ8R6C79ghxe2DO_ActiveDiscovery10.PNG)

Como você pode ver, Kiterunner irá fornecer-lhe uma lista de caminhos interessantes. O fato de o servidor estar respondendo exclusivamente a solicitações para determinados   caminhos /api/ indica que a API existe.

Observe que realizamos essa varredura sem nenhum cabeçalho de autorização, o que a API de destino provavelmente requer. Vou demonstrar como usar o Kiterunner com cabeçalhos de autorização no  Capítulo 7.

Se você quiser usar uma lista de texto em vez de um arquivo ., use a   opção com o arquivo de texto de sua escolha:

```shell
$  kr brute ?target?
```

Se você tiver muitos destinos, poderá salvar uma lista de destinos separados por linha como um arquivo de texto e usar esse arquivo como destino. Você pode usar qualquer um dos seguintes formatos de URI separados por linha como entrada:

Test.com (com)

Test2.com:: 443

http://test3.com (com)

http://test4.com (com)

http://test5.com:8888/api

Um dos recursos mais legais do Kiterunner é a capacidade de repetir solicitações. Assim, você não só terá um resultado interessante para investigar, você também será capaz de dissecar exatamente por que esse pedido é interessante. Para reproduzir uma solicitação, copie toda a linha de conteúdo para o Kiterunner, cole-a usando a   opção de replay kb e inclua a lista de texto que você usou:

```shell
$  kr kb replay "GET 414 [ 183, 7, 8]://192.168.50.35:8888/api/privatizações/count 0cf6841b1e7ac8badc6e237ab300a90ca873d571" -w :/api/palavras de palavras/da-data/kiterunner/routes-large.kite
```

Executar isso irá reproduzir a solicitação e fornecer a resposta HTTP. Você pode então rever o conteúdo para ver se há algo digno de investigação. Eu normalmente reviso resultados interessantes e, em seguida, pivo para testá-los usando o Postman e o Burp Suite.

## **DevTools em**

O DevTools contém algumas ferramentas de hacking de aplicativos da Web altamente subestimadas. As etapas a seguir ajudarão você a filtrar de forma fácil e sistemática milhares de linhas de código para encontrar informações confidenciais em fontes de página. Comece abrindo sua página de destino e, em seguida, abra o DevTools com F12 ou  ctr - shift - I. Ajuste a janela DevTools até ter espaço suficiente para trabalhar. Selecione a guia Rede e atualize a página (CTRL+r).

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/KAIntko1RBud1q6MVwBQ_ActiveDiscovery5.PNG)

Você pode usar a ferramenta de filtro para procurar qualquer termo que você gostaria, como "API", "v1" ou "grafo". Esta é uma maneira rápida de encontrar endpoints de API em uso. Você também pode deixar a guia Devtools Network aberta enquanto executa ações na página da Web. Por exemplo, vamos verificar o que acontece se deixarmos os DevTools abertos enquanto autenticamos ao crAPI. Você deve ver um novo pedido aparecer. Neste ponto, você pode mergulhar mais fundo na solicitação clicando com o botão direito em um dos pedidos e selecionando "Editar e Reenviar".

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/JHIANpvkSDONA1eM3T0S_ActiveDiscovery7.PNG)

Isso permitirá que você verifique a solicitação no navegador, edite os cabeçalhos / órgão de solicitação e envie-a de volta para o provedor da API. Embora este seja um ótimo recurso DevTools, você pode querer entrar em um navegador que foi destinado a interagir com APIs. Você pode usar o DevTools para migrar solicitações individuais para o Postman usando o cURL.

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/dKkYPAvmRTM4i4y825GQ_ActiveDiscovery7-5.PNG)

Depois de copiar a solicitação desejada, abra o Postman. Selecione Importar e clique na guia "Raw text". Cole no pedido do cURL e selecione importação.

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/NPybx1iQaeK63RN9bsTz_ActiveDiscovery8.PNG)

Uma vez que o pedido tenha sido importado, ele terá todos os cabeçalhos necessários e o corpo de solicitação necessários para fazer solicitações adicionais no Postman. Esta é uma ótima maneira de interagir rapidamente com uma API e interagir com uma única solicitação de API. Para criar automaticamente uma coleção de pós-homem mais completa, confira o próximo módulo que está na engenharia reversa de uma API.

O reconhecimento é extremamente importante ao testar APIs. Descobrir endpoints de API é um primeiro passo necessário ao atacar APIs. O bom reconhecimento também tem o benefício adicional de potencialmente fornecer as chaves do castelo na forma de chaves de API, senhas, tokens e outras divulgações de informações úteis.