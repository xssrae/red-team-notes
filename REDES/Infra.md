---
tags:
  - REDES
---
# Funções do Host

Todos os ==computadores que estão conectados a uma rede são classificados como **hosts**==. Os hosts podem ser chamados de *dispositivos finais*. Alguns hosts também são chamados de *clientes*. No entanto, o termo hosts refere-se especificamente a ==dispositivos na rede que recebem um número para fins de comunicação==. Este número identifica o host dentro de uma rede específica. Este número é chamado de **endereço IP** (Internet Protocol). Um endereço IP identifica o host e a rede à qual o host está conectado.

![[Pasted image 20231030142327.png]]

Um exemplo de *software cliente* é um **navegador**, como Chrome ou FireFox. Um único computador pode também executar vários tipos de software cliente.

| Tipo    | Descrição                                                                                                                                                                                               |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| E-mail  | O servidor de executa o software do servidor de e-mail. Clientes usam cliente de e-mail software, como o Microsoft Outlook, para acessar o e-mail no servidor.                                          |
| Web     | O servidor web executa o software do servidor web. Os clientes usam software de navegador, como o Windows Internet Explorer, para acessar páginas da web no servidor.                                   |
| Arquivo | O servidor de arquivos armazena arquivos corporativos e de usuário em um local central. Os dispositivos clientes acessam esses arquivos com software cliente, como o Explorador de arquivos do Windows. |

## Ponto a ponto
Em *pequenas empresas* e em *casas*, muitos computadores ==funcionam como servidores e clientes na rede==. Esse tipo de rede é chamado de **rede ponto a ponto**.

![[Pasted image 20231030142548.png]]

#### As vantagens da rede ponto-a-ponto:
- Fácil de configurar
- Menos complexo
- Menor custo porque os dispositivos de rede e os servidores dedicados podem não ser necessários
- Pode ser usada para tarefas simples como transferir arquivos e compartilhar impressoras.
#### As desvantagens das rede ponto-a-ponto:
- Nenhuma administração centralizada
- Não é tão segura
- Não é escalável
- Todos os dispositivos podem atuar como clientes e servidores, podendo deixar seu desempenho lento.

## Dispositivos Finais
Os dispositivos de rede com os quais as pessoas estão mais *familiarizadas* são **dispositivos finais**. Para distinguir um dispositivo final de outro, cada dispositivo final em uma rede tem um **endereço**. Quando ==um dispositivo final inicia a comunicação, ele usa o endereço do dispositivo final de destino para especificar onde entregar a mensagem==.

## Dispositivos Intermediários
==**Dispositivos intermediários** *conectam* os dispositivos finais individuais à rede==. Eles podem conectar várias redes individuais para formar uma internetwork. Eles oferecem conectividade e asseguram que os dados fluam pela rede.

Esses dispositivos intermediários usam o **endereço do dispositivo final de destino**, em conjunto com as informações sobre as interconexões de rede, para determinar o caminho que as mensagens devem percorrer na rede.

![[Pasted image 20231030143247.png]]

Os dispositivos de rede intermediários executam algumas destas funções:

- **Regenerar** e **retransmitir** *sinais* de comunicação;
- **Manter informação** sobre *quais caminhos existem* pela rede e pela rede interconectada;
- **Notificar** outros dispositivos sobre *erros* e *falhas* de comunicação;
- **Direcionar** dados por *caminhos alternativos* quando houver falha em um link;
- **Classificar** e **direcionar** mensagens de acordo com as *prioridades*;
- **Permitir** ou negar o fluxo de dados, com base em *configurações de segurança*.

>**Observação:** Não mostrado é um hub Ethernet herdado. Um hub Ethernet também é conhecido como repetidor multiporta. Os repetidores regeneram e retransmitem sinais de comunicação. Observe que todos os dispositivos intermediários executam a função de um repetidor.

## Meios de rede
A comunicação transmite através de uma **rede na mídia**. A mídia fornece o canal pelo qual a mensagem viaja da origem ao destino.

As redes modernas usam principalmente três tipos de mídia para interconectar dispositivos, como mostrado na figura:

- **Fios de metal dentro de cabos** - Os dados são codificados em *impulsos elétricos*.
- **Fibras de vidro ou plástico nos cabos (cabo de fibra óptica)** - Os dados são codificados em *pulsos de luz*.
- **Transmissão sem fio** - Os dados são codificados através da modulação de frequências específicas de **ondas eletromagnéticas**.

