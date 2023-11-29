---
tags:
  - API
  - WEB
---

O reconhecimento de API passiva é a prática de **obter informações sobre um alvo sem interagir diretamente com seus sistemas**. Essa abordagem visa encontrar e documentar dados públicos relacionados à superfície de ataque do alvo. Geralmente, utiliza-se inteligência de código aberto (OSINT), que são dados coletados de fontes públicas. O objetivo é identificar endpoints de API, credenciais expostas, informações de versão, documentação da API e detalhes sobre o propósito comercial da API. Essas informações são valiosas para futuras fases de reconhecimento ativo.

Durante o reconhecimento passivo, podem ser descobertos dados sensíveis, como chaves de API, credenciais, JSON Web Tokens (JWT) e outros segredos, o que representa uma ameaça significativa. Descobertas de alto risco incluem exposição de informações pessoais (PII) ou dados confidenciais de usuários, como números de seguro social, nomes completos, endereços de e-mail e informações de cartão de crédito. Tais descobertas devem ser documentadas e relatadas imediatamente devido à sua gravidade.

Diversas técnicas de reconhecimento passivo podem ser aplicadas, como o uso de Google Dorking, Git Dorking, análise de repositórios de API, consulta à Way Back Machine e utilização do Shodan. Essas abordagens visam identificar informações relevantes sem a necessidade de interação direta com os sistemas do alvo.
## **Google Dorking

Mesmo sem quaisquer técnicas de Dorking, encontrar uma API como um usuário final pode ser tão fácil quanto uma pesquisa rápida.

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/3QiE3ZaXRLWKOYwRfCre_redditapisearch.png)

_Pesquisa do Google pela API do Reddit._

|   |   |
|---|---|
|**Consulta do Google Dorking**|**Resultados esperados**|
|inurl:"/wp-json/wp/v2/users|Encontra todos os diretórios de usuários de API WordPress disponíveis publicamente.|
|intitle:"index.of" intexto:"api.txt"|Localize arquivos de chave API disponíveis publicamente.|
|inurl:"/api/v1" intext:"índice de /"|Encontra diretórios de API potencialmente interessantes.|
|ext:php inurl:"api.php?action|Localize todos os sites com uma vulnerabilidade de injeção XenAPI SQL. (Esta consulta foi publicada em 2016; quatro anos depois, existem atualmente 141.000 resultados.)|
|intitle:"index of" api_key OR "api key" OR apiKey -pool|Esta é uma das minhas perguntas favoritas. Ele lista chaves de API potencialmente expostas.|

## Jogos de GitDorking

Independentemente de seu alvo realizar seu próprio desenvolvimento, vale a pena verificar o GitHub (www.github.com) para divulgação de informações confidenciais. Os desenvolvedores usam o GitHub para colaborar em projetos de software. Pesquisar o GitHub para OSINT pode revelar os recursos, a documentação e os segredos da API do seu alvo, como chaves de API, senhas e tokens, que podem ser úteis durante um ataque. Semelhante ao Google Dorking, com o GitHub, você pode especificar parâmetros como:

**Nome do arquivo** :swagger.json

**Extensão** : .json

Comece pesquisando no GitHub o nome da sua organização de destino emparelhado com tipos de informações potencialmente sensíveis, como “api key”, “api keys”, “apikey”, “autorização: Bearer”, “access_token”, “secret” ou “token”. Em seguida, investigue as várias guias de repositório do GitHub para descobrir endpoints de API e possíveis pontos fracos. Analise o código-fonte na guia Código, encontre bugs na guia Problemas e revise as alterações propostas na guia Solicitações de Pull.

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/vJHflsacRw6gsCDkbd2c_GithubExposed.png)

O código contém o código-fonte atual, arquivos readme e outros arquivos. Esta guia fornecerá o nome do último desenvolvedor que se comprometeu com o arquivo dado, quando esse commit aconteceu, os contribuidores e o código-fonte real.

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/Dn6kLSBGmQ2mI5S484Ao_GithubCode.png)

