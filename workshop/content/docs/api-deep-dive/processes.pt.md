---
title: OGC API - Processes
---

# OGC API - Processes

!!! abstract "Público-alvo"
    Estudantes familiarizados com serviços web e APIs, que desejam ter
    uma visão geral do standard OGC API - Processes

!!! abstract "Objetivos de Aprendizagem"
    Ao concluir o módulo, os estudantes serão capazes de:

    - Explicar o que é o standard OGC API - Processes
    - Descrever o que pode ser feito com implementações do OGC API - Processes
    - Compreender os principais recursos oferecidos por implementações do OGC API - Processes
    - Compreender como obter uma descrição das capacidades de uma implementação do OGC API - Processes
    - Compreender como fazer pedidos a uma implementação do OGC API - Processes
    - Conseguir encontrar um endpoint do OGC API - Processes e utilizá-lo através de um cliente

## Introdução

O [OGC API - Processes](https://ogcapi.ogc.org/processes) é um standard que suporta a integração de
tarefas computacionais em processos executáveis que podem ser oferecidos por um
servidor através de uma API Web e invocar por uma aplicação cliente. O
standard especifica uma interface de processamento para comunicar sobre um protocolo
RESTful utilizando codificações em JavaScript Object Notation (JSON). O standard
aproveita conceitos do Standard OGC Web Processing Service (WPS) 2.0
Interface, mas não exige a implementação de um WPS. A parte Core do standard é designada **OGC API - Processes - Parte 1:
Core**. A parte Core do standard suporta a integração de
tarefas computacionais em processos executáveis que podem ser oferecidos por um
servidor através de uma API Web e invocar por uma aplicação cliente, quer
sincronamente quer assincronamente. Exemplos de processos computacionais
que podem ser suportados por implementações desta especificação incluem
álgebra raster, buffering de geometria, geometria de área construtiva, roteamento,
análise de imagens e vários outros.

!!! note
    Este módulo tutorial não tem a intenção de substituir o standard efetivo do
    **OGC API - Processes - Parte 1: Core**. O tutorial
    concentra-se intencionalmente num subconjunto de capacidades para permitir que o
    estudante comece a utilizar o standard. Consulte o standard do **OGC API -
    Processes - Parte 1: Core** para mais detalhes.

### Antecedentes

> Histórico

  Vários dos conceitos especificados no OGC API - Processes tiveram origem no trabalho de especificação de uma interface RESTful para o WPS 2.0. A partir de fevereiro de 2019, todo o trabalho relativo a uma interface RESTful para o WPS 2.0 passou a focar-se no OGC API - Processes.

> Versões

  A versão 1.0.0 do **OGC API - Processes - Parte 1: Core** é a versão mais recente

> Suite de testes

  Estão disponíveis suites de testes para:

  * OGC API - Processes - Parte 1

  Todas as suites de testes estão disponíveis no [OGC Validator](https://cite.ogc.org/teamengine/).

> Implementações

  As implementações podem ser encontradas na [página de implementações](https://github.com/opengeospatial/ogcapi-processes/blob/master/implementations.adoc).

#### Utilização

O **OGC API - Processes - Parte 1: Core** suporta a integração de
tarefas computacionais em processos executáveis que podem ser oferecidos por um
servidor através de uma API Web e invocar por uma aplicação cliente.
Agências governamentais, organizações privadas e institutos académicos utilizam
o standard OGC API - Processes para fornecer implementações de
algoritmos geoespaciais que processam dados. A vantagem disto é que o
processamento de dados geoespaciais, incluindo dados de sensores, pode ser
distribuído, permitindo maior capacidade para processar quantidades maiores
de dados.

Para além da parte aprovada acima, o Standards Working Group (SWG) do OGC API - Processes está a trabalhar nos seguintes rascunhos:

* *Rascunho* **OGC API - Processes - Parte 2: Deploy, Replace, Undeploy** estende as capacidades básicas especificadas na Parte 1 com a capacidade de adicionar, modificar e/ou eliminar processos individuais de forma dinâmica utilizando uma implementação (endpoint) do Standard OGC API - Processes.

* *Rascunho* **OGC API - Processes - Parte 3: Workflows and Chaining** estende as capacidades básicas especificadas na Parte 1 com a capacidade de encadear processos aninhados, referenciar processos tanto locais como externos e coleções de dados acessíveis via standards OGC API como entradas para um processo, e ativar a execução de processos através de especificações de entrega de dados OGC API, como OGC API - Tiles, DGGS, Coverages, Features, EDR e Maps.

#### Relação com outros standards da OGC

-   OGC Web Processing Service Interface Standard (WPS): O standard WPS
    fornece uma interface standard que simplifica a tarefa de
    tornar serviços de processamento geoespacial computacional, simples ou complexos, acessíveis via serviços web. O Standard OGC API - Processes
    é uma forma mais recente e moderna de programar e
    interagir com recursos na web, permitindo melhor
    integração com pacotes de software existentes. O Standard OGC
    API - Processes aborda todos os casos de utilização que foram
    abordados pelo Standard WPS, aproveitando também a especificação
    OpenAPI e uma abordagem orientada a recursos.

### Visão geral dos recursos

O **OGC API - Processes - Parte 1: Core** define os recursos listados na
tabela seguinte.

<table>
  <tr>
    <th>Recurso</th>
    <th>Método</th>
    <th>Caminho</th>
    <th>Propósito</th>
  </tr>
  <tr>
    <td>Landing page</td>
    <td>GET</td>
    <td>/</td>
    <td>Este é o recurso de nível superior, que serve como ponto de entrada.</td>
  </tr>
  <tr>
    <td>Declaração de conformidade</td>
    <td>GET</td>
    <td>/conformance</td>
    <td>Este recurso apresenta informação sobre a funcionalidade que é implementada pelo servidor.</td>
  </tr>
  <tr>
    <td>Definição da API</td>
    <td>GET</td>
    <td>/api</td>
    <td>Este recurso fornece metadados sobre a API propriamente dita. Note que a utilização de /api no servidor é opcional e a definição da API pode estar alojada num servidor completamente separado.</td>
  </tr>
  <tr>
    <td>Lista de processos</td>
    <td>GET</td>
    <td>/processes </td>
    <td>Identificadores de processos, ligações para descrições de processos.</td>
  </tr>
  <tr>
    <td>Descrição do processo </td>
    <td>GET</td>
    <td>/processes/{processID}</td>
    <td>Recupera uma descrição do processo.</td>
  </tr>
  <tr>
    <td>Execução do processo</td>
    <td>POST</td>
    <td>/processes/{processID}/execution</td>
    <td>Cria e executa um trabalho.</td>
  </tr>
  <tr>
    <td>Informação de estado do trabalho</td>
    <td>GET</td>
    <td>/jobs/{jobID}</td>
    <td>Recupera informação sobre o estado de um trabalho.</td>
  </tr>
    <td>Resultados do trabalho</td>
    <td>GET</td>
    <td>/jobs/{jobID}/results</td>
    <td>Recupera o(s) resultado(s) de um trabalho.</td>
  </tr>
  <tr>
    <td>Lista de trabalhos</td>
    <td>GET</td>
    <td>/jobs</td>
    <td>Recupera a lista de trabalhos.</td>
  </tr>
  <tr>
    <td>Eliminação de trabalho</td>
    <td>DELETE</td>
    <td>/jobs/{jobID} </td>
    <td>Cancela e elimina um trabalho.</td>
  </tr>
</table>

### Exemplo

O [servidor de demonstração](https://demo.pygeoapi.io/master) oferece e executa vários processos através de uma interface que está em conformidade com o OGC API - Processes.

Um exemplo de pedido que pode ser utilizado para navegar em todos os processos disponíveis encontra-se em <https://demo.pygeoapi.io/master/processes>.

Note que a resposta ao pedido é HTML neste caso.

Alternativamente, os mesmos dados podem ser recuperados no formato GeoJSON, através do pedido https://demo.pygeoapi.io/master/processes?f=json

## Recursos

### Landing page

Dado que o OGC API - Processes utiliza o OGC API - Common e o OGC API - Features como blocos de construção, consulte o [OGC API - Features](features.md#landing-page) para
uma explicação detalhada.

### Declarações de conformidade

Dado que o OGC API - Processes utiliza o OGC API - Common e o OGC API - Features como blocos de construção, consulte o [OGC API - Features](features.md#conformance-declarations) para
uma explicação detalhada.

### Definição da API

Dado que o OGC API - Processes utiliza o OGC API - Common como bloco de construção, consulte o [OGC API - Features](features.md#api-definition) para
uma explicação detalhada de uma implementação de exemplo.

### Lista de processos

Os processos oferecidos através de uma implementação do **OGC API - Processes** são organizados num ou mais processos. O endpoint
`/processes` fornece informação sobre e acesso à lista de processos.

Para cada processo, existe uma ligação para a descrição detalhada do
processo (representada pelo caminho **/processes/{processId}** e
relação de ligação **self**. Além disso, existem ligações para executar o
processo, bem como a lista de trabalhos resultantes da execução do processo.

A informação do processo inclui também se o processo pode ser executado em modo
síncrono e/ou assíncrono (opções de controlo de trabalho). O modo assíncrono é valioso
para executar trabalhos de longa duração sem bloquear o fluxo de trabalho de pedido/resposta HTTP.
Isto também significa que o cliente pode voltar a verificar o estado do trabalho e o
resultado assim que este estiver concluído.

Finalmente, existem definições para a estrutura de entrada necessária para executar o processo
(expressa como JSON Schema), bem como a estrutura de saída que o cliente deve esperar
quando recebe uma resposta da execução do processo.

Abaixo segue um excerto da resposta ao pedido
<https://demo.pygeoapi.io/master/processes?f=json>

```json
{
    "version": "0.2.0",
    "id": "hello-world",
    "title": "Hello World",
    "description": "An example process that takes a name as input, and echoes it back as output. Intended to demonstrate a simple process with a single literal input.",
    "jobControlOptions":[
        "sync-execute",
        "async-execute"
    ],
    "keywords":[
        "hello world",
        "example",
        "echo"
    ],
    "links":[
        {
            "type": "text/html",
            "rel": "about",
            "title": "information",
            "href": "https://example.org/process",
            "hreflang": "en-US"
        },
        {
            "type": "application/json",
            "rel": "self",
            "href": "https://demo.pygeoapi.io/master/processes/hello-world?f=json",
            "title": "Process description as JSON",
            "hreflang": "en-US"
        },
        {
            "type": "text/html",
            "rel": "alternate",
            "href": "https://demo.pygeoapi.io/master/processes/hello-world?f=html",
            "title": "Process description as HTML",
            "hreflang": "en-US"
        },
        {
            "type": "text/html",
            "rel": "http://www.opengis.net/def/rel/ogc/1.0/job-list",
            "href": "https://demo.pygeoapi.io/master/jobs?f=html",
            "title": "jobs for this process as HTML",
            "hreflang": "en-US"
        },
        {
            "type": "application/json",
            "rel": "http://www.opengis.net/def/rel/ogc/1.0/job-list",
            "href": "https://demo.pygeoapi.io/master/jobs?f=json",
            "title": "jobs for this process as JSON",
            "hreflang": "en-US"
        },
        {
            "type": "application/json",
            "rel": "http://www.opengis.net/def/rel/ogc/1.0/execute",
            "href": "https://demo.pygeoapi.io/master/processes/hello-world/execution?f=json",
            "title": "Execution for this process as JSON",
            "hreflang": "en-US"
        }
    ],
    "inputs":{
        "name":{
            "title": "Name",
            "description": "The name of the person or entity that you wish tobe echoed back as an output",
            "schema":{
                "type": "string"
            },
            "minOccurs":1,
            "maxOccurs":1,
            "metadata":null,
            "keywords":[
                "full name",
                "personal"
            ]
        },
        "message":{
            "title": "Message",
            "description": "An optional message to echo as well",
            "schema":{
                "type": "string"
            },
            "minOccurs":0,
            "maxOccurs":1,
            "metadata":null,
            "keywords":[
                "message"
            ]
        }
    },
    "outputs":{
        "echo":{
            "title": "Hello, world",
            "description": "A \"hello world\" echo with the name and (optional) message submitted for processing",
            "schema":{
                "type": "object",
                "contentMediaType": "application/json"
            }
        }
    },
    "example":{
        "inputs":{
            "name": "World",
            "message": "An optional message."
        }
    },
    "outputTransmission":[
        "value"
    ]
}
```

### Descrição do processo

O exemplo anterior demonstrou informação do processo para todos os processos oferecidos por um servidor OGC API - Processes. Para aceder à informação do processo de um único processo, execute o seguinte pedido no servidor de demonstração:

<https://demo.pygeoapi.io/master/processes/hello-world?f=json>

!!! note
    A informação de um único processo exige o identificador do processo como parte do URL

### Execução do processo

Agora que temos a informação adequada do processo, podemos executar o processo. A execução do processo
exige que os pedidos sejam executados com HTTP POST, com um payload conforme especificado/exigido pelo servidor (JSON).

!!! note
    Os navegadores web não conseguem facilmente fazer pedidos HTTP POST, pelo que utilizamos o comando [curl](https://curl.se).
    Pode utilizar qualquer ferramenta que seja capaz de executar pedidos HTTP POST conforme indicado abaixo.

```bash
curl -X 'POST' \
  'https://demo.pygeoapi.io/master/processes/hello-world/execution' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "inputs": {
    "message": "Great to see you here",
    "name": "OGC API workshop participant"
  }
}'
```

O servidor irá responder com uma resposta imediata (modo síncrono por predefinição), conforme abaixo:

```json
{
    "id": "echo",
    "value": "Hello OGC API workshop participant! Great to see you here"
}
```

Para executar o mesmo processo em modo assíncrono, precisamos de adicionar o cabeçalho
HTTP **Prefer: respond-async**. Além disso, a resposta a uma execução assíncrona do processo é sempre vazia, sendo
que o cabeçalho HTTP **Location** contém um URL para a informação do trabalho resultante.


!!! note
    Adicionamos a opção `-v` ao comando curl abaixo para podermos inspecionar os cabeçalhos de resposta

```bash
curl -v -X 'POST' \
  'https://demo.pygeoapi.io/master/processes/hello-world/execution' \
  -H 'Prefer: respond-async' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "inputs": {
    "message": "Great to see you here",
    "name": "OGC API workshop participant"
  }
}'
```

Um excerto da resposta mostra o cabeçalho HTTP **Location** (localização):

```bash
< HTTP/2 201 
< access-control-allow-origin: *
< content-language: en-US
< content-type: application/json
< date: Mon, 04 Dec 2023 16:33:06 GMT
< location: https://demo.pygeoapi.io/master/jobs/cdbc641c-92c2-11ee-9c88-0242ac120003
< preference-applied: respond-async
< server: gunicorn
< x-powered-by: pygeoapi 0.16.dev0
< content-length: 4
```

!!! note
    O URL do cabeçalho HTTP `location` será sempre único

### Informação de estado do trabalho

Utilizando o URL do cabeçalho HTTP `location` acima, podemos inspecionar o estado do trabalho:

<https://demo.pygeoapi.io/master/jobs/cdbc641c-92c2-11ee-9c88-0242ac120003?f=json>

```json
{
    "processID": "hello-world",
    "jobID": "cdbc641c-92c2-11ee-9c88-0242ac120003",
    "status": "successful",
    "message": "Job complete",
    "progress":100,
    "parameters":null,
    "job_start_datetime": "2023-12-04T16:33:06.806485Z",
    "job_end_datetime": "2023-12-04T16:33:06.812615Z",
    "links":[
        {
            "href": "https://demo.pygeoapi.io/master/jobs/cdbc641c-92c2-11ee-9c88-0242ac120003/results?f=html",
            "rel": "about",
            "type": "text/html",
            "title": "results of job cdbc641c-92c2-11ee-9c88-0242ac120003 as HTML"
        },
        {
            "href": "https://demo.pygeoapi.io/master/jobs/cdbc641c-92c2-11ee-9c88-0242ac120003/results?f=json",
            "rel": "about",
            "type": "application/json",
            "title": "results of job cdbc641c-92c2-11ee-9c88-0242ac120003 as JSON"
        }
    ]
}
```

### Resultados do trabalho

Aqui vemos que o trabalho foi totalmente executado e concluído, mas não contém os resultados efetivos. Para inspecionar
os resultados efetivos, utilizamos os objetos de ligação que fornecem os resultados de acordo:

<https://demo.pygeoapi.io/master/jobs/cdbc641c-92c2-11ee-9c88-0242ac120003/results?f=json>

!!! note
    Vemos que os resultados dos pedidos/respostas síncronos e assíncronos são idênticos e
    que apenas o controlo de execução é diferente.


### Lista de trabalhos

Da mesma forma que um servidor OGC API - Processes fornece acesso à informação de processo de todos os seus
processos, o servidor fornece o mesmo para todos os seus trabalhos (de qualquer processo), utilizando o seguinte URL:

<https://demo.pygeoapi.io/master/jobs?f=json>

### Eliminação de trabalho

Se quisermos eliminar um determinado trabalho, podemos executar um pedido HTTP DELETE contra o ID do trabalho.

!!! note
    Os navegadores web não conseguem facilmente fazer pedidos HTTP DELETE, pelo que utilizamos o comando [curl](https://curl.se).
    Pode utilizar qualquer ferramenta que seja capaz de executar pedidos HTTP DELETE conforme indicado abaixo.

```bash
curl -X 'DELETE' https://demo.pygeoapi.io/master/jobs/cdbc641c-92c2-11ee-9c88-0242ac120003
```

!!! note
    Experimente executar um HTTP GET no trabalho que foi apenas eliminado e verifique que já não existe (HTTP 404).

!!! note
    Alguns servidores podem implementar controlo de acesso para prevenir a eliminação errónea ou não desejada de um trabalho ou
    outro recurso.

## Resumo

O standard OGC API - Processes permite a execução de processos computacionais e a recuperação de metadados que descrevem o propósito e a funcionalidade dos processos. Este aprofundamento proporcionou uma introdução ao standard e uma visão geral dos vários endpoints, que permitem monitorizar, criar, atualizar e eliminar esses processos num servidor.