![[Pasted image 20231030143611.png]]

**Critérios principais** para a escolha da mídia de rede:

- Qual é a **distância máxima** pela qual o meio físico consegue carregar um sinal com êxito?
- Qual é o **ambiente** em que a mídia será instalada?
- Qual é a **quantidade de dados** e a que **velocidade** deve ser transmitida?
- Qual é o **custo** do meio físico e da instalação?

# Representações e topologias de rede

==*Arquitetos* e *administradores* de rede devem ser capazes de mostrar como suas redes serão.== Eles precisam ser capazes de ver facilmente **quais componentes se conectam a outros componentes**, onde eles serão localizados e como eles serão conectados. 

![[Pasted image 20231030143941.png]]

Um diagrama fornece uma maneira fácil de entender como os dispositivos se conectam em uma rede grande. Esse tipo de “fotografia” de uma rede é conhecido como um **diagrama de topologia**. A capacidade de reconhecer as *representações lógicas* dos componentes físicos de rede é crucial para se permitir visualizar a organização e a operação de uma rede.

Além dessas representações, é utilizada **terminologia especializada** para descrever como cada um desses dispositivos e mídias se conectam:

- **Placa de interface de rede (NIC)** - Uma NIC *conecta fisicamente* o dispositivo final à rede.
- **Porta física** - Um *conector* ou *tomada* em um dispositivo de rede onde a mídia se conecta a um dispositivo final ou outro dispositivo de rede.
- **Interface** - *Portas especializadas* em um dispositivo de rede que se conectam a redes individuais. Como os ==roteadores conectam redes, as portas em um roteador são chamadas de interfaces de rede==.

## Diagramas de Topologia

- **Diagramas de topologia física**: Ilustram a *localização física* dos dispositivos intermediários e a *instalação dos cabos*. É possível ver que as salas em que esses dispositivos estão localizados estão rotuladas nesta topologia física.
- **Diagramas de topologia lógica**: Ilustram *dispositivos*, *portas* e o *esquema de endereçamento da rede*. É possível ver quais dispositivos finais estão conectados a quais dispositivos intermediários e que mídia está sendo usada.

# Tipos comuns de redes

## LANs e WANs
Os dois tipos mais comuns de infraestruturas de rede são as **redes locais (LANs)** e as redes de **longa distância (WANs)**. 

Uma **LAN** é uma infraestrutura de rede que ==fornece acesso a usuários e dispositivos finais em uma pequena área geográfica.== Normalmente, uma LAN é usada em um departamento dentro de uma empresa, uma casa ou uma rede de pequenas empresas.

- Interconectam dispositivos finais em uma **área limitada**, como uma casa, uma escola, um edifício de escritórios ou um campus.
- Uma LAN é geralmente administrada por **uma única organização ou pessoa**. O controle administrativo é imposto no nível da rede e governa as políticas de segurança e controle de acesso.
- As LANs fornecem largura de banda de **alta velocidade** para dispositivos finais internos e dispositivos intermediários, conforme mostrado na figura.

Uma **WAN** é uma infraestrutura de rede que ==fornece acesso a outras redes em uma ampla área geográfica==, que normalmente pertence e é gerenciada por uma corporação maior ou por um provedor de serviços de telecomunicações.

- **Interconectam as LANs** em *grandes áreas* geográficas, como entre cidades, estados, províncias, países ou continentes.
- As WANs são geralmente administradas por **vários prestadores** de serviço.
- As WANs geralmente fornecem links de velocidade **mais lenta** entre as LANs.

![[Pasted image 20231030150406.png]]

## A Internet
Coleção mundial de **redes interconectadas** (internetworks, ou internet para abreviar). A internet não é de propriedade de nenhum indivíduo ou grupo. Existem organizações que foram desenvolvidas para ajudar a manter a estrutura e a padronização de protocolos e processos da Internet. Essas organizações incluem a Internet Engineering Task Force (IETF), a Internet Corporation for Assigned Names and Numbers (ICANN) e a Internet Architecture Board (IAB), além de muitas outras.

## Intranets e Extranets

![[Pasted image 20231030150816.png]]