Usando a guia Código, você pode revisar o código em sua forma atual ou usar o ctrl -F para procurar termos que possam lhe interessar (como API, chave e segredo). Além disso, a visualização histórica se compromete com o código usando o botão Histórico encontrado perto do canto superior direito da imagem acima. Se você se deparou com um problema ou comentário que o levou a acreditar que houve uma vez que as vulnerabilidades associadas ao código, você pode procurar commits históricos para ver se as vulnerabilidades ainda são visíveis.

Ao olhar para um commit, use o botão Split para ver uma comparação lado a lado das versões do arquivo para encontrar o local exato onde uma alteração no código foi feita.![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/I7Zza4TSRgG0dQ5NFdQg_GithubHistory.png)O botão Split (à direita da imagem acima) permite que você separe o código anterior (à esquerda) e o código atualizado (direita). Aqui, você pode ver um commit com um aplicativo que removeu a chave da API do Google Maps do código, revelando a chave e o endpoint da API para o qual foi usada.

A guia Problemas é um espaço onde os desenvolvedores podem rastrear bugs, tarefas e solicitações de recursos. Se um problema estiver aberto, há uma boa chance de que a vulnerabilidade ainda esteja livre dentro do código (consulte a Figura 6-9).

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/S0xHhF3QWyPOOVFIewWQ_GithubIssue.png)

Este é um exemplo, de um problema aberto do GitHub que fornece a localização exata de uma chave de API exposta no código de um aplicativo. Se o problema for encerrado, anote a data do problema e pesquise o histórico de confirmação para quaisquer alterações nessa época.

A guia Solicitações Pull é um lugar que permite aos desenvolvedores colaborar em alterações no código. Se você revisar essas alterações propostas, às vezes poderá ter sorte e encontrar uma exposição de API que está em processo de resolução. Como essa alteração ainda não foi mesclada com o código, podemos ver facilmente que a chave da API ainda está exposta na guia Arquivos alterado. A guia Alterado Arquivos revela a seção de código que o desenvolvedor está tentando alterar.

Se você não encontrar pontos fracos em um repositório do GitHub, use-o para desenvolver o perfil do seu alvo. Tome nota das linguagens de programação em uso, informações de endpoint da API e documentação de uso, o que será útil para o futuro.

## TrufaHog (Ceral)

TruffleHog é uma ótima ferramenta para descobrir automaticamente segredos expostos. Você pode simplesmente usar a seguinte corrida Docker para iniciar uma varredura TruffleHog do Github do seu alvo.

$ sudo docker run -it -v "$PWD:/pwd" trufflesecurity/trufflehog: mais recente github --org-target-name

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/01s4gYuoQmq9GgdZg4oG_TruffleHogv3.png)

