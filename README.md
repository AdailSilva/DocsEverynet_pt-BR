## Documentação Everynet
#### Tradução: AdailSilva
##### E-mail: adail101@hotmail.com

> ##### Para contratar Brokers:
[https://iotopenlabs.io/home/catalogo-de-solucoes/conectividade-lorawan/#](https://iotopenlabs.io/home/catalogo-de-solucoes/conectividade-lorawan/# "https://iotopenlabs.io/home/catalogo-de-solucoes/conectividade-lorawan/#")

> ##### Plataforma para Testes On-Line:
[https://jsfiddle.net/](https://jsfiddle.net/ "https://jsfiddle.net/")

### Introdução à plataforma Everynet

A plataforma Everynet foi projetada para operar em grande escala e, portanto, separa a funcionalidade do Network Server (NS) do gerenciamento da Radio Access Network (RAN).

Todos os recursos da plataforma são totalmente extensíveis via API, conforme descrito nesta documentação, e portais de gerenciamento convenientes estão disponíveis com base nessas APIs.

> O portal NS está disponível em: ns.us.everynet.io  (Network Server)

> O portal RAN está disponível em: ran.us.everynet.io  (Radio Access Network)

> O portal NS está disponível em: ns.eu.everynet.io  (Network Server)

> O portal RAN está disponível em: ran.eu.everynet.io  (Radio Access Network)

> O portal NS está disponível em: ns.atc.everynet.io (Network Server)

> O portal RAN está disponível em: ran.atc.everynet.io (Radio Access Network)

Onde .us/.eu/.atc especifica as instâncias americana, européia e brasileira compartilhada respectivamente. Outras regiões e outras instâncias privadas estão disponíveis.

Para poder gerenciar convenientemente um número muito alto de objetos (dispositivos, filtros, conexões, usuários, chaves), os portais e os servidores subjacentes incluem amplos recursos de pesquisa e filtro. Os filtros fornecem um mecanismo poderoso para rotear dados entre conjuntos de dispositivos e conexões com servidores de aplicativos externos. Ao filtrar tags, EUIs, gateways e tipos de mensagens, é possível estabelecer relacionamentos complexos entre dispositivos e aplicativos, até mesmo compartilhar dados de um dispositivo para vários aplicativos.

### Começo rápido

##### Convite para o NS

Os novos usuários da plataforma Everynet Network Server (NS) receberão um convite por email para o portal. Na primeira entrada, o portal solicitará que o usuário defina uma senha e faça login.

O NS é composto por 'Organizações' e o escopo de visão limitado a objetos pertencentes a essa organização. A Everynet iniciará o primeiro usuário em uma nova organização e, posteriormente, poderá adicionar e gerenciar outros usuários através do portal.

[![E-mail de convite](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/01.png "E-mail de convite")](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/01.png "E-mail de convite")

#### Layout do portal

O Everynet NS e o portal foram projetados para serem escalonados para muitos milhões de dispositivos e usuários, o que rapidamente se tornaria complicado para navegar por grupos e listas simples. Para superar isso, todos os objetos no servidor podem receber várias tags para facilitar a pesquisa.

O escopo de visão para qualquer usuário é definido por sua organização. A organização contém todas as suas tags, dispositivos, filtros, conexões, usuários e chaves.


#### Visão principal

A visualização padrão do portal Everynet NS é mostrada abaixo.

O campo de pesquisa fornece um mecanismo conveniente para descobrir rapidamente grupos de dispositivos no servidor. No exemplo mostrado aqui, uma seleção de dispositivos que foram marcados com 'teste' foram listados à esquerda da tela. As principais informações de cada dispositivo estão visíveis na lista de blocos.

###### Os dispositivos podem ser pesquisados usando:

- dev_eui
- dev_addr
- dev_class
- tags
- app_eui
- activation
- encryption
- org

Quando um dispositivo é selecionado (no exemplo, mostra onde o dispositivo é destacado), seus detalhes completos podem ser visualizados e os atributos modificados no painel direito da tela. Cada um desses atributos é mapeado para as APIs do desenvolvedor.

[![Tela inteira de dispositivos](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/02.jpg "Tela inteira de dispositivos")](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/02.jpg "Tela inteira de dispositivos")

#### Criar um dispositivo

Na visualização "Dispositivos", clique no ícone.

Os EUIs, endereços e chaves necessários podem ser preenchidos dependendo das opções para o tipo de ativação e se a criptografia do payload é finalizada na rede ou no servidor de aplicativos. Os valores EUI/addr/keys fornecidos pelo usuário podem ser inseridos ou preenchidos automaticamente.

É possível atribuir várias tags a cada dispositivo para facilitar as pesquisas subsequentes.

[![Criar dispositivo](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/03.jpg "Criar dispositivo")](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/03.jpg "Criar dispositivo")

#### Criar um filtro

Na visualização "Filtro", clique no ícone.

Os filtros fornecem um mecanismo para formar grupos de dispositivos. Esses grupos podem ser formados filtrando tags, EUIs ou gateway e tipo de mensagem.

[![Criar filtro](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/04.jpg "Criar filtro")](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/04.jpg "Criar filtro")

#### Criar uma conexão

Na visualização 'Conexão', clique no ícone.

O Everynet NS fornece conectividade de dispositivo, mas as soluções completas dependem de integrações com servidores de aplicativos externos de terceiros para fazer uso dos dados fornecidos. Esse recurso fornece as 'Conexões' para essas integrações externas.

Muitos servidores de aplicativos externos usam integrações HTTP ou MQTT padrão do setor, e a lista de conexões específicas (MyDevices, PubNub etc.) continuará a crescer.

Como cada conexão possui propriedades exclusivas, a lista de parâmetros muda de acordo com a seleção.

[![Criar conexão](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/04.jpg "Criar conexão")](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/04.jpg "Criar conexão")

### Introdução a API Everynet

O Everynet Network Server (NS) expõe duas interfaces diferentes: RESTful e WebSocket. Essas interfaces foram projetadas para os seguintes propósitos:

1. **API de gerenciamento de servidor** - API RESTFul para gerenciamento de contas, provisionamento de dispositivos, configuração de servidor, filtro, chaves, provisionamento de usuários, etc.

2. **API de fluxo de dados** - API baseada no WebSocket para transmitir mensagens e depurar dados entre o NS e o Application Server (AS).

3. **Adaptadores** - Ponte entre o NS e serviços de terceiros, como: MQTT, PubNub, HTTP, etc...

4. **Exemplos** - Os exemplos do Application Server (AS) implementados para diferentes APIs.

### API de gerenciamento

#### Motivação

A API de gerenciamento é uma interface RESTful projetada para provisionar dispositivos para o servidor de rede. Além de dispositivos, permite filtrar o fluxo de mensagens provenientes da API de dados criando filtros. Também permite criar e conectar adaptadores aos serviços de IoT de terceiros: PubNub, AWS MQTT, MyDevices, MQTT, Hub IoT do Azure, etc.

#### URLs de terminal

A Everynet está operando em diferentes regiões e redes privadas, incluindo regiões gerais da UE, dos EUA e do Brasil. Cada região usa seu próprio URL de terminal.

Regiões personalizadas e redes privadas podem obter os URLs dos terminais Everynet.

> https://ns.eu.everynet.io/api/v1.0 - Região europeia.

> https://ns.us.everynet.io/api/v1.0 - Região dos Estados Unidos.

> https://ns.atc.everynet.io/api/v1.0 - Região brasileira.

A seção "Experimente" está em construção e não está funcionando.

#### Recursos

A API de gerenciamento expõe os seguintes endpoints:

- **Users** - Operações CRUD para usuários do NS. As permissões podem ser atribuídas a cada usuário para limitar as informações e a disponibilidade de ações para os usuários.

- **Keys** - Operações CRUD para chaves da API NS. As chaves são usadas para autenticar clientes na API de dados e na API de gerenciamento. As permissões também podem ser atribuídas a cada chave, para que seja possível limitar o fluxo de dados da API de dados para cada chave única.

- **Permissions** - Projetadas para restringir permissões para diferentes usuários e chaves. Por exemplo, o Join Server deve ter acesso às mensagens de ingresso, mas não tem acesso às mensagens de dados comuns.

- **Devices** - Provisionamento e cancelamento de provisionamento de dispositivos.

- **Bands** - Gerenciamento de bandas regionais, cada banda inclui informações detalhadas sobre parâmetros de rádio e constantes de temporização (atraso) que são usadas para transmitir mensagens do NS para os Dispositivos.

- **Filters** - Operações CRUD para os filtros. Os filtros são projetados para filtrar o fluxo de mensagens do dispositivo por aplicativos, gateways, tags, dispositivos e tipos de mensagens. Todos os parâmetros são sequências separadas por vírgula.

Você deve fazer o seguinte para usar um filtro:

1. Crie um filtro usando a API ou a GUI de gerenciamento e memorize filter_id.

2. Estabeleça uma conexão da API de dados usando uma string de consulta com o parâmetro filter e o valor filter_id, em que filter_id é um identificador de filtro memorizado na primeira etapa.

- Conexões - operação CRUD para as conexões entre o NS e as plataformas IoT de terceiros: MyDevices, AWS MQTT, PubNub ou qualquer servidor HTTP.

#### Exemplo - Pegar Usuários com o utilitário cUrl:

> curl -X GET "https://ns.atc.everynet.io/api/v1.0/users?access_token=SEU_TOKEN" -H "accept: application/json"

> Todos os exemplos de requisições a seguir foram construídos e testados nos softwares cURL e Postman.

- **User v1.0**
Os usuários são usados para delegar o controle sobre determinados dispositivos para determinadas pessoas. Esta página descreve as operações CRUD aplicadas aos usuários e o processo de autenticação/autorização do usuário.

> POST
/users
Adicionar usuário ao servidor de rede

> GET
/users
Obter lista de usuários do servidor de rede

> PATCH
/users/{id}
Atualizar dados do usuário

> DELETE
/users/{id}
Excluir usuário do servidor de rede

> POST
/auth
Autorização

> GET
/logout
Sair

- **Key v1.0**
As chaves são necessárias para autorizar o uso da API. Esta página descreve as operações CRUD aplicadas às chaves.

> POST
/keys
Criar chave

> GET
/keys
Obter lista de chaves

> GET
/keys/{id}
Recuperar chave por identificador de chave

> PATCH
/keys/{id}
Atualizar uma chave

> DELETE
/keys/{id}
Deletar uma chave

- **Device v1.0**
Endpoint Devices é usado para executar o gerenciamento de dispositivos.

> POST
/devices
Criar dispositivo

> GET
/devices
Obter listar de dispositivos

> GET
/devices/{dev_eui}
Obter lista de dispositivos por dev_eui

> PATCH
/devices/{dev_eui}
Atualizar dispositivo

> DELETE
/devices/{dev_eui}
Deletar dispositivo

- **Band v1.0**
Gerenciamento de bandas de frequência regional. Cada banda inclui informações detalhadas sobre parâmetros de rádio e configurações de temporização (atraso) que são usadas para transmitir mensagens do NS para dispositivos, etc.

> GET
/bands
Obter lista de bandas

> GET
/bands/{bandName}
Obter banda pelo nome

- **Filter v1.0**
Operações CRUD para os filtros. Os filtros são projetados para filtrar o fluxo de mensagens do dispositivo por aplicativos, gateways, tags, dispositivos e tipos de mensagens. Todos os parâmetros são sequências separadas por vírgula. Você deve fazer o seguinte para usar um filtro...

1. Crie um filtro usando a API ou a GUI de gerenciamento e memorize filter_id.

2. Estabeleça uma conexão da API de dados usando uma string de consulta com o parâmetro filter e o valor filter_id, em que filter_id é um identificador de filtro memorizado na primeira etapa.

> POST
/filters
Criar um filtro

> GET
/filters
Obter uma lista de filtros

> GET
/filters/{id}
Obter um filtro pelo id

> PATCH
/filters/{id}
Atualzar um filtro

> DELETE
/filters/{id}
Deletar um filtro

- **Connection v1.0**
Operação CRUD para Conexões entre NS e plataformas IoT de terceiros, como MyDevices, AWS MQTT, PubNub ou qualquer servidor HTTP.

> GET
/connections
Obter uma lista de conexões

> GET
/connections/{id}
Obter uma conexão pelo id

> DELETE
/connections/{id}
Deletar uma conexão

### API de dados

#### Motivação

**API de dados** - É uma interface de streaming bidirecional baseada em WebSockets e projetada para troca de mensagens entre o Network Server (NS) e o Application Server (AS) no modo em tempo real. Todas as operações específicas do LoRaWAN, como a ativação do OTAA, também são realizadas usando essa interface.

API de dados projetada como uma interface em tempo real e não fornece armazenamento persistente de mensagens, armazenamento de estado do dispositivo e assim por diante. Em outras palavras, é uma interface de streaming pura entre o AS e o NS.

A API de dados é baseada em WebSocket, que permite desenvolver aplicativos sem servidor e amplamente utilizados em diferentes linguagens de programação.

#### URLs de terminal

A Everynet está operando em diferentes regiões e redes privadas, incluindo regiões gerais da UE, dos EUA e do Brasil. Cada região usa seu próprio URL de terminal.

Regiões personalizadas e redes privadas podem obter os URLs dos terminais Everynet.

> wss://ns.eu.everynet.io/api/v1.0/data - região europeia.

> wss://ns.us.everynet.io/api/v1.0/data - região dos Estados Unidos.

> wss://ns.atc.everynet.io/api/v1.0/data - região brasileira.

#### Localizações do servidor

LoRaWAN é um protocolo de comunicação síncrona e em tempo real. Isso significa que o tempo geral de processamento da mensagem é limitado pelo valor padrão de um segundo. Inclui todos os tempos de ping, processamento no NS e AS e assim por diante. Infelizmente, o buffer de downlink no lado NS abre uma enorme falha de segurança em um protocolo e essa é a razão pela qual a Everynet não está armazenando em buffer as mensagens de downlink. Isso leva a uma situação em que o tempo de ping entre o AS e o NS se torna crítico. Verifique se o seu AS está localizado na mesma região que o NS.

#### Recursos

A interface da API de dados fornece os seguintes recursos:

- Conexão bidirecional contínua para recebimento e envio de mensagens em tempo real e evita a busca NS constante para novas mensagens

- Recepção de mensagens no formato JSON. Todas as versões compatíveis com LoRaWAN são suportadas: confirmadas/não confirmadas, uplinks, solicitações de junção, comandos MAC. Todos os metadados também podem ser fornecidos: parâmetros de RF, duplicadas e assim por diante...

- A transmissão de mensagens de downlink, incluindo comandos MAC, é realizada da maneira ideal. Os seguintes parâmetros são otimizados: capacidade de downlink da rede, melhor perda de canal de RF, melhores chances de alcançar o gateway no tempo (tempo de ping).

- Recebimento de mensagens de serviço/depuração do NS: como erros de MIC ou manipulação incorreta do contador.

- Filtragem de mensagens baseada em servidor: por identificador de dispositivo, gateway, tag de dispositivo, aplicativo,...

- A compatibilidade com versões anteriores é obtida usando o sistema de controle de versão da mensagem.

### Começando

1. Instale o cliente ant WebSocket, por exemplo, wscat:

> npm install -g wscat

2. Gere chave de API de dados na GUI do NS. Temos essa chave:

> SEU_TOKEN

3. Use este URL para se conectar à API de dados:

> wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN

Usando o wscat, você pode se conectar ao fluxo da API de dados:

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN"

4. Conexão estabelecida! :-)

### Conexão

A conexão à API de dados é realizada através do WebSocket.

Observe que o protocolo Websocket implementa as chamadas mensagens PING/PONG para manter Websockets ativos [https://tools.ietf.org/html/rfc6455#section-5.5.2\], mesmo atrás de proxies, firewalls e balanceadores de carga. O servidor de rede envia uma mensagem PONG ao cliente a cada 25 segundos. Esta mensagem não requer uma resposta. O recebimento desta mensagem indica que a conexão está ativa. Para verificar a conexão, o cliente pode enviar uma mensagem PING, em resposta, NS, envie uma mensagem PONG.

É possível especificar os seguintes parâmetros na string de consulta da solicitação:

 - **access_token** - Este é um campo obrigatório usado para autenticar a solicitação de conexão. Esse token pode ser gerado usando a API de gerenciamento ou a GUI do servidor de rede em uma guia Chaves. Este é o único campo obrigatório que você precisa especificar para estabelecer uma conexão.

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN"

 - **lora=1** - Permite que a conexão receba não apenas dados do aplicativo, mas também todos os comandos MAC gerados pelo servidor de rede. Os comandos MAC serão incluídos nas mensagens de uplink e downlink. O valor padrão é 0.

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&lora=1"

 - **radio=1** - Force o NS a incluir metadados de rádio em cada mensagem de uplink. O valor padrão é 0 (sem metadados de rádio).

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&radio=1"

 - **duplicate=1** - Force o NS a transmitir todas as duplicadas da mensagem de uplink de todos os gateways que foram capazes de receber uma mensagem. O valor padrão é 0: nenhuma duplicata será entregue ao AS.

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&duplicates=1"

 - **last_messages=** - Recupera até N últimas mensagens históricas. O valor máximo é 1000.

Apenas os 5 últimos jsons:

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&last_messages=5"

 - **from_unixtime** - Recupere mensagens históricas de um momento específico. Formato de carimbo de data e hora Unix.

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&last_messages=[1234567890]"

 - **types** - Diz ao NS para filtrar as mensagens de acordo com a lista de tipos de mensagens. Aceita uma lista separada por vírgula de tipos de mensagens. Por exemplo, se for necessário receber apenas mensagens de uplink e join_request, você deve usar: types=uplink,join_request. O valor padrão é: types=uplink,downlink,downlink_request,join_request,status_response.

###### Tipos:
> uplink, downlink_request, downlink_response, downlink, join_request, join_response, status_request, status_response, downlink_claim, error, warning e info.

> -- Observação, valores não permitidos: downlink_response, join_response e status_request.

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&types=uplink,downlink_request,downlink,join_request,status_response,downlink_claim,error,warning,info"

 - **gateways** - Informa ao NS que você deseja receber mensagens se elas receberem apenas por lista fechada de gateways. Aceita uma lista separada por vírgula de identificadores de gateway. Por padrão, esta opção está desativada (aceita dados de qualquer gateway).

##### EUI de cada gateway separado por vígula

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&gateways=b0fd0b7002700000,b0fd0b7003540000,b0fd0b7003800000,b0fd0b7003850000,b0fd0b70046e0000,b0fd0b7005440000,b0fd0b7005790000,b0fd0b70072c0000"

 - **applications** - Informa ao NS que você deseja receber mensagens se elas receberem apenas pela lista fechada de aplicativos (APP_EUI_). _Aceita uma lista separada por vírgula de identificadores APP_EUI. Por padrão, esta opção está desativada (aceita dados de qualquer aplicativo).

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&applications=3bc8d41c49ab4a96,2bfe1a9ed185c1eb,56f7dac775f3ba57"

 - **devices** - Informa ao NS que você deseja receber mensagens se elas receberem apenas pela lista fechada de dispositivos (dev_eui). Aceita uma lista separada por vírgula de identificadores de dispositivo. Por padrão, esta opção está desativada (aceita dados de qualquer dispositivo).

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&devices=0012f80000000xxx,0012f80000000xxx"

 - **tags** - Informa ao NS que você deseja receber mensagens se elas receberem apenas por lista fechada de tags. Aceita uma lista separada por vírgula de dtags. Por padrão, esta opção está desativada (aceita dados do dispositivo com qualquer tag).

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&tags=test,otaa,adailsilva,iot_monitor"

 - **filter** - Informa ao NS que você deseja receber a mensagem passada por um filtro específico. Aceita um ID de filtro como um valor. Você deve criar um filtro antes de usar este campo. É possível fazer isso por meio da GUI ou da API de gerenciamento.

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&filter=SEU_FILTRO"

Todos os parâmetros descritos são passados pela **string de consulta** de conexão.

Parâmetro filter e parâmetros types, gateways, applications, tags e devices são mutuamente exclusivos. Isso significa que você deve especificar ou filtrar ou qualquer um dos outros parâmetros, mas não juntos.

Toda a filtragem realizada no lado NS.

#### Recuperação de histórico

Para sua conveniência, armazenamos dados por um período de tempo.

 - uplink, downlink - **48 horas**
 - outras mensagens - **1 hora**

Após a conexão, você pode recuperar as mensagens antigas, das quais poderá perder.

Para fazer isso, você deve especificar os parâmetros from_unixtime e/ou last_messages.

Todas as mensagens recuperadas virão com o sinalizador meta.history = true. (valor no json)

Não queremos atrapalhar seu tráfego e comunicação atuais em tempo real; portanto, todas as mensagens históricas aparecerão de maneira assíncrona.

Você pode receber mensagens de fluxo atual entre as históricas. Isso ajuda a manter o tráfego sensível à latência atualizado.

**Exemplo de reconexão com recuperação de histórico**

A melhor maneira de usar o recurso de histórico é armazenar meta.time (valor no json) da última mensagem recebida e, posteriormente, usar esse unixtime na reconexão no parâmetro from_unixtime.

Mas você deve ter em mente que isso pode exigir muitas mensagens. Para limitar a quantidade deles, use o parâmetro last_messages.

Apenas os 5 últimos jsons com este tempo:

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&from_unixtime=[1234567890]&last_messages=5"

#### Mais exemplos

Conecte-se à API de dados sem filtragem:

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN"

Conecte-se à API de dados e obtenha mensagem apenas do dispositivo com dev_eui=SEU_DEVICE_EUI

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&devices=SEU_DEVICE_EUI"

### Mensagens
Depois de conectar-se à API de dados, você pode receber e enviar mensagens diferentes: enviar mensagens do uplink do dispositivo, mensagens de depuração etc.

Todas as mensagens recebidas ou transmitidas através da interface da API de dados são objetos JSON com o seguinte formato:

| Nome | Tipo  | Descrição |
| ------------ | ------------ | ------------ |
| type | string  | O tipo de mensagem é usado para dividir as mensagens por sua funcionalidade: mensagens informativas, mensagens de uplink, mensagens de erro e assim por diante. |
| meta | objeto | Os metadados são uma estrutura comum para todos os tipos de mensagens e contêm esse tipo de informação como: identificador de dispositivo, identificador de mensagem e assim por diante... |
| params  | objeto  | Contém parâmetros específicos para o tipo específico de uma mensagem. Por exemplo, as mensagens de uplink mantêm o campo "payload", mas são perdidas nas solicitações de associação. |

#### Tipos

Cada mensagem contém um campo de tipo que é incluído para dividir as mensagens por sua funcionalidade: uplinks, downlinks, join, errors.

Cada tipo de mensagem possui uma estrutura de parâmetros correspondente.

Para um melhor entendimento, você pode dividir as mensagens em dois grupos:

1. LoRaWAN - mensagens geradas devido a ações do dispositivo ou para executar qualquer ação nos dispositivos.
Essas mensagens têm os seguintes tipos: uplink, downlink_request, downlink_response, downlink, join_request, join_response, status_request, status_response, downlink_claim.

2. Mensagens de serviço com tipos: error (erro), warning (aviso) e info (informação). Essas mensagens são geradas pelo NS no processo de processamento de mensagens LoRaWAN. Este grupo tem um propósito mais informativo/depuração que o primeiro.

Aqui está uma lista de tipos de mensagens:

| Nome | Descrição | Direção |
| ------------ | ------------ | ------------ |
| uplink | Uplink mensagens de dispositivos. Contém payload, informações de rádio, comandos mac e assim por diante... | do NS para o AS |
| downlink_request | Solicite uma mensagem gerada pelo NS caso tenha a oportunidade de enviar uma mensagem de downlink para um dispositivo. No caso de o AS ter algum downlink, ele será enviado ao NS. | do NS para o AS |
| downlink_response | Mensagem de resposta gerada pelo AS como resposta à mensagem downlink_request | do AS para o NS |
| downlink | Mensagem gerada pelo NS logo após uma mensagem de downlink ser realmente enviada para um dispositivo. Observe que não é possível usar esse tipo de mensagem para realmente enviar o downlink para um dispositivo. Por favor, use a sequência downlink_request/downlink_response.  | do NS para o AS |
| join_request | A mensagem de solicitação de associação é gerada no caso de o dispositivo estar usando o OTAA no lado do aplicativo. | do NS para o AS |
| join_response | A mensagem de aceitação de associação deve ser emitida pelo AS após um procedimento de associação bem-sucedido | do AS para o NS |
| status_request | Esta mensagem é gerada pelo AS para solicitar o status do dispositivo de acordo com a especificação LoRaWAN. Consulte o comando DevStatusReq MAC para obter detalhes.  | do AS para o NS |
| status_response | Mensagem com status do dispositivo de acordo com a especificação LoRaWAN. | do NS para o AS |
| downlink_claim | Esse tipo é usado apenas para dispositivos de classe C e notifica o servidor de rede sobre um novo pacote de uplink disponível. | de AS para o NS |
| error | Essas mensagens são geradas pelo NS para informar o AS sobre erros críticos que ocorreram durante o processamento de mensagens LoRaWAN e interações de NS para AS. Por exemplo: MIC está incorreto. | de NS para o AS |
| warning | Mensagem desse tipo é gerada em caso de erro durante o processamento da mensagem, mas o NS conseguiu concluir o processamento. Por exemplo: AS não está disponível. | de NS para o AS |
| info | Este é um tipo de mensagem auxiliar que pode ser usado para entender todas as etapas do processamento em detalhes. Por exemplo: a mensagem foi entregue com sucesso ao AS. | de NS para o AS |

#### Metadata

Cada mensagem contém a seguinte estrutura de metadados (essa estrutura é comum a todos os tipos de mensagens):

| Nome | Tipo | Descrição |
| ------------ | ------------ | ------------ |
| application | string | O identificador do aplicativo (app_eui pela especificação LoraWAN). |
| device | string | O identificador do dispositivo (dev_eui pela especificação LoraWAN). |
| device_addr | string | O endereço do dispositivo (dev_addr pela especificação LoraWAN). |
| gateway | string | O endereço MAC do gateway. |
| history | bool | Este sinalizador define para salvar as mensagens no histórico do Everynet Network Server. |
| network | string | O identificador da rede de gateways. |
| packet_hash | string | Mensagem hash. É muito importante entender os hashes de mensagens para interação bidirecional. |
| packet_id | string | Identificador de mensagem. Cada mensagem possui um identificador exclusivo. É possível usá-lo para identificar duplicadas. |
| version | integer | Versão atual do protocolo de servidor de rede everynet, padrão: 1. |

###### Mensagens bidirecionais

A API de dados suporta mensagens bidirecionais usando o modelo de solicitação-resposta.
Por exemplo, as mensagens downlink_request, downlink_response são usadas para obter dados do downlink do AS e enviá-los ao dispositivo.

Aqui está um diagrama que descreve um fluxo de mensagens entre NS e AS para enviar uma mensagem de downlink para um dispositivo:

[![packet_hash](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/06.svg "packet_hash")](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/06.svg "packet_hash")

Em outras palavras, a sequência é a seguinte:

- O NS envia ao AS um downlink_request com packet_hash=1 e aguarde a resposta.

- O AS processa esta mensagem e envia uma resposta com packet_hash=1.

- O NS corresponde a downlink_request e downlink_response e envia a mensagem para o dispositivo final.

#### Parâmetros

Os parâmetros de campo são específicos para cada tipo de mensagem e descritos na seção correspondente dedicada ao tipo de mensagem.

### Uplink - são mensagens recebidas de dispositivos finais.

O NS é capaz de adicionar opcionalmente os seguintes parâmetros adicionais às mensagens de uplink:

- radio - objeto que contém informações sobre propriedades de RF como RSSI, SNR e assim por diante...
Você deve usar o parâmetro radio=1 durante o procedimento de conexão para receber esses dados do NS.

Por exemplo:

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&radio=1"


- mac_commands - lista de comandos MAC recebidos nesta mensagem de uplink.

Por favor, use o parâmetro lora=1 em uma string de consulta para receber essas informações do NS.

Por exemplo:

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&lora=1"

Outra funcionalidade do NS é a capacidade de receber ou descartar mensagens duplicadas.
Para receber todas as mensagens duplicadas, use duplicate=1 na string de consulta.

Por exemplo:

> wscat C "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&duplicate=1"

Revise este diagrama para entender melhor como funciona a mensagem de uplink:

[![uplink](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/07.svg "uplink")](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/07.svg "uplink")

Neste diagrama, você pode ver como a mensagem de uplink é entregue ao AS:

1. O dispositivo envia uma mensagem para o gateway.

2. O gateway processa a mensagem e adiciona algumas informações adicionais a ela (por exemplo, parâmetros de RF) e envia para o NS.

3. O NS recebe a mensagem de uplink do gateway e a processa (descriptografar, desserializar,...) e a envia ao AS através da API de dados.

4. AS recebe uma mensagem com type=uplink

#### Parâmetros

| Nome | Descrição |
| ------------ | ------------ |
| rx_time | float, tempo em unixtime, quando o gateway recebeu este pacote, requerido. |
| counter_up | integer, contador de uplink do pacote LoraWAN, requerido. |
| port | integer, número da porta, FPort do pacote LoraWAN, requerido. |
| payload | string, opcional. |
| encrypted_payload | string, necessária. |
| duplicate | booleano, se a mensagem estiver duplicada, esse sinalizador será verdadeiro, obrigatório. |
| radio | objeto, dados de rádio, requerido. |
| radio.freq | float, frequência central em MHz (float não assinado, precisão Hz), requerido. |
| radio.time | float, unixtime, hora de receber a mensagem no gateway, opcional. |
| radio.modulation | object, informações sobre modulação, requerido. |
| radio.modulation.type | string, enumeração: LORA, FSK, requerido. |
| radio.modulation.coderate | string, identificador de taxa de codificação LoRa ECC, requerido. |
| radio.modulation.spreading | integer, obrigatório. |
| radio.modulation.bandwidth | integer, obrigatório. |
| radio.hardware | objeto, informações sobre hardware, requerido. |
| radio.hardware.tmst | integer, envie o pacote com um determinado valor de carimbo de data/hora (ignorará o tempo), requerido. |
| radio.hardware.channel | integer, canal IF do concentrador usado para RX (número inteiro não assinado), requerido. |
| radio.hardware.chain | integer, concentrador 'cadeia de RF', requerido. |
| radio.hardware.status | integer, status do CRC: 1 = OK, -1 = falha, 0 = nenhum CRC, requerido. |
| radio.hardware.rssi | float, RSSI em dBm (número inteiro assinado, precisão de 1 dB), requerido. |
| radio.hardware.snr | float, taxa SNR lora em dB (float assinado, precisão de 0,1 dB), requerido. |
| radio.hardware.gps | Coordenadas do gateway que foram usadas para receber esta mensagem específica: string, enum: LORA, FSK, requiredobject, geodata, opcional. |
| radio.hardware.gps.lat | float, latitude, opcional. |
| radio.hardware.gps.lng | flutuador, longitude, opcional. |
| radio.hardware.gps.alt | float, altitude, opcional. |

#### Exemplo:

O **primeiro exemplo** mostra como receber uma mensagem de uplink sem informações de rádio.

Vamos usar o cliente WebSocket chamado wscat.

Para se conectar ao servidor e começar a receber mensagens, você deve executar este comando (não se esqueça de usar seu próprio access_token):

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&types=uplink"

Você deve obter algo assim depois que seu cliente estiver conectado à API de dados:

JSON
----

```json
{
    "meta": {
        "network": "75697b95",
        "packet_hash": "889a72ab34a647f504ef37d598589431",
        "application": "70b3d54b17db0106",
        "device_addr": "36c365b4",
        "time": 1504806725.252493,
        "device": "faa73111a2aead2c",
        "packet_id": "bfa4be139911fe8ff80bc0afbf110fa3",
        "gateway": "7c95bd79864622a4"
    },
    "params": {
        "rx_time": 1504806725.245682,
        "port": 55,
        "counter_up": 118,
        "payload": "MjRjZjA4YWQyZGE5NGZlZDlkNmRiY2VkOTMwYWMzZjM=",
        "encrypted_payload": "ehMceJ/3W3itJE8rwwvL3y0yu485QMHpLCa4km/TZYM="
    },
    "type": "uplink"
}
```

O **segundo exemplo** mostra como receber mensagens de uplink com detalhes de RF em cada mensagem.

Vamos usar o wscat novamente, mas você deve adicionar radio=1 à string de consulta:

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&types=uplink&radio=1"

Logo após o estabelecimento da conexão da API de dados, você deve começar a receber mensagens como:

JSON
----

```json
{
    "meta": {
        "network": "75697b95",
        "packet_hash": "79f664df2c2073af798fa87497305d8d",
        "application": "70b3d54b17db0106",
        "device_addr": "36c365b4",
        "time": 1504806731.256388,
        "device": "faa73111a2aead2c",
        "packet_id": "fdbb09021c4523d9f28bb815ca872c70",
        "gateway": "7c95bd79864622a4"
    },
    "params": {
        "rx_time": 1504806731.249041,
        "port": 27,
        "radio": {
            "modulation": {
                "bandwidth": 125000,
                "type": 0,
                "spreading": 12,
                "coderate": "4/7"
            },
            "hardware": {
                "status": 1,
                "chain": 0,
                "tmst": 514586002,
                "snr": 5.0,
                "rssi": -100.0,
                "channel": 0,
                "gps": {
                    "lat": 59.890445709228516,
                    "lng": 30.258167266845703
                }
            },
            "freq": 868.1,
            "datarate": 0,
            "time": 1504806731.249041
        },
        "counter_up": 120,
        "payload": "ZGEwOTg3MmI4NmU4NGI4MDg4YzZmMWU4ZjM5NmViODU=",
        "encrypted_payload": "aiN3/x3Z7wz7NMPq+qoWf/17pq2J3Cx/p1kjvarfLEE="
    },
    "type": "uplink"
}
```

### Downlink Request (Solicitação de downlink)

Downlink Request - é uma mensagem usada pelo NS para informar ao AS que o NS tem uma oportunidade (janela TX) de enviar mensagem de downlink para um determinado dispositivo. Para enviar a mensagem de downlink, o AS deve gerar uma mensagem de resposta que conterá os dados necessários para o dispositivo.

Em outras palavras, se o AS tiver algo para enviar de volta ao dispositivo final, deverá enviar uma mensagem do tipo downlink_response para o NS.

Você pode perguntar por que temos um método tão complicado para enviar mensagens de downlink para o dispositivo final e por que NS é um iniciador da mensagem de downlink. Por que não usar o AS como iniciador e apenas armazenar esta mensagem no lado NS?

Infelizmente, não é possível no caso do NS não ter acesso ao AppSKey ou AppKey do dispositivo. Os contadores de uplink e downlink devem ser criptografados no lado do cliente, o que é um grande obstáculo para implementar um downlink simplificado direcionado ao AS.

Revise este diagrama de sequência para entender melhor como funciona o downlink_request e o downlink_response:

[![downlink_request](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/08.svg "downlink_request")](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/08.svg "downlink_request")

No diagrama, você pode ver as seguintes ações/eventos:

 - O NS recebe a mensagem de uplink do dispositivo final e a processa.

 - O NS envia uma mensagem de uplink para o AS.

 - O NS calcula o momento em que o downlink deve ser transmitido ao dispositivo e envia o downlink_request ao AS.

 - AS processa downlink_request e constrói um payload para a mensagem de downlink.

 - AS envia downlink_response para NS.

 - NS recebe downlink_response do AS.

 - O NS cria uma mensagem de downlink para o dispositivo final e envia dados para ele.

 - O NS cria uma mensagem com type=downlink e a transmite ao AS.

Observe que a mensagem de downlink pode ser recebida pelo AS, mesmo que nunca tenha emitido downlink_response para o NS.

Por exemplo, o NS recebeu uma mensagem confirmada de uplink e deve reconhecê-la de acordo com a especificação LoRaWAN. Isso significa que o NS enviará um downlink para o dispositivo e a mensagem com o tipo downlink será transmitida ao AS.

### Downlink Request (Solicitação de downlink)

Aqui, descrevemos todos os parâmetros incluídos na mensagem downlink_request de NS para AS.

#### Parâmetros

| Nome | Descrição |
| ------------ | ------------ |
| tx_time | float, registro de data e hora UNIX do tempo de transmissão de pacotes futuros, requerido. |
| counter_down | integer, contador de pacotes de downlink, requerido. |
| max_size | integer, tamanho máximo de payload que pode ser entregue, requerido. |

#### Exemplo:

JSON
----

```json
{
    "meta": {
        "network": "75697b95",
        "packet_hash": "79f664df2c2073af798fa87497305d8d",
        "application": "70b3d54b17db0106",
        "device_addr": "36c365b4",
        "time": 1504806731.258602,
        "device": "faa73111a2aead2c",
        "packet_id": "fdbb09021c4523d9f28bb815ca872c70",
        "gateway": "7c95bd79864622a4",
        "history": true
    },
    "type": "downlink_request",
    "params": {
        "counter_down": 71,
        "max_size": 51,
        "tx_time": 1504806733.249041
    }
}
```

### Downlink Response (Resposta de downlink)

Aqui, descrevemos todos os parâmetros incluídos na mensagem downlink_response de AS para NS.

#### Parâmetros

| Nome | Descrição |
| ------------ | ------------ |
| pendente | booleano, FPending, True se houver mais dados aguardando envio, opcional, padrão: false. |
| confirmed | booleano, mensagem confirmada, o servidor de rede aguardará a confirmação da entrega do dispositivo, opcional, padrão: false. |
| counter_down | integer, FCntDown (FCnt), reatribuir contador de pacotes de downlink, opcional, padrão: valor da mensagem de downlink NS. |
| port | integer, FPort, porta Frame, opcional, padrão: 1. |
| payload | codificada em string-base64, mensagem (codificada em BASE64, simples). Use isso no caso de app_key ser fornecido à rede. A criptografia será fornecida pela rede. |
| encrypted_payload | codificado em string-base64, FRMPayload, Message (codificado em BASE64, criptografado). Use isso no caso de o Application Server estar executando um procedimento de criptografia. |
| queue_if_late | booleano, opcional, padrão: false. Se o aplicativo estiver atrasado para responder, envie o payload para o próximo slot de downlink, se ele não tiver sido substituído. |

#### Exemplo:

JSON
----

```json
{
    "meta": {
        "network": "75697b95",
        "packet_hash": "79f664df2c2073af798fa87497305d8d",
        "application": "70b3d54b17db0106",
        "device_addr": "36c365b4",
        "time": 1504806731.258602,
        "device": "faa73111a2aead2c",
        "packet_id": "fdbb09021c4523d9f28bb815ca872c70",
        "gateway": "7c95bd79864622a4",
        "history": true
    },
    "type": "downlink_response",
    "params": {
        "pending": false,
        "confirmed": true,
        "counter_down": 71,
        "port": 25,
        "payload": "a0f1hh"
    }
}
```

### Downlink

Depois que a mensagem de downlink é transmitida para o dispositivo final, o NS gera uma mensagem com o type=downlink e envia essa mensagem para o AS.

Observe que essas mensagens não podem ser usadas para realmente enviar mensagens de downlink para os dispositivos finais. É gerado apenas para notificar o AS que o downlink foi enviado com sucesso pelo NS.

Para iniciar uma mensagem de downlink para o dispositivo, leia a seção downlink_request com atenção.

O NS permite adicionar opcionalmente informações sobre comandos MAC à mensagem de downlink: adicione o parâmetro lora=1 à string de consulta.

Por exemplo:

> wscat -c "wss://ns.atc.everynet.io/api/v1.0/data?access_token=SEU_TOKEN&&lora=1"

Para uma melhor compreensão do fluxo de mensagens, consulte este diagrama de sequência:

[![downlink](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/09.svg "downlink")](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/09.svg "downlink")

Em outras palavras, a seguinte sequência está ocorrendo:

 - Mensagem de uplink confirmado para transmissão ao dispositivo e aguarda a confirmação do servidor de rede.

 - O NS recebe mensagem de uplink do dispositivo, processa-a e envia mensagens de uplink e downlink_request para o AS.

 - O AS recebe mensagens de uplink e downlink_request, mas não tem nada para enviar de volta ao dispositivo.

 - O NS cria uma mensagem de downlink para o dispositivo e a envia um ack (acknowledge) confirmando o uplink.

 - O NS envia a mensagem de downlink ao AS para notificar sobre a mensagem de downlink para o dispositivo.

#### Parâmetros

A mensagem do tipo downlink possui os seguintes campos:

| Nome | Descrição |
| ------------ | ------------ |
| counter_down | integer, contador de downlink do pacote LoraWAN, requerido. |
| port | integer, FPort do pacote LoraWAN, requerido. |
| payload | string, mensagem (codificada em BASE64, simples). Use isso no caso de app_key ser fornecido à rede. A criptografia será fornecida pela rede, opcional. |
| encrypted_payload | string, FRMPayload, mensagem (codificada em BASE64, criptografada). Use isso no caso de o Application Server estar executando um procedimento de criptografia, requerido. |
| duplicate | booleano, se a mensagem estiver duplicada, esse sinalizador será verdadeiro, obrigatório. |
| radio | object, inclui informações de rádio sobre hardware, modulação, frequência, requerido. |
| radio.freq | float, frequência central em MHz (float não assinado, precisão Hz), requerido. |
| radio.time | float, unixtime, hora de receber a mensagem no gateway, opcional. |
| radio.modulation | object, informações sobre modulação, requerido. |
| radio.modulation.type | string, tipo de modulação, enumeração: LORA, FSK, requerido. |
| radio.modulation.coderate | string, identificador de taxa de codificação LoRa ECC, requerido. |
| radio.modulation.spreading | integer, fator de propagação da mensagem LoRa, requerido. |
| radio.modulation.bandwidth | integer, largura de banda da mensagem LoRa, requerido. |
| radio.hardware | object, informações sobre hardware, requerido. |
| radio.hardware.tmst | integer, envia o pacote com um determinado valor de carimbo de data/hora (ignorará o tempo), requerido. |
| radio.hardware.channel | integer, canal IF do concentrador usado para RX (número inteiro não assinado), requerido. |
| radio.hardware.chain | integer, concentrador 'cadeia de RF', requerido. |
| radio.hardware.status | integer, status do CRC: 1 = OK, -1 = falha, 0 = nenhum CRC, requerido. |

#### Exemplo:

JSON
----

```json
{
    "meta": {
        "network": "75697b95",
        "packet_hash": "79f664df2c2073af798fa87497305d8d",
        "application": "70b3d54b17db0106",
        "device_addr": "36c365b4",
        "time": 1504806731.759066,
        "device": "faa73111a2aead2c",
        "packet_id": "fdbb09021c4523d9f28bb815ca872c70",
        "gateway": "7c95bd79864622a4",
        "history": true
    },
    "params": {
        "radio": {
            "modulation": {
                "bandwidth": 125000,
                "type": 0,
                "coderate": "4/7",
                "spreading": 12,
                "inverted": true
            },
            "hardware": {
                "status": 1,
                "chain": 0,
                "power": 14.0,
                "tmst": 515586002,
                "channel": 0
            },
            "freq": 868.1,
            "datr": "SF12BW125",
            "time": 1504806732.249041
        },
        "payload": "YLRlwzaHRwAEAAUA0q2EFHt7NA==",
        "port": 0,
        "counter_down": 71
    },
    "type": "downlink"
}
```

### Join (Junte-se)

Este tipo de mensagem deve ser usado para o dispositivo OTAA no lado AS. Esta mensagem não será gerada se o AppKey for fornecido ao AS e o AS puder executar o procedimento de junção sozinho.


Você deve usar estes parâmetros para provisionar um dispositivo OTAA para o servidor de rede por meio da Management API ou da GUI:

- criptografia = APP

Isso significa que o servidor de aplicativos será responsável por executar o procedimento de ativação.

- ativação = OTAA

O tipo de ativação é OTAA.

Para uma melhor compreensão do fluxo de dados do OTAA, vejamos este diagrama.

[![join](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/09.svg "join")](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/09.svg "join")

A sequência é a seguinte:

 - O dispositivo inicia uma solicitação de associação e a envia ao servidor de rede.

 - O NS recebe uma solicitação de associação, processa-a, prepara a mensagem de associação e envia-a ao AS.

 - O AS recebe a mensagem de junção, com uma solicitação de junção fechada e a processa.

 - AS prepare a mensagem de junção com a aceitação de junção interna e envie de volta para o NS.

 - O NS recebe a mensagem de junção do AS, prepara a mensagem de junção aceita e a envia para o dispositivo final.


### Join Request (Solicitação de associação)

Join Request - esse é um objeto JSON que é transferido do NS para o AS.

#### Parâmetros

A solicitação de associação contém os seguintes campos:

| Nome | Descrição |
| ------------ | ------------ |
| net_id | Identificador de rede por LoraWAN, string, obrigatório. |
| dev_nonce | É um valor aleatório para cada tamanho de dispositivo final: 2 bytes, sequência, requerido. |
| dev_eui | O identificador do dispositivo final, string, requerido. |
| dev_addr | O endereço do dispositivo final, string, requerido. |
| cf_list | Lista de frequências de canal, sequência, opcional. |

#### Exemplo:

JSON
----

```json
{
    "meta": {
        "network": "9e9bf02a",
        "packet_hash": "adc6bcac0d06195bc0329c3ef6a2d6ea",
        "application": "b3a1067cf7085309",
        "time": 1504638900.866375,
        "device": "8c30dd074be218cb",
        "packet_id": "287f9555a3e8b000ffc8c3c50f60e309",
        "gateway": "017e8cd996cd3a0e"
    },
    "params": {
        "dev_eui": "8c30dd074be218cb",
        "dev_addr": "01d6dcd6",
        "dev_nonce": "f9e7",
        "net_id": "000000"
    },
    "type": "join_request"
}
```

### Join Response (Resposta de Ingresso)

Join accept - esta é uma mensagem join_response, que é transferida do AS para o NS.

#### Parâmetros

A resposta de junção contém os seguintes campos:

| Nome | Descrição |
| ------------ | ------------ |
| nwkskey | string, chave de sessão de rede, requerido. |
| accept_payload | string, mensagem de aceitação de associação (codificada em BASE64, criptografada), requerido. |

#### Exemplo:

JSON
----

```json
{
    "meta": {
        "network": "9e9bf02a",
        "packet_hash": "adc6bcac0d06195bc0329c3ef6a2d6ea",
        "application": "b3a1067cf7085309",
        "time": 1504638900.866375,
        "device": "8c30dd074be218cb",
        "packet_id": "287f9555a3e8b000ffc8c3c50f60e309",
        "gateway": "017e8cd996cd3a0e"
    },
    "type": "join_response",
    "params": {
        "nwkskey": "d64c9050214b394aa2042f0e934b6180",
        "accept_payload": "ysgRl452xNLep9S1NTIg2lomKDxUgn3DJ7DE+b00Ass"
    }
}
```

### Status

As mensagens do tipo status devem ser usadas como mensagens informativas sobre o status da bateria do dispositivo e os parâmetros de RF.

A mensagem de status está implementando a funcionalidade DevStatusReq do comando MAC do LoRaWAN.

Para recuperar um status de dispositivo usando o DevStatusReq, você deve executar as seguintes etapas:

1. O AS envia status_request ao NS.

2. O NS recupera informações do dispositivo e as envia por status_response ao AS.

Vamos percorrer o diagrama de sequência para entender como a mensagem de status funciona:

[![status](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/09.svg "status")](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/09.svg "status")

Esta é uma sequência:

 - AS envia mensagem de status para NS.

 - O NS envia status_request ao dispositivo final e obtém status_response.

 - O NS cria uma mensagem de status para o AS e a envia.

### Status Request (Solicitação de status)

Solicitação de status - é uma mensagem do tipo status que foi enviada do AS para o NS.

#### Metadata (Metadados)

Você deve especificar os seguintes campos de metadados da mensagem de status antes de enviá-lo:

 - device - identificador de dispositivo (dev_eui).
 - network - identificador de rede ao qual este dispositivo pertence.

É possível especificar um gateway como uma opção para solicitar ao mecanismo de otimização de downlink do NS que use um gateway específico para enviar uma mensagem de downlink. Se esse gateway não estiver ativo, a solicitação não será enviada.

#### Parâmetros

Não há parâmetros nesta mensagem.

#### Exemplo:

JSON
----

```json 
{
    "meta": {
        "network": "1a3f34a3",
        "device": "ba27356cb8a25961"
    },
    "type": "status"
}
```

### Status Response (Resposta de status)

Status Response - esta é uma mensagem do tipo status, enviada do formulário NS para o AS.

#### Parâmetros

| Nome | Descrição |
| ------------ | ------------ |
| baterry | float, nível da bateria do dispositivo: 1-254 (0 = fonte de alimentação externa, 255 = desconhecido), requerido. |
| snr | float, relação sinal/ruído em dB arredondada para o valor inteiro mais próximo do último pacote recebido com sucesso, requerido. |
| rx_time | float, tempo em unixtime, quando o gateway recebeu este pacote, requerido. |

#### Exemplo:

JSON
----

```json
{
    "meta": {
        "network": "1a3f34a3",
        "packet_hash": "5e99eb9640ea76257911d3ebeb525b07",
        "application": "64649e06824532c7",
        "device_addr": "ac1ffea9",
        "time": 1504638907.180523,
        "device": "ba27356cb8a25961",
        "packet_id": "1c87b507b5fa4ef0f610d7f1befd593d",
        "gateway": "4adc2ea8e5a8fc8f"
    },
    "params": {
        "battery": 254.0,
        "snr": 20.0,
        "rx_time": 1504638907.171101
    },
    "type": "status"
}
```

### Downlink Claim (Reivindicação de downlink)

Esse tipo de mensagem é usado nos dois casos a seguir:

1 - Para dispositivos com classe C: para enviar imediatamente uma mensagem de downlink para o dispositivo.
2 - Para dispositivos com classe A: para agendar mensagem de downlink para o próximo intervalo de tempo disponível.

As mensagens do tipo downlink_claim permitem notificar o NS sobre a disponibilidade dos dados do downlink no lado do AS (o AS está pronto para enviar algum dispositivo). Em outras palavras, o downlink_claim inicia a transmissão da mensagem downlink_request do NS para o AS.

Vamos percorrer estes diagramas de sequência para entender melhor como a mensagem downlink_claim funciona:

Para classe A

[![notify_class_a](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/12.svg "notify_class_a")](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/12.svg "notify_class_a")

Sequência é semelhante a seguinte:

 - AS envia a mensagem downlink_claim ao NS.
 - O NS prepara downlink_request e envia para o AS.
 - AS processando downlink_request.
 - O AS gera payload do downlink e envia downlink_response ao NS.
 - O NS recebe o payload do downlink e o salva.
 - O dispositivo final envia uma mensagem de uplink ao NS.
 - O NS recebe o payload do downlink e gera imediatamente a mensagem do downlink e a envia para o dispositivo final.
 - O NS gera uma mensagem de downlink para o AS e a envia.

Para a classe C

[![notify](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/13.svg "notify")](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/13.svg "notify")

Sequência é semelhante a seguinte:

 - AS envia a mensagem downlink_claim ao NS
 - O NS prepara downlink_request e envia para o AS
 - AS processando downlink_request
 - O AS gera payload do downlink e envia downlink_response ao NS
 - O NS gera mensagem de downlink e a envia para o dispositivo final
 - O NS gera uma mensagem de downlink para o AS e a envia.


#### Metadata (Metadados)

Você deve especificar os seguintes campos nos metadados downlink_claim para emitir uma mensagem desse tipo:

 - device - identificador de dispositivo

É possível especificar um gateway e uma rede como uma opção para solicitar ao mecanismo de otimização de downlink do NS que use um gateway específico para enviar uma mensagem de downlink. Se esse gateway não estiver ativo, a solicitação não será enviada.

#### Parâmetros

A lista de parâmetros está vazia.

Exemplo:

JSON
----

```json
{
    "meta": {
        "network": "1a3f34a3",
        "gateway": "",
        "device": "ba27356cb8a25961"
    },
    "type": "downlink_claim"
}
```

### Location (Localização)

As mensagens do tipo location devem ser usadas como mensagens informativas sobre soluções de localização geográfica do dispositivo. Eles são gerados no caso de uma nova solução estar disponível para um dispositivo específico.

Cada solução contém coordenadas geográficas estimadas do sensor e algumas informações específicas

Métodos atualmente suportados:

 - simple:moving

Método simple:moving

Este método resolve a posição do dispositivo com base na qualidade do sinal de uplinks recebidos.

#### Parâmetros

| Nome | Descrição |
| ------------ | ------------ |
| solutions | array, Matriz de soluções de geolocalização que este dispositivo suporta. |

#### Objeto Solution

| Nome | Descrição |
| ------------ | ------------ |
| lat | float, Latitude. |
| lng | float, Longitude. |
| precision | float, Resultado da precisão da solução, em metros. |
| method | string, Nome do método da solução. |
| quality | float, A qualidade da solução, deve ser usada para comparar soluções. |

#### Exemplo:

JSON
----

```json
{
  "meta": {
    "packet_hash": "899e8989368abce7c62eb1342be086a5",
    "org": "59bd2b1c61a6040008f6a110",
    "time": 1527533919.123981,
    "device": "6231384f96b377f7",
    "application": "62982a08f8ae78cd"
  },
  "type": "location",
  "params": {
    "solutions": [
      {
        "lat": 51.50740,
        "lng": 0.12780,
        "quality": 1,
        "precision": 1200,
        "method": "simple:moving"
      }
    ]
  }
}
```

### Error (Erro)

As mensagens do tipo error visam notificar o AS sobre erros críticos durante o processamento da mensagem LoRaWAN.

Essas mensagens são geradas no caso de o NS não conseguir concluir o processamento da mensagem LoRaWAN por alguns motivos: MIC ruim, CRC ou outro...

No diagrama abaixo, você pode ver um exemplo desse tipo de erro: o dispositivo está tentando executar o OTAA usando o dev_nonce que já foi usado anteriormente.

[![error](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/14.svg "error")](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/14.svg "error")


A sequência nesse exemplo tem a seguinte aparência:

 - O dispositivo inicia o OTAA e envia join_request ao NS.

 - O NS processa join_request, cria join_accept e envia de volta ao dispositivo.

 - O dispositivo está tentando executar o OTAA novamente usando o mesmoDEV_NONCE, cria join_request e envia para o NS.

 - O NS identifica um erro e envia uma mensagem de erro ao AS.

#### Parâmetros

| Nome | Descrição |
| ------------ | ------------ |
| message | string, requerido. |
| code | string, opcional. |

#### Exemplo:

JSON
----

```json
{
    "meta": {
        "network": "a0842237",
        "packet_hash": "451d26187b5dbc94e12d040ae094b5e2",
        "application": "b3a1067cf7085309",
        "time": 1504638860.752536,
        "device": "8c30dd074be218cb",
        "packet_id": "9b34f5f1bf8a38ccff7589e30312bf67",
        "gateway": "f5791b767ff5cf7a"
    },
    "type": "error",
    "params": {
        "message": "Join request rejected. The same DEV_NONCE was processed before. Possible replay attack"
    }
}
```

#### Lista de erros

 - A solicitação da mensagem de downlink falhou devido ao erro do servidor de rede: razão.

 - Não foi possível criptografar os dados do aplicativo. O aplicativo retornou o payload descriptografado, mas não forneceu APP_SESSION_KEY para criptografia.

 - O aplicativo retornou o payload com formato incorreto. String base64 esperada.

 - Solicitação de associação rejeitada: o dispositivo dev_eui tenta enviar dados para o AppEUI errado (app_eui).

 - Pedido de ingresso rejeitado. O mesmo DEV_NONCE foi processado antes. Possível ataque de repetição.

 - Falha na verificação MIC da solicitação de associação para DEV_EUI.

 - Falha na associação: tempo limite da solicitação do aplicativo. Verifique a disponibilidade do aplicativo.

 - Falha na associação devido ao erro do servidor de rede: reasone.

 - Falha na verificação do MIC da mensagem de dados. Parece que os contadores não são sincronizados. O Core tentará recuperar os contadores.

 - Os contadores de dispositivos não são sincronizados e não é possível recuperá-los.

 - O contador de uplink do dispositivo é menor ou igual ao último contador de uplink conhecido. Possível ataque de repetição.

 - Falha ao enviar a mensagem 'status': tempo limite da solicitação do aplicativo. Verifique a disponibilidade do aplicativo.

 - O envio da mensagem 'status' falhou devido ao erro do servidor de rede: razão.

### Warning (Atenção)

Essa mensagem será gerada se o NS tiver alguns problemas durante o processamento da mensagem, mas ainda assim concluir as etapas de processamento com êxito.

Aqui está um exemplo da situação em que nenhum AS respondeu ao NS downlink_request.

[![warning](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/15.svg "warning")](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/15.svg "warning")

 - Mensagem de uplink confirmada pelo dispositivo.
 - O processo NS confirmou a mensagem de uplink, prepare downlink_request e envie-a para o AS.
 - O AS não responde e não envia downlink_response de volta ao NS NS.
 - O NS não recebe o downlink_reseponse do AS, cria uma mensagem de aviso e a envia para o AS.


#### Parâmetros

| Nome | Descrição |
| ------------ | ------------ |
| message | string, requerido. |
| code | string, opcional. |

#### Exemplo:

JSON
----

```json
{
    "meta": {
        "network": "75697b95",
        "packet_hash": "79f664df2c2073af798fa87497305d8d",
        "application": "70b3d54b17db0106",
        "device_addr": "36c365b4",
        "time": 1504806731.754539,
        "device": "faa73111a2aead2c",
        "packet_id": "fdbb09021c4523d9f28bb815ca872c70",
        "gateway": "7c95bd79864622a4"
    },
    "type": "warning",
    "params": {
        "message": "Requesting downlink message failed: application request timeout. Please check application availability."
    }
}
```

#### Lista de avisos

 - Mensagem de downlink com payload vazio enviado ao dispositivo dev_eui.

 - Downlink desativado para este dispositivo.

 - A solicitação da mensagem de downlink falhou: tempo limite da solicitação do aplicativo. Verifique a disponibilidade do aplicativo.

 - O pacote recebido está fora da banda do dispositivo.

 - O dispositivo tentou enviar uma solicitação de associação, mas os uplinks estão bloqueados neste dispositivo.

 - O dispositivo tentou enviar mensagem, mas os uplinks estão bloqueados neste dispositivo.

 - Mensagem de uplink com contador repetido recebido.


### Informações

Mensagens com o tipo info são mensagens auxiliares projetadas para fornecer mais informações sobre as etapas de processamento de mensagens ao AS.

Este é um exemplo de processo bem-sucedido da OTAA:

[![info](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/16.svg "info")](https://github.com/AdailSilva/DocsEverynet_pt-BR/blob/master/images/16.svg "info")

 - O dispositivo inicia o processo OTAA e envia join_request ao NS.

 - O processo NS join_request, cria join_accept e envia mensagem do tipo info para o AS, informando que o processo OTAA foi concluído com êxito.

#### Parâmetros

| Nome | Descrição |
| ------------ | ------------ |
| message | string, requerido. |
| code | string, opcional. |

#### Exemplo:

JSON
----

```json
{
    "meta": {
        "network": "a5cd542d",
        "packet_hash": "2ed8b2694a5e0c8e24e5bb2229124192",
        "application": "0fbdac8884ed782b",
        "time": 1504699637.060622,
        "device": "51924777a6205c40",
        "packet_id": "fc3d9d3550f3cc2419e718873f230e7b",
        "gateway": "e576313d4513efc4"
    },
    "params": {
        "message": "Join request accepted"
    },
    "type": "info"
}
```

Lista de mensagens informativas

 - Mensagem de downlink agendada para envio.

 - A solicitação da mensagem de downlink do aplicativo foi bem-sucedida.

 - Solicitação de participação duplicada recebida.

 - Pedido de associação aceito.

 - Resposta de ingresso recebida com sucesso do aplicativo.

 - Mensagem de dados recebida e processada.

 - Mensagem de uplink sem payload recebido e processado.

 - Mensagem de status entregue ao aplicativo.

 - Mensagem duplicada recebida duplicada recebida.

### Adaptadores

Adaptador - é uma ponte entre o NS e serviços de terceiros, como: MQTT, PubNub, HTTP, etc...

A versão atual do NS contém os seguintes adaptadores:

 - HTTP
 - MQTT
 - My devices

#### Conexão HTTP

Este conector permite que os dados sejam transferidos de/para o Everynet Network Server para um servidor HTTP específico hospedado pelo usuário.

Para habilitar o adaptador HTTP, você deve criar uma nova conexão na API de gerenciamento Everynet ou na interface do servidor de rede, selecione 'Adaptador HTTP/HTTP' e use os seguintes argumentos:

| Argumento | Requerido | Descrição |
| ------------ | ------------ | ------------ |
| description | não | Descrição da conexão. |
| filter | sim | ID do filtro do servidor de rede. |
| url | sim | URL do seu servidor, mais descrição abaixo. |
| authorization | não | valor do cabeçalho da autorização, mais descrição abaixo. |

#### URL

Exemplo:

> https://usuario:senha@exemplo.com.br:1234/messages/{type}/{device}

A substituição de campos se aplica apenas às peças, após o campo da porta (caminho, parâmetros, consulta, hash)

Se o campo não estiver presente, ele será deixado como está, por exemplo, /messages/{type}/{device}

Lista de campos que podem ser substituídos:

|   |   |
| ------------ | ------------ |
| device | O dispositivo EUI (dev_eui pela especificação LoraWAN). |
| device_addr | O endereço do dispositivo (dev_addr pela especificação LoraWAN). |
| application | A aplicação EUI (app_eui pela especificação LoraWAN). |
| gateway | O endereço mac do gateway. |
| network | O identificador de rede de gateways. |
| type | O tipo de mensagem (uplink / join / error / e.t.c.) |

#### Autorização

Você pode especificar um valor de cabeçalho de autorização.

**Este campo é obrigatório se você deseja enviar solicitações AO servidor de rede.**

Este valor é usado para ambos os lados da solicitação.

- O conector enviará solicitações para seu aplicativo com esse cabeçalho.

- O conector espera que esse cabeçalho tenha o mesmo valor, se você enviar uma solicitação.

Exemplo:

Se você especificar o campo como:

> "authorization": "Token 123"

Os pedidos conterão o cabeçalho e esperam o mesmo do seu aplicativo, se ele fizer pedidos:

> Headers:
...
Authorization: Token 123
...

#### Recebendo mensagens do servidor de rede

O Connector executa dois tipos de solicitações HTTP para seu aplicativo: POST e OPTIONS

As mensagens do NS são solicitadas pelo POST (o exemplo é fornecido abaixo)

A solicitação é considerada bem-sucedida pelo conector se a resposta for HTTP 2xx ou HTTP 4xx.

O conector tem 4 segundos para realizar a conexão com seu aplicativo (incluindo o handshake SSL) e, em seguida, 1 segundo para receber uma resposta. A solicitação deve ser recebida dentro desses tempos limite para ser considerada bem-sucedida.

Responda o mais rápido possível. Evite realmente processar e reagir a eventos dentro do mesmo processo. Implemente uma fila para manipular eventos de entrada após serem recebidos.

O conector suporta conexões keep-alive e mantém até 10 conexões paralelas.

#### Envie mensagens para o servidor de rede

Se sua resposta for HTTP 2xx, o tipo MIME é application/json e contém JSON válido, o payload será encaminhado para o NS.

Se sua resposta for HTTP 4xx, o corpo da resposta será ignorado.

Se sua resposta for HTTP 5xx, a solicitação será tratada como falhada.

#### Solicita tratamento de erros e novas tentativas

Seu aplicativo pode responder com um HTTP 3xx e seguiremos até dois redirecionamentos, até que você forneça um código de sucesso HTTP 2xx ou HTTP 4xx.

Se sua solicitação falhar, tentaremos novamente duas vezes com um intervalo crescente entre elas.

Cada solicitação vem com cabeçalhos personalizados configurados para dar suporte à lógica de tentativas:

 - Request-Id (ID da solicitação): ID exclusivo da solicitação. É o mesmo para todas as novas tentativas.

- Retry-Number (Número de novas tentativas): presente se houver uma nova tentativa e contiver o número de sequência de novas tentativas.

>Request-Id (ID da solicitação): 93c437e8-6e88-11ea-87f8-9da0f1c114a3
>Retry-Number (Número de novas tentativas): 2

A solicitação é tratada como falhada se falhar em todas as novas tentativas. Nesse caso, o último erro será armazenado nos logs de conexão.

Existe um contador de taxa de erro no interior, monitorando os últimos 600 segundos ou 10000 solicitações. Esse contador inclui POST e OPTIONS.

Se você tiver 5% ou mais de solicitações com falha no aplicativo, sua conexão ficará temporariamente desativada por 60 segundos.

As conexões com taxa inferior a 100 solicitações por 600 segundos não serão desativadas.

#### Ciclo de trabalho

Após a conexão inicializar ou ser desativada, o conector tenta fazer uma verificação de saúde do seu aplicativo usando a solicitação OPTIONS.

Se primeiro solicitar êxito, a conexão será tratada como aberta e o tráfego começará a fluir.

se você não tiver solicitações do NS por 10 segundos, a solicitação de verificação OPTIONS será enviada.

Se a sua taxa de erro for alta o suficiente para falhar. A conexão será temporariamente desabilitada e todos os soquetes TCP do seu aplicativo serão fechados.

O ciclo de trabalho da conexão começa desde o início quando o tempo limite de desativação expirou.

#### Solicitações do aplicativo

O URL para as solicitações:
>
https://adapters.ns.sua_regiao.everynet.io/http2/cb/seu_id_de_conexao

>
Exemplo:
https://adapters.ns.atc.everynet.io/http2/cb/5eb858c86c1837f2550ae2cb

Você pode enviar as solicitações ao servidor de rede com solicitações HTTP para esse URL.

Todas as regras aplicadas a esta solicitação são semelhantes à resposta da sua inscrição, mas você DEVE especificar o cabeçalho da Autorização (consulte a seção).

Você pode especificar um valor de cabeçalho de autorização.

### Exemplos de uso

#### Verificação de conexão

Para verificar se seu servidor está disponível ou não, o conector fará uma verificação.

Periodicamente, ele enviará a solicitação OPTIONS para seu aplicativo, que você deve responder com alguma resposta HTTP adequada.

Exemplo:
>
OPTIONS /lora/%7Bdevice%7D/%7Btype%7D HTTP/1.1
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
Host: exemplo.com.br
Content-Length: 0
Request-Id: 93c437e8-6e88-11ea-87f8-9da0f1c114a3

>
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8
Allow: POST, OPTIONS
Content-Length: 0
Date: Mon, 16 Jul 2018 10:38:10 GMT

#### Simple flow uplink, downlink_request (Fluxo simples, uplink, downlink_request)

Sobre o que é este exemplo:

 - Você possui um servidor HTTP com o seguinte URL: http://exemplo.com.br

 - Você receberá mensagens de uplink no ponto de extremidade do servidor http://exemplo.com.br/uplink e mensagens de downlink_request para http://seuservidor.com.br/downlink_request.

O que você deveria fazer:

1. Crie um filtro no NS para os dados que você deseja receber. Selecione os tipos de uplink e downlink_response.

2. Crie uma conexão HTTP com o seguinte URL: http://exemplo.com.br/{type} e o ID do filtro que você acabou de criar.

3. Depois disso, o servidor enviará uma solicitação de verificação de conexão ao seu aplicativo.

>
OPTIONS /exemplo HTTP/1.1
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: everynet-http
Host: exemplo.com.br
Authorization: b24023b99492fc94
Content-Length: 0
Request-Id: 93c437e8-6e88-11ea-87f8-9da0f1c114a3

>
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8
Allow: POST, OPTIONS
Content-Length: 0
Date: Fri, 20 Jul 2018 06:53:53 GMT

Se o seu aplicativo respondeu a isso, o conector começa a enviar mensagens para o seu aplicativo.

Exemplo de mensagem de uplink:

>
POST /uplink HTTP/1.1
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: everynet-http
Host: exemplo.com.br
Content-Length: 543
Content-Type: application/json
Request-Id: 93c437e8-6e88-11ea-87f8-9da0f1c114a3

JSON
----

```json
{
   "params":{
      "payload":"MzQ3NjcwNjFiNDc3NGU2ZmFiZjBhNmY4YTJjYmI0Y2M=",
      "port":7,
      "duplicate":false,
      "counter_up":3,
      "rx_time":1532073817.157281,
      "encrypted_payload":"pLgR8Tzh3JptkhtozJ5OlFuS3zQCygWD5hmx9zMjLnU="
   },
   "meta":{
      "network":"e23d2f31af81b25ef50375b5b7810c52",
      "packet_hash":"73465c1ed0cae413816d0f78baf3dcc2",
      "application":"1293e9e373666fd5",
      "device_addr":"d242b7a6",
      "time":1532073817.175208,
      "device":"b2b48f713c2f973d",
      "packet_id":"f577207419bb4701ff9f7874c2e2808e",
      "gateway":"92a199d4e41ab64b"
   },
   "type":"uplink"
}
```

>
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
Date: Fri, 20 Jul 2018 08:03:37 GMT

Exemplo de mensagem downlink_request e resposta da mensagem downlink_response de volta:

>
POST /downlink_request HTTP/1.1
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: everynet-http
Host: exemplo.com.br
Content-Length: 412
Content-Type: application/json

JSON
----

```json
{
   "params":{
      "counter_down":3,
      "max_size":51,
      "tx_time":1532075747.295559
   },
   "meta":{
      "network":"12b5d8a8df8d9255c65d6d565d836a9d",
      "packet_hash":"cf59f7bf410a9eb23383f41342c3c7fe",
      "application":"6264dd6a1b4e9ca1",
      "device_addr":"f22eef89",
      "time":1532075746.335046,
      "device":"c20ba71a9affafc6",
      "packet_id":"a8b464039cca609bed00f8ec58f494fe",
      "gateway":"524d07d7ef40dea3"
   },
   "type":"downlink_request"
}
```

>
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 476
Date: Fri, 20 Jul 2018 08:35:46 GMT

JSON
----

```json
{
  "meta": {
    "application": "6264dd6a1b4e9ca1", 
    "device": "c20ba71a9affafc6", 
    "device_addr": "f22eef89", 
    "gateway": "524d07d7ef40dea3", 
    "network": "12b5d8a8df8d9255c65d6d565d836a9d", 
    "packet_hash": "cf59f7bf410a9eb23383f41342c3c7fe", 
    "packet_id": "a8b464039cca609bed00f8ec58f494fe", 
    "time": 1532075746.335046
  }, 
  "params": {
    "counter_down": 3, 
    "payload": "220de733f4", 
    "port": 50
  }, 
  "type": "downlink_response"
}
```

### Classe C downlink_claim

Você também pode enviar esse tipo de mensagem como resposta ao seu aplicativo.

1-3. Repita as mesmas etapas para o exemplo de fluxo Simples

1. Se você deseja enviar a mensagem downlink_claim, é necessário definir o parâmetro de autorização na conexão. Ele será usado para verificar as solicitações do seu aplicativo ao conector para verificação de segurança.

Por exemplo:

 - Authorization (Autorização) = Token 1234567890 (O mesmo que um campo de autorização na conexão que você definiu).
 - Connection ID (ID da conexão) = 5b51a9a8e15b770005c928c9.

 - Authorization = Token 1234567890
 - Connection ID = 5b51a9a8e15b770005c928c9

>
POST /http2/cb/5b51a9a8e15b770005c928c9 HTTP/1.1
Accept: application/json, */*
Accept-Encoding: gzip, deflate
Authorization: Token 1234567890
Connection: keep-alive
Content-Length: 142
Content-Type: application/json
Host: adapters.ns.atc.everynet.io
User-Agent: HTTPie/1.0.0-dev

JSON
----

```json
{
    "meta": {
        "device": "d2953b67bca671a6", 
        "network": "12024f9efc46a98120a6fac272a9c3a4"
    }, 
    "type": "downlink_claim"
}
```

>
HTTP/1.1 202 Accepted
Connection: keep-alive
Content-Length: 0
Content-Type: text/html; charset=utf-8
Date: Fri, 20 Jul 2018 09:47:30 GMT

### Conexão MQTT

Este conector permite conectar o Servidor de Rede ao seu aplicativo usando o protocolo MQTT.

#### Para tipos de mensagens, consulte a seção correspondente das mensagens da API de dados.

| Argumento | Requerido | Descrição |
| ------------ | ------------ | ------------ |
| description | não | Descrição da conexão. |
| uri | sim | URI do corretor, consulte o esquema. |
| filter | sim | O ID do filtro do servidor de rede. |
| topic_up | sim | O nome do tópico para as mensagens que o servidor de rede publicará. A TI oferece suporte à substituição em tempo real por tipo e campos em "meta". O nome deste tópico pode conter o tipo de mensagem e os campos da meta, por exemplo, /messages/{type}/{device}/ |
| topic_down | não | O nome do tópico para o servidor de rede da mensagem será assinado. |

Lista de esquemas que podem ser usados no campo URI:

| Esquema | Criptografada | Porta padrão | Descrição |
| ------------ | ------------ | ------------ | ------------ |
| mqtt:// | não | 1883 | TCP MQTT nativo. |
| mqtts:// | sim | 8883 | TLS TCP MQTT nativo, requer certificado válido para nome de domínio. |
| ws:// | não | 80 | WebSocket MQTT, suporta caminho customizado (/mqtt, se não fornecido). |
| wss:// | sim | 443 | Secured WebSocket MQTT, suporta caminho personalizado (/mqtt, se não fornecido), requer certificado válido para o nome de domínio. |

A autenticação é opcional, mas, se houver, deve ser feita usando os parâmetros básicos do URI mqtts://usuario:senha@exemplo.com.br:1234

A lista de campos pode ser substituída no campo topic_up:

|   |   |
| ------------ | ------------ |
| device | O dispositivo EUI (dev_eui pela especificação LoRaWAN). |
| device_addr | O endereço do dispositivo (dev_addr pela especificação LoRaWAN). |
| application | A aplicação EUI (app_eui pela especificação LoRaWAN). |
| gateway | O endereço mac do gateway. |
| network | O identificador de rede de gateways. |
| type | O tipo de mensagem (uplink / join / error / e.t.c.). |

#### QoS

Todas as mensagens são enviadas usando MQTT QoS=1

Isso significa que seu corretor DEVE reconhecer com PUBACK todas as mensagens.

O tempo limite para a mensagem que está aguardando é de **1 segundo**

O máximo de mensagens em espera é de **100 mensagens**

#### Reconexões

Se a conexão com o broker cair, o conector está tentando se reconectar a ele. O tempo limite para isso é o seguinte. Começa com **0,1s** e dobra a cada falha seguinte, o tempo limite máximo é de **60s**.

#### Mensagens perdidas

Durante a reconexão, o conector solicita mensagens antigas do NS desde que a conexão caiu.

### Ciclo de trabalho do adaptador

Depois que a conexão com o broker MQTT for estabelecida, o conector começará a PUBLISH dados para o topic_up gerado.

Se o topic_down for fornecido, o conector o assinará logo após a conexão bem-sucedida.

#### Publicando mensagens

Para o formato das mensagens do servidor de rede, consulte a seção correspondente da API de dados.

#### Assinando Mensagens

Para o formato das mensagens para o servidor de rede, consulte a seção correspondente da API de dados.

Você precisa enviar a mensagem JSON da API de dados adequada.

Se suas mensagens não forem JSON, elas serão descartadas silenciosamente.

### Exemplo de uso:

#### Fluxo simples, uplink, downlink_request

Sobre o que é este exemplo:

- Você possui o broker do MQTT com o seguinte URI: mqtt: //exemplo.com.br

- Você receberá mensagens de uplink no tópico /lora/uplink e mensagens de downlink_request para /lora/downlink_request

- Você enviará mensagens para o servidor de rede publicando no tópico /donwstream

O que você deveria fazer:

1. Crie um filtro no NS para os dados que você deseja receber. Selecione os tipos de uplink e downlink_response.

2. Crie uma conexão MQTT com o seguinte:

- URI = mqtt://exemplo.com.br
- Filter ID = aquele do filtro que você acabou de criar.
- Publish topic = /lora/{type}
- Subscribe topic = /downstream

3. Após a criação, o conector se conecta ao seu broker e começa a enviar mensagens.

Exemplo de mensagem de uplink:

> Topic: /lora/uplink

JSON
----

```json
{
  "params": {
    "payload": "MzQ3NjcwNjFiNDc3NGU2ZmFiZjBhNmY4YTJjYmI0Y2M=",
    "port": 7,
    "duplicate": false,
    "counter_up": 3,
    "rx_time": 1532073817.157281,
    "encrypted_payload": "pLgR8Tzh3JptkhtozJ5OlFuS3zQCygWD5hmx9zMjLnU="
  },
  "meta": {
    "network": "e23d2f31af81b25ef50375b5b7810c52",
    "packet_hash": "73465c1ed0cae413816d0f78baf3dcc2",
    "application": "1293e9e373666fd5",
    "device_addr": "d242b7a6",
    "time": 1532073817.175208,
    "device": "b2b48f713c2f973d",
    "packet_id": "f577207419bb4701ff9f7874c2e2808e",
    "gateway": "92a199d4e41ab64b"
  },
  "type": "uplink"
}
```

Exemplo de mensagem downlink_request e resposta de volta da mensagem com downlink_response:

> Topic: /lora/downlink_request

JSON
----

```json
{
  "params": {
    "counter_down": 3,
    "max_size": 51,
    "tx_time": 1532075747.295559
  },
  "meta": {
    "network": "12b5d8a8df8d9255c65d6d565d836a9d",
    "packet_hash": "cf59f7bf410a9eb23383f41342c3c7fe",
    "application": "6264dd6a1b4e9ca1",
    "device_addr": "f22eef89",
    "time": 1532075746.335046,
    "device": "c20ba71a9affafc6",
    "packet_id": "a8b464039cca609bed00f8ec58f494fe",
    "gateway": "524d07d7ef40dea3"
  },
  "type": "downlink_request"
}
```

>
< Publish: /dowstream

JSON
----

```json
{
  "meta": {
    "application": "6264dd6a1b4e9ca1", 
    "device": "c20ba71a9affafc6", 
    "device_addr": "f22eef89", 
    "gateway": "524d07d7ef40dea3", 
    "network": "12b5d8a8df8d9255c65d6d565d836a9d", 
    "packet_hash": "cf59f7bf410a9eb23383f41342c3c7fe", 
    "packet_id": "a8b464039cca609bed00f8ec58f494fe", 
    "time": 1532075746.335046
  }, 
  "params": {
    "counter_down": 3, 
    "payload": "220de733f4", 
    "port": 50
  }, 
  "type": "downlink_response"
}
```

### Classe C downlink_claim

Para enviar uma mensagem de downlink da classe C, você precisa enviar uma mensagem de downlink_claim

>
< Publish: /dowstream

JSON
----

```json
{
    "meta": {
        "device": "d2953b67bca671a6", 
        "network": "12024f9efc46a98120a6fac272a9c3a4"
    }, 
    "type": "downlink_claim"
}
```

### MyDevices (Meus dispositivos)

Este conector permite conectar o servidor de rede aos MyDevices.

Este conector propaga apenas mensagens de uplink e não duplicada.

| Argumento | Requerido | Descrição |
| ------------ | ------------ | ------------ |
| description | não | Descrição da conexão. |
| filter | sim | O ID do filtro do servidor de rede. |

#### Lista de controle

- Verifique se seu filtro está correto

- Verifique se o seu dispositivo está provisionado na plataforma Cayenne.

### API de uso

A API de uso foi projetada para fornecer informações de uso do serviço que poderiam ser usadas pelos sistemas de relatório e cobrança. Os relatórios de uso fornecidos pela API de uso contêm informações diferentes sobre a quantidade de mensagens de uplink e downlink consumidas, quantidade de chamadas de API produzidas, etc.

Todas as informações são agrupadas e agregadas usando horários e nome da organização.

#### Endpoints (Pontos finais)

A Everynet está operando em diferentes regiões e redes privadas. Cada região usa seu próprio URL de terminal. Regiões personalizadas e redes privadas podem obter URLs de terminal do suporte da Everynet.

Por exemplo, os pontos finais da região dos EUA, da UE e do Brasil são:

>https://ns.eu.everynet.io/api/v1.0/usage - região europeia.

>https://ns.us.everynet.io/api/v1.0/usage - região dos Estados Unidos.

>https://ns.atc.everynet.io/api/v1.0/usage - região brasileira.

#### Recursos

>
 - /api/v1.0/usage/totals - relatório de uso agregado para a organização específica ou lista de organizações.
 - /api/v1.0/usage/management - relatório de uso indicando apenas o uso da API de gerenciamento.
 - /api/v1.0/usage/data - relatório de uso indicando apenas o uso da API de dados.

Todos os relatórios podem ser produzidos com base horária, diária, mensal e trimestral. Consulte a seção Parâmetros de consulta abaixo.

#### Parâmetros de consulta

| Nome | Formato | Descrição |
| ------------ | ------------ | ------------ |
| access_token | access_token | A chave da API. Direitos de administrador necessários. Requerido. |
| from | yyyymmddHHMMSS | Hora de preparar o relatório. Incluindo a borda. Requerido. |
| to | yyyymmddHHMMSS | Tempo para preparar o relatório. NÃO incluindo a borda. Requerido. |
| group_time | quarter | month | day | hour | Agrupamento por intervalo de tempo. Opcional. Padrão para 'dia'. |
| round_time | true | false | Truncar from/to (de/para) horários para o slot group_time. Opcional. O padrão é verdadeiro. |
| with_defaults | true | false | Preencha os intervalos de tempo com 0 se nenhum uso for registrado. Opcional. O padrão é verdadeiro. |
| orgs | * | org_id [,org_id] | Apenas administrador. Lista de IDs da organização ou * para obter dados de todos. O padrão é a organização do solicitante. |

#### Formatos de relatório

A API de uso permite gerar relatórios em diferentes formatos de dados: JSON, CSV, TSV. Por favor, use o CSV caso deseje usar o Excel ou uma ferramenta similar para análises posteriores.

#### JSON

Para obter um relatório no formato JSON, use os seguintes endpoints:

>
/api/v1.0/usage/totals.json
/api/v1.0/usage/management.json
/api/v1.0/usage/data.json


Exemplo de relatório:

> /api/v1.0/usage/data.json

JSON
----

```json
[
  {
    "org_name": "Everynet",
    "total_uplinks": 8156,
    "time_slot_start": "2019-01-01 00:00:00",
    "unique_downlink_devices": 3,
    "org_plan": "prepaid",
    "unique_active_devices": 3,
    "org_id": "5a5f5dcf65eb1500057416cf",
    "unique_uplink_devices": 3,
    "total_downlinks": 73,
    "unique_uplinks": 4649,
    "time_slot_start": "2019-01-02 00:00:00",
    "duplicate_uplinks": 3507
  }
]
```

#### CSV (padrão)

>
./totals
./totals.csv
./management
./management.csv
./data
./data.csv

Exemplo de relatório:

> ./data.csv

>
Time slot starts,Time slot ends,Organization ID,Organization Name,Organization Plan,Unique active devices,Unique uplink devices,Unique downlink devices,Unique uplinks,Duplicate uplinks,Total uplinks,Total downlinks
2019-01-01 00:00:00,2019-01-02 00:00:00,5a5f5dcf65eb1500057416cf,Everynet,prepaid,3,3,3,4649,3507,8156,73

#### TSV

>
./totals.tsv
./management.tsv
./data.tsv

Exemplo de relatório:

> ./data.tsv

>
Time slot starts    Time slot ends    Organization ID    Organization Name    Organization Plan    Unique active devices    Unique uplink devices    Unique downlink devices    Unique uplinks    Duplicate uplinks    Total uplinks    Total downlinks
2019-01-01 00:00:00    2019-01-02 00:00:00    5a5f5dcf65eb1500057416cf    Everynet    prepaid    3    3    3    4649    3507    8156    73


#### Relatórios de conteúdo

Todos os resultados contêm linhas classificadas por (time_slot_start, org, org_plan). Os nomes das organizações são preenchidos usando os valores mais recentes.

#### Uso de dados

> ./data.*

| Nome coluna | ID coluna | Formato | Exemplo |
| ------------ | ------------ | ------------ | ------------ |
| Time slot starts | time_slot_start | String | 2019-01-01 00:00:00 |
| Time slot ends | time_slot_end | String | 2019-01-02 00:00:00 |
| Organization ID | org_id | String | 5a5f5dcf65eb1500057416cf |
| Organization Name | org_name | String | Everynet |
| Organization Plan | org_plan | String | prepaid |
| Unique active devices | unique_active_devices | Integer | 23 |
| Unique uplink devices | unique_uplink_devices | Integer | 23 |
| Unique downlink devices | unique_downlink_devices | Integer | 5 |
| Unique uplinks | unique_uplinks | Integer | 1000 |
| Duplicate uplinks | duplicate_uplinks | Integer | 400 |
| Total uplinks | total_uplinks | Integer | 1400 |
| Total downlinks | total_downlinks | Integer | 50 |

#### Uso de gerenciamento

> ./management.*

| Nome coluna | ID da coluna | Formato | Exemplo |
| ------------ | ------------ | ------------ | ------------ |
| Time slot starts | time_slot_start | String | 2019-01-01 00:00:00 |
| Time slot ends | time_slot_end | String | 2019-01-02 00:00:00 |
| Organization ID | org_id | String | 5a5f5dcf65eb1500057416cf |
| Organization Name | org_name | String | Everynet |
| Organization Plan | org_plan | String | prepaid |
| Devices created | devices_created | Integer | 4 |
| Devices updated | devices_updated | Integer | 13 |
| Devices deleted | devices_deleted | Integer | 2 |
| Devices total minimum | devices_total_min | Integer | 330 |
| Devices total maximum | devices_total_max | Integer | 334 |
| Devices total before | devices_total_before | Integer | 332 |
| Devices total after | devices_total_after | Integer | 332 |
| Filters created | filters_created | Integer | 1 |
| Filters updated | filters_updated | Integer | 2 |
| Filters deleted | filters_deleted | Integer | 0 |
| Filters total minimum | filters_total_min | Integer | 3 |
| Filters total maximum | filters_total_max | Integer | 4 |
| Filters total before | filters_total_before | Integer | 3 |
| Filters total after | filters_total_after | Integer | 4 |
| Keys created | keys_created | Integer | 0 |
| Keys updated | keys_updated | Integer | 0 |
| Keys deleted | keys_deleted | Integer | 0 |
| Keys total minimum | keys_total_min | Integer | 3 |
| Keys total maximum | keys_total_max | Integer | 3 |
| Keys total before | keys_total_before | Integer | 3 |
| Keys total after | keys_total_after | Integer | 3 |
| Users created | users_created | Integer | 1 |
| Users updated | users_updated | Integer | 0 |
| Users deleted | users_deleted | Integer | 0 |
| Users total minimum | users_total_min | Integer | 2 |
| Users total maximum | users_total_max | Integer | 3 |
| Users total before | users_total_before | Integer | 2 |
| Users total after | users_total_after | Integer | 3 |

#### Uso total

Basicamente, é o uso de dados + gerenciamento ao mesmo tempo

> ./totals.*

| Nome da coluna | ID da coluna | Formato | Exemplo |
| ------------ | ------------ | ------------ | ------------ |
| Time slot starts | time_slot_start | String | 2019-01-01 00:00:00 |
| Time slot ends | time_slot_end | String | 2019-01-02 00:00:00 |
| Organization ID | org_id | String | 5a5f5dcf65eb1500057416cf |
| Organization Name | org_name | String | Everynet |
| Organization Plan | org_plan | String | prepaid |
| Unique active devices | unique_active_devices | Integer | 23 |
| Unique uplink devices | unique_uplink_devices | Integer | 23 |
| Unique downlink devices | unique_downlink_devices | Integer | 5 |
| Unique uplinks | unique_uplinks | Integer | 1000 |
| Duplicate uplinks | duplicate_uplinks | Integer | 400 |
| Total uplinks | total_uplinks | Integer | 1400 |
| Total downlinks | total_downlinks | Integer | 50 |
| Devices created | devices_created | Integer | 4 |
| Devices updated | devices_updated | Integer | 13 |
| Devices deleted | devices_deleted | Integer | 2 |
| Devices total minimum | devices_total_min | Integer | 330 |
| Devices total maximum | devices_total_max | Integer | 334 |
| Devices total before | devices_total_before | Integer | 332 |
| Devices total after | devices_total_after | Integer | 332 |
| Filters created | filters_created | Integer | 1 |
| Filters updated | filters_updated | Integer | 2 |
| Filters deleted | filters_deleted | Integer | 0 |
| Filters total minimum | filters_total_min | Integer | 3 |
| Filters total maximum | filters_total_max | Integer | 4 |
| Filters total before | filters_total_before | Integer|  3 |
| Filters total after | filters_total_after | Integer | 4 |
| Keys created | keys_created | Integer | 0 |
| Keys updated | keys_updated | Integer | 0 |
| Keys deleted | keys_deleted | Integer | 0 |
| Keys total minimum | keys_total_min | Integer | 3 |
| Keys total maximum | keys_total_max | Integer | 3 |
| Keys total before | keys_total_before | Integer | 3 |
| Keys total after | keys_total_after | Integer | 3 |
| Users created | users_created | Integer | 1 |
| Users updated | users_updated | Integer | 0 |
| Users deleted | users_deleted | Integer | 0 |
| Users total minimum | users_total_min | Integer | 2 |
| Users total maximum | users_total_max | Integer | 3 |
| Users total before | users_total_before | Integer | 2 |
| Users total after | users_total_after | Integer | 3 |

### Exemplos

Obter uso mensal para todas as organizações por 2 meses.

# http request GET


**Exemplo para obter resultados de consumo de: 01/05/2020 até: 10/05/2020.**

#### Representação em JSON

https://ns.atc.everynet.io/api/v1.0/usage/data.json?access_token=SEU_TOKEN&from=20200501000000&to=20200510000000&group_time=day

#### Representação em CSV (neste formato os dados podem ser manipulados por uma planilha do Excel)

https://ns.atc.everynet.io/api/v1.0/usage/data.csv?access_token=SEU_TOKEN&&from=20200501000000&to=20200510000000&group_time=day

*Observação: Não é permitido intervalos de tempo muito amplos.

JSON
----

```json
[
  {
    "org_name": "Everynet",
    "total_uplinks": 0,
    "time_slot_start": "2019-01-01 00:00:00",
    "unique_downlink_devices": 0,
    "org_plan": "prepaid",
    "unique_active_devices": 0,
    "org_id": "59d4d7faaabb6e00055df373",
    "unique_uplink_devices": 0,
    "total_downlinks": 0,
    "unique_uplinks": 0,
    "time_slot_end": "2019-01-02 00:00:00",
    "duplicate_uplinks": 0
  },
  {
    "org_name": "Everynet",
    "total_uplinks": 0,
    "time_slot_start": "2019-01-02 00:00:00",
    "unique_downlink_devices": 0,
    "org_plan": "prepaid",
    "unique_active_devices": 0,
    "org_id": "59d4d7faaabb6e00055df373",
    "unique_uplink_devices": 0,
    "total_downlinks": 0,
    "unique_uplinks": 0,
    "time_slot_end": "2019-01-03 00:00:00",
    "duplicate_uplinks": 0
  },
  {
    "org_name": "Everynet",
    "total_uplinks": 0,
    "time_slot_start": "2019-01-03 00:00:00",
    "unique_downlink_devices": 0,
    "org_plan": "prepaid",
    "unique_active_devices": 0,
    "org_id": "59d4d7faaabb6e00055df373",
    "unique_uplink_devices": 0,
    "total_downlinks": 0,
    "unique_uplinks": 0,
    "time_slot_end": "2019-01-04 00:00:00",
    "duplicate_uplinks": 0
  }
]
```

**Exemplo para obter resultados de consumo de: 01/05/2020 até: 10/05/2020.**

> curl -v -X GET "https://ns.atc.everynet.io/api/v1.0/usage/data.json?access_token=SEU_TOKEN&from=20200501000000&to=20200510000000&group_time=day" -H "accept: application/json"

### Exemplos de servidor de aplicativos

Aqui você pode encontrar exemplos de servidor de aplicativos implementados para diferentes APIs:

 - API de dados
 - PubNub
 - MQTT

Link: [https://github.com/everynet/app.example](https://github.com/everynet/app.example "https://github.com/everynet/app.example")

### Planos de canal.

Notas e exemplos de parâmetros de região específicos da Everynet.

 - AS923-2
 - LA915A

### AS923

Especificações específicas da Everynet AS923-2.

Os canais 0 e 1 são fixos e é obrigatório que seja implementado no dispositivo final. Outros canais configurados pelo servidor de rede usando comandos MAC durante o estágio de integração (após ingressar no OTAA ou primeiro uplink no ABP).

### Canais para Uplink:

| Canal | Frequência | Taxa de dados  | Tipo |
| ------------ | ------------ | ------------ | ------------ |
| 0 | 921.4 | 0,1,2,3,4,5 | Fixed |
| 1 | 921.6 | 0,1,2,3,4,5 | Fixed |
| 2 | 921.2 | 0,1,2,3,4,5 | |
| 3 | 921.8 | 0,1,2,3,4,5 | |
| 4 | 922.0 | 0,1,2,3,4,5 | |
| 5 | 922.2 | 0,1,2,3,4,5,6 | |
| 6 | 922.4 | 0,1,2,3,4,5 | |
| 7 | 922.6 | 7 | FSK |

Por padrão, a janela de recebimento do RX1 usa o mesmo canal que o uplink anterior.

Tempo limite do RX1 = 1s

Deslocamento do datarate RX1 = 0

A janela de recebimento do RX2 usa uma frequência e taxa de dados fixas. Os parâmetros padrão são:

921,4 MHz / DR2 (SF10/125KHz)

### Datarates:

| Índice | Largura de banda | Fator de propagação | Tamanho máximo do payload | Taxa de bits física [bit/s] |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| 0 | 125 kHz | SF12 | 59 | 250 |
| 1 | 125 kHz | SF11 | 59 | 440 |
| 2 | 125 kHz | SF10 | 59 | 980 |
| 3 | 125 kHz | SF9 | 123 | 1760 |
| 4 | 125 kHz | SF8 | 230 | 3125 |
| 5 | 125 kHz | SF7 | 230 | 5470 |
| 6 | 250 kHz | SF7 | 230 | 12500 |
| 7 | FSK | 230 | nada consta |

#### Exemplos:

Há alterações em arquivos comuns como LoRaMac.h, Region.c, CMake. Verifique todas as alterações do projeto na implementação da pilha Stackforce LoRaWAN modificada pela Everynet.

[RegionAS923-2.c](https://ns.docs.everynet.io/channel_plans/AS923/RegionAS923-2.c "RegionAS923-2.c")

Link para download:

[https://ns.docs.everynet.io/channel_plans/AS923/RegionAS923-2.c](https://ns.docs.everynet.io/channel_plans/AS923/RegionAS923-2.c "https://ns.docs.everynet.io/channel_plans/AS923/RegionAS923-2.c")


[RegionAS923-2.h](https://ns.docs.everynet.io/channel_plans/AS923/RegionAS923-2.h "RegionAS923-2.h")

Link para download:

[https://ns.docs.everynet.io/channel_plans/AS923/RegionAS923-2.h](https://ns.docs.everynet.io/channel_plans/AS923/RegionAS923-2.h "https://ns.docs.everynet.io/channel_plans/AS923/RegionAS923-2.h")

### LA915A

Implantação da Everynet do plano de canais AU915-928 para o Brasil.

Primeiros 8 canais utilizados.

ChannelsDefaultMask[0] = 0xFF;

### Canais para Uplink:

| Índice | Frequência | Taxa de dados |
| ------------ | ------------ | ------------ |
| 0 | 915.2 | 0,1,2,3,4,5 |
| 1 | 915.4 | 0,1,2,3,4,5 |
| 2 | 915.6 | 0,1,2,3,4,5 |
| 3 | 915.8 | 0,1,2,3,4,5 |
| 4 | 916.0 | 0,1,2,3,4,5 |
| 5 | 916.2 | 0,1,2,3,4,5 |
| 6 | 916.4 | 0,1,2,3,4,5 |
| 7 | 916.6 | 0,1,2,3,4,5 |

### Canais para Downlink:

| Índice | Frequência |
| ------------ | ------------ |
| 0 | 923.3 |
| 1 | 923.9 |
| 2 | 924.5 |
| 3 | 925.1 |
| 4 | 925.7 |
| 5 | 926.3 |
| 6 | 926.9 |
| 7 | 927.5 |

Frequência de downlink, na verdade, não escrita em fontes, mas calculada na configuração da janela RX1 da seguinte maneira:

923300000 + (uplink_channel_number % 8) * 600000

O canal da janela RX2 é fixo:

Frequência: 923.3 Datarate (Taxas de dados): 8.

Atraso de recebimento para a janela RX1: 5 segundos.

Atraso de recebimento para a janela RX2: 6 segundos.

Tempo de espera padrão do uplink: 0.

Tempo de espera padrão do downlink: 0.

#### Datarates (Taxas de dados)

| Índice | Largura de banda | Fator de espalhamento | Tamanho máximo do payload | Taxa de bits física [bit/s] |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| 0 | 125 kHz | SF12 | 51 | 250 |
| 1 | 125 kHz | SF11 | 51 | 440 |
| 2 | 125 kHz | SF10 | 51 | 980 |
| 3 | 125 kHz | SF9 | 115 | 1760 |
| 4 | 125 kHz | SF8 | 242 |3125 |
| 5 | 125 kHz | SF7 | 242 | 5470 |
| 6 | 500 kHz | SF8 | 242 | 12500 |

### Exemplos:

[RegionLA915.c](https://ns.docs.everynet.io/channel_plans/la915a/RegionLA915.c "RegionLA915.c")

Link para download:

[https://ns.docs.everynet.io/channel_plans/la915a/RegionLA915.c](https://ns.docs.everynet.io/channel_plans/la915a/RegionLA915.c "https://ns.docs.everynet.io/channel_plans/la915a/RegionLA915.c")

[RegionLA915.h](https://ns.docs.everynet.io/channel_plans/la915a/RegionLA915.h "RegionLA915.h")

Link para download:

[https://ns.docs.everynet.io/channel_plans/la915a/RegionLA915.h](https://ns.docs.everynet.io/channel_plans/la915a/RegionLA915.h "https://ns.docs.everynet.io/channel_plans/la915a/RegionLA915.h")

Há alterações em arquivos comuns como LoRaMac.h, Region.c, CMake. Verifique todas as alterações do projeto na implementação da pilha Stackforce LoRaWAN modificada pela Everynet.

### Stackforce

Implementação de pilha Semtech\Stackforce LoRaWAN modificada pela Everynet - adicionado planos de canais AS923-2 (indonésio) e LA915 (brasileiro).

Baseado no hash de confirmação da ramificação principal: e33839f4b650e951a3aa2068315bc7bc5a3607a8


[LoRaMac-node_Everynet_modified.zip](https://ns.docs.everynet.io/channel_plans/Stackforce/LoRaMac-node_Everynet_modified.zip "LoRaMac-node_Everynet_modified.zip")

Link Download:

[https://ns.docs.everynet.io/channel_plans/Stackforce/LoRaMac-node_Everynet_modified.zip](https://ns.docs.everynet.io/channel_plans/Stackforce/LoRaMac-node_Everynet_modified.zip "https://ns.docs.everynet.io/channel_plans/Stackforce/LoRaMac-node_Everynet_modified.zip")

Alterne para ramificar everynet para usar modificações.

Testado com placas NUCLEO-L073 (LA) e B-L072Z-LRWAN1 (AS).

Kit de Ferramentas: CMake (3.16.0)

Toolchain: GCC para arm-none-eabi 8.3.1

IDE: VSCode (1.42.1)

SO: Windows_NT x64

#### Como construir.

Instale [VSCode](https://code.visualstudio.com/ "VSCode"), [GNU ARM Toolchain](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain "GNU ARM Toolchain"), [CMake](https://cmake.org/ "CMake").

VSCode  

Link: [https://code.visualstudio.com/](https://code.visualstudio.com/ "https://code.visualstudio.com/")

GNU ARM ToolChain

Link: [https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain "https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain")

CMake

Link: [https://cmake.org/](https://cmake.org/ "https://cmake.org/")

No VSCode. Vá para as extensões, pesquise e instale a seguir:

 - C/C ++
 - CMake Tools
 - vá para .vscode \ settings.json
 - edit TOOLCHAIN_PREFIX - defina o caminho para a pasta de instalação do GNU ARM Toolchain

## Problemas (nada consta)

## Publicado com GitBook
Link: [https://www.gitbook.com/](https://www.gitbook.com/ "https://www.gitbook.com/")