**Intranet** é uma **conexão privada** de LANs e WANs que pertence a uma *organização*. Uma intranet é projetada para ser acessada apenas por membros da organização, funcionários ou outras pessoas autorizadas.

Uma organização pode usar uma **extranet** para fornecer acesso seguro e protegido a indivíduos que trabalham para uma organização diferente, mas exigem acesso aos dados da organização. Aqui estão alguns exemplos de extranets:

- Uma **empresa** que fornece acesso a fornecedores e contratados externos;
- Um **hospital** que fornece um sistema de reservas aos médicos para que eles possam marcar consultas para seus pacientes;
- Um **escritório** local de educação que está fornecendo informações sobre orçamento e pessoal às escolas de seu distrito.

# Conexões com a Internet

## Tecnologias de Acesso à Internet
==**Usuários domésticos**, **trabalhadores remotos** e **pequenos escritórios** geralmente exigem uma conexão com um **ISP (Fornecedor de acesso à internet)** para acessar a Internet==. As opções de conexão variam muito entre os ISPs e as localizações geográficas. No entanto, as opções populares incluem *banda larga a cabo*, a banda larga via *digital subscriber line (DSL)*, *WANs sem fio* e serviços de *telefonia móvel celular*.

As **organizações** geralmente precisam acessar outros sites corporativos e a Internet. Conexões rápidas são necessárias para dar suporte a serviços comerciais que incluem telefones IP, videoconferência e armazenamento em data center. As controladoras oferecem *interconexões de nível empresarial*. Os serviços populares de nível empresarial *incluem DSL*, *linhas dedicadas* e *Metro Ethernet*.

## Conexões com a Internet para Residências e Pequenos Escritórios

![[Pasted image 20231030151940.png]]

- **Cabo** - Fornece *alta largura de banda*, *alta disponibilidade* e uma *conexão sempre ativa* à Internet.
- **DSL** - O DSL funciona utilizando a *linha telefônica*. Em geral, usuários de pequenos escritórios e escritórios domésticos se conectam com o uso de DSL Assimétrico (ADSL), o que significa que a velocidade de *download é maior que a de upload*.
- **Celular** - Usa uma *rede de telefonia celular* para se conectar. Onde quer que você possa obter um sinal de celular, você pode obter acesso à Internet por celular. O desempenho é *limitado pelos recursos do telefone e da torre de celular* à qual está conectado.
- **Satélite** - A disponibilidade do acesso à Internet via satélite é um benefício nas áreas que, de outra forma, não teriam conectividade com a Internet. As antenas parabólicas exigem uma *linha de visão clara para o satélite*.
- **Conexão Discada (Dial-up)** – Uma opção de *baixo custo* que usa qualquer linha telefônica e um modem. 

## Conexões Corporativas com a Internet
![[Pasted image 20231030152256.png]]

- **Linha Alugada Dedicada** - ==As linhas alugadas são *circuitos reservados* na rede do provedor de serviços== que conectam escritórios *geograficamente separados* para redes privadas de voz e / ou dados. Os circuitos são *alugados* a uma taxa mensal ou anual.
- **Metro Ethernet** - Isso às vezes é conhecido como Ethernet WAN e ethernet metropolitanas. *Estendem* a tecnologia de acesso à LAN na WAN.
- **DSL de negócios** - Disponível em vários formatos. Uma escolha popular é a *linha de assinante digital simétrica (SDSL)*, que é semelhante à versão DSL do consumidor, mas fornece uploads e downloads nas mesmas *velocidades altas*.
- **Satélite** - O serviço de satélite pode fornecer uma conexão quando uma solução com fio não está disponível.

## A Rede Convergente
**Redes Separadas Tradicionais**

Considere uma escola construída há trinta anos. Naquela época, algumas salas de aula eram cabeadas para a rede de dados, a rede telefônica e a rede de vídeo para televisões. ==Essas redes separadas não puderam se comunicar. Cada rede usava tecnologias diferentes para transmitir o sinal de comunicação. Cada rede possuía seu próprio conjunto de regras e padrões para assegurar a comunicação bem-sucedida.== *Vários serviços foram executados em várias redes*.

![[Pasted image 20231030153737.png]]

**Redes convergentes**