No exemplo acima, você pode ver que a opção alvo foi Venmo e os resultados da verificação indicam URLs que devem ser investigados para segredos potencialmente vazados. Além de pesquisar no Github, o TruffleHog também pode ser usado para procurar segredos em outras fontes como Git, Gitlab, Amazon S3, sistema de arquivos e Syslog. Para explorar essas outras opções, use a bandeira "-h". Para obter informações adicionais, confira [https://github.com/trufflesecurity/trufflehog](https://github.com/trufflesecurity/trufflehog).

# **Diretórios de API**

Programmableweb.com é uma fonte de informações relacionadas à API ([https://www.programmableweb.com/apis/directory](https://www.programmableweb.com/apis/directory)). Para saber mais sobre APIs, você pode usar sua API University. Para coletar informações sobre seu destino, use o Diretório de API, um banco de dados pesquisável de mais de 23.000 APIs. Espere encontrar endpoints de API, informações de versão, informações de lógica de negócios, o status da API, código-fonte, SDKs, artigos, documentação da API e um changelog.

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/Pl5zVW8Rde4fCFd32jz3_twilioapidirectory.png)

_Página da API Twilio em programmableweb.com._

Clique nas várias guias na lista de diretórios e observe as informações que você encontra. Para ver o local do ponto de extremidade da API, a localização do portal e o modelo de autenticação. Para ver informações sobre o histórico de versões das APIs, selecione uma versão específica listada na guia Versões. Nesse caso, os links de portal e de endpoint também levam à documentação da API. No caso do Twilio, você pode ver todas as especificações relacionadas à versão atual da API REST.

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/8Zn6Z9PIRse67JCxJz8s_twilioapidirectory2.png)

_A página de especificações Twilio em programmableweb.com._

Na página Especificações Twilio, você pode aprender todos os tipos de informações úteis sobre a API. Por exemplo, o URL de endpoint da API está listado, o fórum para a API, o URL de suporte do desenvolvedor, o modelo de autenticação e muito mais estão todos listados nesta página. Na parte inferior da página Especificações, você também pode ver artigos relacionados à API e aos desenvolvedores da API, o que pode ser útil ao atacar a API.

## **Shodan (suda)**

Shodan é o motor de busca para dispositivos acessíveis a partir da internet. O Shodan verifica regularmente todo o espaço de endereços IPv4 para sistemas com portas abertas e torna públicas as suas informações coletadas em https://shodan.io. Você pode usar o Shodan para descobrir APIs externas e obter informações sobre as portas abertas do seu destino, tornando-o útil se você tiver apenas um endereço IP ou o nome da organização para trabalhar. Como com os Google Dorks, você pode pesquisar o Shodan casualmente digitando o nome de domínio ou os endereços IP do seu alvo; alternativamente, você pode usar parâmetros de pesquisa como faria ao escrever consultas do Google. A tabela a seguir mostra algumas consultas úteis do Shodan.

|   |   |
|---|---|
|**Perguntas de Shodan**|**Propósito**|
|nome de host:"targetname.com"|Usar o hostname executará uma pesquisa Shodan básica para o nome de domínio do seu alvo. Isso deve ser combinado com as seguintes consultas para obter resultados específicos para o seu alvo.|
|"tipo conteúdo: aplicação/json"|As APIs devem ter seu tipo de conteúdo definido como JSON ou XML. Esta consulta irá filtrar os resultados que respondem com JSON.|
|"tipo de conteúdo: aplicação/xml"|Esta consulta irá filtrar os resultados que respondem com XML.|
|"200 OK" (desconto)|Você pode adicionar "200 OK" às suas consultas de pesquisa para obter resultados que tiveram solicitações bem-sucedidas. No entanto, se uma API não aceitar o formato da solicitação do Shodan, provavelmente emitirá uma resposta de 300 ou 400.|
|"wp-json" (tradução)|Isso irá procurar aplicações web usando a API do WordPress.|

# **A máquina do caminho**

O Wayback Machine é um arquivo de várias páginas da web ao longo do tempo. Isso é ótimo para o reconhecimento passivo da API porque isso permite que você confira as mudanças históricas no seu alvo. Se, por exemplo, o alvo uma vez anunciado uma API de parceiro em sua página de destino, mas agora o ocultar atrás de um portal autenticado, você poderá detectar essa alteração usando o Wayback Machine. Outro caso de uso seria ver as alterações na documentação da API existente. Se a API não tiver sido bem gerenciada ao longo do tempo, então há uma chance de que você possa encontrar endpoints aposentados que ainda existem, mesmo que o provedor da API acredite que eles sejam aposentados. São conhecidos como APIs Zombie. As APIs de zumbi se enquadram na vulnerabilidade do Gerenciamento de Ativos Improper na lista Top 10 da API OWASP. Encontrar e comparar snapshots históricos da documentação da API pode simplificar o teste para o Gerenciamento de Ativos Improper.

 ![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/FGPF2fPT8ysfQHtTHQbk_Wayback1.PNG)

Verifique se há diferenças entre a documentação da API. Mais tarde, quando você estiver testando ativamente a API, certifique-se de testar usando endpoints antigos,

## **Conclusão**

Neste módulo, abordamos algumas técnicas básicas que podem ser implantadas para reunir sobre a superfície de ataque da API do seu alvo. O primeiro passo para hackear as APIs de um alvo é descobrir o máximo de informações possível sobre elas. Usar essas técnicas de reconhecimento pode não apenas ajudá-lo a descobrir a existência de APIs, mas também pode levar a descobertas críticas de vulnerabilidade. Em seguida, vamos nos concentrar em técnicas de reconhecimento ativo.