Hoje, as redes separadas de dados, telefone e vídeo convergem. ==Diferentemente das redes dedicadas, as redes convergentes são capazes de fornecer dados, voz e vídeo entre muitos tipos diferentes de dispositivos na mesma infraestrutura de rede.== Essa infraestrutura de rede usa o mesmo conjunto de regras, os mesmos contratos e normas de implementação. As redes de dados convergentes transportam *vários serviços em uma rede*.

![[Pasted image 20231030153757.png]]

# Redes confiáveis

## Tolerância a Falhas
Uma ==rede **tolerante a falhas** é aquela que *limita* o número de dispositivos afetados durante uma falha.== Ela foi desenvolvido para permitir uma *recuperação rápida* quando ocorre uma falha. Essas redes dependem de vários caminhos entre a origem e o destino de uma mensagem. ==Se um caminho falhar, as mensagens serão instantaneamente enviadas por um link diferente.== Ter vários caminhos para um destino é conhecido como redundância.

![[Pasted image 20231030154050.png]]

## Escalabilidade
Uma ==**rede escalável** se *expande rapidamente* para oferecer suporte a novos usuários e aplicativos==. Ele faz isso sem degradar o desempenho dos serviços que estão sendo acessados por usuários existentes. Essas redes são escaláveis porque os projetistas seguem padrões e protocolos aceitos.

![[Pasted image 20231030154115.png]]

## Qualidade do Serviço
A **qualidade do serviço (QoS)** é um requisito crescente das redes atualmente. Novos aplicativos disponíveis para usuários em redes, como transmissões de voz e vídeo ao vivo, criam expectativas mais altas em relação à qualidade dos serviços entregues.

==O congestionamento acontece quando a demanda por largura de banda excede a quantidade disponível. A *largura de banda* é medida pelo número de bits que podem ser transmitidos em um único segundo, ou bits por segundo (bps)==. Ao tentar uma comunicação simultânea pela rede, a demanda pela largura de banda pode exceder sua disponibilidade, criando um congestionamento na rede.

Quando o volume de tráfego é maior do que o que pode ser transportado pela rede, os dispositivos retêm os pacotes na memória até que os recursos estejam disponíveis para transmiti-los. Com uma política de QoS configurada, ==o roteador é capaz de gerenciar o fluxo do tráfego de voz e de dados, priorizando as comunicações por voz se a rede ficar congestionada.==

![[Pasted image 20231030154242.png]]

## Segurança da rede
A infraestrutura da rede, os serviços e os dados contidos nos dispositivos conectados à rede são recursos pessoais e comerciais críticos. Os administradores de rede devem abordar dois tipos de preocupações de segurança de rede: ==**segurança da infraestrutura de rede** e **segurança da informação**.==

Proteger a infraestrutura de rede inclui ==*proteger fisicamente* os dispositivos que fornecem conectividade de rede e *impedir o acesso não autorizado*== ao software de gerenciamento que reside neles, conforme mostrado na figura.

![[Pasted image 20231030154306.png]]

- **Confidencialidade** - Confidencialidade dos dados significa que apenas os destinatários pretendidos e autorizados podem acessar e ler dados.
- **Integridade** - A integridade dos dados garante aos usuários que as informações não foram alteradas na transmissão, da origem ao destino.
- **Disponibilidade** - A disponibilidade de dados garante aos usuários acesso oportuno e confiável aos serviços de dados para usuários autorizados.

# Tendências das redes

## Traga seu próprio dispositivo (BYOD)
O BYOD permite aos usuários finais a liberdade de usar ferramentas pessoais para acessar informações e se comunicar através de uma rede comercial ou do campus. Isso inclui laptops, notebooks, tablets, smartphones e e-readers.
## Colaboração On-line
A colaboração é definida como “ato de trabalho com outro ou outros em um projeto em parceria”. As ferramentas de colaboração, oferecem aos funcionários, alunos, professores, clientes e parceiros uma maneira de conectar, interagir e alcançar instantaneamente seus objetivos.
## Comunicações em vídeo
A videoconferência é uma ferramenta poderosa para se comunicar com outras pessoas, local e globalmente. O vídeo está se tornando um requisito fundamental para a colaboração efetiva à medida que as empresas se expandem pelos limites geográficos e culturais.
## Computação em nuvem
A computação em nuvem é uma das maneiras pelas quais *acessamos e armazenamos dados*. A computação em nuvem nos permite armazenar arquivos pessoais, até fazer backup de uma unidade inteira em servidores pela Internet. Aplicativos como processamento de texto e edição de fotos podem ser acessados usando a nuvem.

Para as empresas, a computação em nuvem amplia os recursos de TI sem exigir investimento em nova infraestrutura, treinamento de novas equipes ou licenciamento de novo software.

A computação em nuvem é possível devido aos **data centers**. Para segurança, confiabilidade e tolerância a falhas, os provedores de nuvem geralmente armazenam dados em *data centers distribuídos*. Em vez de armazenar todos os dados de uma pessoa ou uma organização em um data center, eles são armazenados em vários data centers em locais diferentes.

Existem quatro tipos principais de nuvens: *nuvens públicas*, *nuvens privadas*, *nuvens híbridas* e *nuvens da comunidade*.

| Tipo de nuvem           | Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nuvens públicas**     | Aplicativos e serviços baseados em nuvem oferecidos em uma nuvem pública são criados disponível para a população em geral. Os serviços podem ser gratuitos ou são oferecidos em um modelo de pagamento por uso, como pagar por armazenamento on-line. A nuvem pública usa a internet para fornecer serviços.                                                                                                                                                                                                                                                                                                                                                                                      |
| **Nuvens privadas**     | Os aplicativos e serviços baseados em nuvem oferecidos em uma nuvem privada são destinado a uma organização ou entidade específica, como um governo. A nuvem privada pode ser configurada usando o rede, embora isso possa ser caro para construir e manter. Uma nuvem privada também pode ser gerenciada por uma organização externa com acesso estrito segurança.                                                                                                                                                                                                                                                                                                                               |
| **Nuvens híbridas**     | Uma nuvem híbrida é composta de duas ou mais nuvens (exemplo: parte privada, parte pública), onde cada parte permanece um objeto distinto, mas ambos são conectado usando uma única arquitetura. Indivíduos em uma nuvem híbrida seria capaz de ter graus de acesso a vários serviços com base em direitos de acesso do usuário.                                                                                                                                                                                                                                                                                                                                                                  |
| **Nuvens comunitárias** | Uma nuvem de comunidade é criada para uso exclusivo por entidades ou organizações específicas. As diferenças entre nuvens públicas e nuvens da comunidade são as necessidades funcionais que foram personalizadas para a comunidade. Por exemplo, organizações de saúde devem manter a conformidade com políticas e leis (por exemplo, HIPAA) que exigem confidencialidade e autenticação especial. As nuvens comunitárias são usadas por várias organizações que têm necessidades e preocupações semelhantes. As nuvens comunitárias são semelhantes a um ambiente de nuvem pública, mas com níveis definidos de segurança, privacidade e até mesmo conformidade normativa de uma nuvem privada. |

## Tendências Tecnológicas em Casa
A tecnologia de casa inteligente se integra aos aparelhos diários, que podem ser conectados a outros dispositivos para tornar os aparelhos mais “inteligentes” ou automatizados. Atualmente, a tecnologia de casa inteligente está sendo desenvolvida para todos os cômodos de uma casa. A tecnologia doméstica inteligente se tornará mais comum à medida que as redes domésticas e a tecnologia de Internet de alta velocidade se expandirem.
## Rede Powerline
Usando um adaptador padrão powerline, os dispositivos podem se conectar à LAN onde quer que haja uma *tomada elétrica*. Nenhum cabo de dados precisa ser instalado, e há pouca ou nenhuma eletricidade adicional usada. Usando a mesma fiação que fornece a eletricidade, a rede powerline envia informações ao enviar dados em determinadas frequências.
## Banda Larga Sem Fio
- **Provedor de serviços de Internet sem fio**: *WISP* é um provedor de serviços de Internet que conecta assinantes a um ponto de acesso ou hot spot designado usando tecnologias sem fio semelhantes encontradas em redes locais sem fio domésticas (WLANs). Os WISPs são mais comumente encontrados em ambientes rurais onde DSL ou serviços a cabo não estão disponíveis.
- **Serviço de banda larga sem fio**: Outra solução sem fio para casas e pequenas empresas é a banda larga sem fio

# Segurança de Redes

## Ameaças à Segurança
==A **proteção de uma rede** envolve *protocolos*, *tecnologias*, *dispositivos*, *ferramentas* e *técnicas* para proteger dados e mitigar ameaças.== Vetores de ameaça podem ser *internos* ou *externos*. Hoje, muitas ameaças à segurança de rede externa se originam da Internet.

Existem várias ameaças externas comuns às redes:

- **Vírus, worms e cavalos de Tróia** - Eles contêm software ou código malicioso em execução no dispositivo do usuário.
- **Spyware e adware** - Estes são tipos de software que são instalados no dispositivo de um usuário. O software, em seguida, coleta secretamente informações sobre o usuário.
- **Ataques de dia zero** - Também chamados de ataques de hora zero, ocorrem no primeiro dia em que uma vulnerabilidade se torna conhecida.
- **Ataques de ator de ameaça** - Uma pessoa mal-intencionada ataca dispositivos de usuário ou recursos de rede.
- **Ataques de negação de serviço** - Esses ataques atrasam ou travam aplicativos e processos em um dispositivo de rede.
- **Interceptação de dados e roubo** - Esse ataque captura informações privadas da rede de uma organização.
- **Roubo de identidade** - Esse ataque rouba as credenciais de login de um usuário para acessar informações privadas.

Também é importante considerar **ameaças internas**. ==Há muitos estudos que mostram que as violações mais comuns ocorrem por causa de *usuários internos da rede*. Isso pode ser atribuído a dispositivos perdidos ou roubados, mau uso acidental por parte dos funcionários e, no ambiente comercial, até mesmo funcionários mal-intencionados.== Com as estratégias BYOD em evolução, os dados corporativos ficam muito mais vulneráveis. Portanto, ao desenvolver uma política de segurança, é importante abordar ameaças de segurança externas e internas.

![[Pasted image 20231030160647.png]]

## Soluções de Segurança
Nenhuma solução única pode proteger a rede da variedade de ameaças existentes. Por esse motivo, ==a segurança deve ser **implementada em várias camadas,** com uso de mais de uma solução. Se um componente de segurança falhar na identificação e proteção da rede, outros poderão ter êxito==.

Estes são os componentes básicos de segurança para uma rede doméstica ou de pequeno escritório:

- **Antivirus e antispyware** - Esses aplicativos ajudam a ==*proteger os dispositivos finais* contra a infecção por software malicioso==.
- **Filtragem por firewall** - A filtragem por ==**firewall** bloqueia o *acesso não autorizado* dentro e fora da rede.== Isso pode incluir um sistema de firewall baseado em host que impede o acesso não autorizado ao dispositivo final ou um serviço básico de filtragem no roteador doméstico para impedir o acesso não autorizado do mundo externo à rede.

Em contrapartida, a ==implementação de segurança para uma rede corporativa geralmente consiste em vários componentes incorporados à rede para *monitorar* e *filtrar o tráfego*.== Idealmente, todos os componentes trabalham juntos, o que minimiza a manutenção e melhora a segurança. Redes maiores e redes corporativas usam *antivírus*, *antispyware* e filtragem por *firewall*, mas também têm outros requisitos de segurança:

- **Sistemas de firewall dedicados** - Eles fornecem ==recursos de firewall mais avançados que podem filtrar grandes quantidades de tráfego com mais granularidade==.
- **Listas de controle de acesso (ACL)** - Eles filtram ainda mais o acesso e o encaminhamento de tráfego com base em endereços e aplicativos IP.
- **Sistemas de prevenção de intrusões (IPS)** - Identificam ameaças de rápida disseminação, como ataques de dia zero ou hora zero.
- **Redes privadas virtuais (VPN)** - fornecem acesso seguro a uma organização para trabalhadores remotos.

Os **requisitos de segurança de rede** devem considerar o *ambiente*, os vários *aplicativos* e os *requisitos de computação*. Ambientes domésticos e comerciais devem poder proteger seus dados e, ao mesmo tempo, permitir a qualidade do serviço que os usuários esperam de cada tecnologia. Além disso, as soluções de segurança implementadas devem ser adaptáveis às tendências de crescimento e variáveis da rede.

O estudo das ameaças à rede e de técnicas de mitigação é iniciado com um claro entendimento da infraestrutura de roteamento e de comutação usada para organizar serviços de rede.
