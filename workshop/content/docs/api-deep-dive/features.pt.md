---
title: Features
---

```json
[


    [


# OGC API - Features[](#ogc-api-features)

Público-alvo
Estudantes que estão familiarizados com serviços web e APIs, e querem ter
uma visão geral do padrão OGC API - Features

Objetivos de Aprendizagem
No final do módulo os estudantes serão capazes de:

Explicar o que é o padrão OGC API - Features
Descrever o que pode ser feito com implementações OGC API - Features
Compreender os principais recursos oferecidos por implementações de OGC API - Features
Compreender como obter uma descrição das capacidades de uma implementação de OGC API - Features
Compreender como emitir pedidos a uma implementação de OGC API - Features
Ser capaz de encontrar um endpoint OGC API - Features e usá-lo através de um cliente

## Introdução[](#introducao)

[OGC API - Features](https://ogcapi.ogc.org/features) é um padrão que fornece
uma família de interfaces leves para acesso a dados geoespaciais.
O padrão, que também é chamado de API OGC API - Features, aborda duas operações fundamentais; descoberta e consulta.
Operações de descoberta permitem que a API seja interrogada para determinar as suas
capacidades e recuperar informação (metadados) sobre esta distribuição
de um recurso. Isto inclui a definição da API do servidor bem como
metadados sobre os recursos de dados geoespaciais fornecidos pelo servidor.
Operações de consulta permitem que os recursos de dados geoespaciais sejam recuperados da
base de dados subjacente com base em critérios de seleção simples, definidos
por este padrão e selecionados pelo cliente.

Note
Este módulo de tutorial não tem a intenção de ser uma substituição ao
OGC API - Features padrão. O tutorial
foca intencionalmente num subconjunto de capacidades a fim de fazer com que o
estudante comece a usar o padrão. Por favor consulte o [OGC API -
Features padrão](https://docs.ogc.org/is/19-069/19-069.html) para mais detalhes.

### Antecedentes[](#antecedentes)

História

A versão 1.0.0 foi publicada em 2020-02-01.

Versões

A versão 1.0.0 do OGC API - Features - Parte 1: Núcleo é a versão mais recente atual

Suite de testes

Uma suite de testes está disponível para:

OGC API - Features - Parte 1
OGC API - Features - Parte 2

Todas as suites de testes estão disponíveis no [Validador OGC](https://cite.ogc.org/teamengine/).  

Implementações

Implementações podem ser encontradas na [página de implementações](https://github.com/opengeospatial/ogcapi-features/tree/master/implementations).

#### Utilização[](#utilizacao)
OGC API - Features fornece uma família de
interfaces de consulta leves para aceder a recursos de dados geoespaciais
requisitando dados em entidades ou coleções de entidades. Um recurso de dados geoespaciais é uma coleção de
dados geoespaciais que podem ser amostrados usando os padrões de consulta de entidades da API.

O padrão fornece uma interface padrão para requisitar dados
geoespaciais vetoriais consistindo em entidades geográficas e as suas propriedades.
O benefício disto é que as aplicações cliente podem requisitar dados de origem
de múltiplas implementações da API, e depois renderizar os dados para
exibição ou processar os dados ulteriormente como parte de um fluxo de trabalho. O padrão
permite que os dados sejam acedidos consistentemente com outros dados. As propriedades de entidades
codificadas usando tipos de dados comuns como strings de texto, data
e hora também podem ser acedidas consistentemente.

#### Relação com outros padrões OGC[](#relacao-com-outros-padroes-ogc)

OGC API - Common: O OGC API - Features usa OGC API - Common como bloco de construção.
Serviço Web de Entidades (WFS): A API OGC API - Features é completamente compatível com o WFS, no sentido em que suporta Entidades e Propriedades de Entidades. Estende a funcionalidade WFS permitindo 'Coleções', uma forma de 'coleção de coleções'. A API OGC API - Features também suporta a recuperação de dados spatiotemporais por localização nomeada bem como coordenadas.
Serviço Web de Cobertura (WCS): O mecanismo de mensagem primário da API OGC API - Features é JSON, incluindo GeoJSON, sobre HTTP(S). As implementações da API OGC API - Features são descritas usando a especificação OpenAPI V3.0. A API OGC API - Features é consistente com os padrões WCS mas não requer que o utilizador final ou desenvolvedor use os termos Domain e RangeSet. A API OGC API - Features também pode ser usada para gerar uma única consulta contra uma coleção de coberturas, fornecendo que os sistemas de referência de coordenadas de dados sejam consistentes.
Sensor Observation Service (SOS): A API OGC API - Features permite a recuperação de dados de cobertura e respostas HTML - ambos não são suportados pelo padrão SOS. Além disso, as implementações SOS usam a operação GetCapabilities para fornecer descrições de recursos disponíveis. Em contraste, a API OGC API - Features usa documentos de definição OpenAPI para descrever interfaces disponíveis.

### Visão geral de Recursos[](#visao-geral-de-recursos)

O Padrão OGC API - Features define os
recursos listados na tabela seguinte.

Visão geral dos recursos OGC API - Features

    Recurso
    Método
    Caminho
    Propósito

    Página inicial
    GET
    /
    Este é o recurso de nível superior, que serve como ponto de entrada.

    Declaração de conformidade
    GET
    /conformance
    Este recurso apresenta informação sobre a funcionalidade que está implementada pelo servidor.

    Definição da API
    GET
    /api
    Este recurso fornece metadados sobre a API em si. Note que o uso de /api no servidor é opcional e a definição da API pode ser alojada num servidor completamente separado.

    Metadados de coleções
    GET
    /collections
    Metadados descrevendo as coleções de dados disponíveis desta API.

    Metadados de Coleção Única
    GET
    /collections/{collectionId}
    Metadados descrevendo a coleção de dados que tem o identificador único {collectionId}.

    Metadados de Itens
    GET
    /collections/{collectionId}/items
    Recupera metadados sobre itens disponíveis.

    Item único
    GET
    /collections/{collectionId}/items/{itemId}
    Recupera um item único de uma coleção.

### Exemplo[](#exemplo)

Este [servidor de demonstração](https://demo.pygeoapi.io/master) publica
dados geoespaciais através de uma interface que é conforme com o padrão OGC API -
Features. Uma aplicação cliente está disponível
[aqui](https://demo.pygeoapi.io/master/collections?f=html) .

Um exemplo de pedido que pode ser usado para recuperar dados da coleção de estradas
[encontra-se aqui](https://demo.pygeoapi.io/master/collections/roads/items?limit=1)

Note que a resposta ao pedido é GeoJSON, neste caso o formato de saída predefinido e único suportado.

## Recursos[](#recursos)

Esta secção fornece informação básica sobre os tipos de recursos
que OGC API - Features oferece.

Cada recurso fornece ligações que se relacionam com recursos. Isto permite
que uma aplicação cliente navegue pelos recursos, a partir da página inicial
até às entidades individuais. O servidor identifica a
relação entre um recurso e outros recursos ligados através de um
tipo de relação de ligação, representado pelo atributo rel. Os tipos de
relação de ligação usados por implementações do OGC API - Features
podem ser encontrados na [Secção
8.1](https://docs.ogc.org/is/19-069/19-069.html#toc17) do
padrão.

### Página inicial[](#pagina-inicial)

A página inicial é o recurso de nível superior que serve como ponto de
entrada. Uma aplicação cliente precisa de conhecer a localização da página inicial
do servidor. A partir da página inicial, a aplicação cliente pode
recuperar ligações para os caminhos de Declaração de Conformidade, Coleção e Definição da API. Um exemplo de página inicial está em
[https://demo.pygeoapi.io/master](https://demo.pygeoapi.io/master)

A ligação para a Definição da API é identificada através do
tipo de relação de ligação service-desc e service-doc.

A ligação para a Declaração de Conformidade é identificada através do
tipo de relação de ligação conformance.

A ligação para as Coleções é identificada através do tipo de relação
de ligação data.

Um extrato da página inicial de um servidor de demonstração é mostrado abaixo.

{
  &quot;title&quot;: &quot;pygeoapi master demo instance&quot;,
  &quot;description&quot;: &quot;A lightweight (NoSQL) TILES compliant, Functions as a Service (FaaS), cloud native geospatial API engine&quot;,
  &quot;keywords&quot;: [
    &quot;pygeoapi&quot;,
    &quot;geoprocessing&quot;,
    &quot;ogcapi&quot;,
    &quot;tiles&quot;,
    &quot;functions&quot;,
    &quot;serverless&quot;,
    &quot;cloud native&quot;,
    &quot;NoSQL&quot;,
    &quot;geospatial&quot;,
    &quot;api&quot;
  ],
  &quot;keywords_format&quot;: &quot;comma-separated&quot;,
  &quot;theme&quot;: &quot;https://demo.pygeoapi.io/master/assets/images/pygeoapi_icon.png&quot;,
  &quot;logo&quot;: &quot;https://demo.pygeoapi.io/master/assets/images/pygeoapi_icon.png&quot;,
  &quot;type&quot;: &quot;API&quot;,
  &quot;apis&quot;: [],
  &quot;data&quot;: [],
  &quot;languages&quot;: [
    &quot;en-US&quot;
  ],
  &quot;version&quot;: &quot;0.0.0-dev&quot;,
  &quot;license&quot;: {
    &quot;name&quot;: &quot;MIT&quot;,
    &quot;description&quot;: &quot;MIT License&quot;,
    &quot;url&quot;: &quot;https://opensource.org/licenses/MIT&quot;
  },
  &quot;apis&quot;: [],
  &quot;links&quot;: [
    {
      &quot;type&quot;: &quot;application/json+yaml&quot;,
      &quot;rel&quot;: &quot;service-desc&quot;,
      &quot;href&quot;: &quot;https://demo.pygeoapi.io/master/openapi.yaml&quot;,
      &quot;hreflang&quot;: &quot;en-US&quot;,
      &quot;title&quot;: &quot;OpenAPI definition of the pygeoapi demo instance as yaml&quot;
    },
    {
      &quot;type&quot;: &quot;application/vnd.oai.openapi+json;version=3.0&quot;,
      &quot;rel&quot;: &quot;service-desc&quot;,
      &quot;href&quot;: &quot;https://demo.pygeoapi.io/master/openapi&quot;,
      &quot;hreflang&quot;: &quot;en-US&quot;,
      &quot;title&quot;: &quot;OpenAPI definition of the pygeoapi demo instance as json&quot;
    },
    {
      &quot;type&quot;: &quot;text/html&quot;,
      &quot;rel&quot;: &quot;service-doc&quot;,
      &quot;href&quot;: &quot;https://demo.pygeoapi.io/master/openapi&quot;,
      &quot;hreflang&quot;: &quot;en-US&quot;,
      &quot;title&quot;: &quot;OpenAPI definition of the pygeoapi demo instance as human readable document&quot;
    },
    {
      &quot;type&quot;: &quot;application/json&quot;,
      &quot;rel&quot;: &quot;conformance&quot;,
      &quot;href&quot;: &quot;https://demo.pygeoapi.io/master/conformance&quot;,
      &quot;hreflang&quot;: &quot;en-US&quot;,
      &quot;title&quot;: &quot;Conformance declaration HTML document&quot;
    },
    {
      &quot;type&quot;: &quot;application/json&quot;,
      &quot;rel&quot;: &quot;data&quot;,
      &quot;href&quot;: &quot;https://demo.pygeoapi.io/master/collections&quot;,
      &quot;hreflang&quot;: &quot;en-US&quot;,
      &quot;title&quot;: &quot;List of all collections available through the API&quot;,
      &quot;variables&quot;: []
    },
    {
      &quot;type&quot;: &quot;application/geo+json&quot;,
      &quot;rel&quot;: &quot;data&quot;,
      &quot;href&quot;: &quot;https://demo.pygeoapi.io/master/collections&quot;,
      &quot;hreflang&quot;: &quot;en-US&quot;,
      &quot;title&quot;: &quot;List of all collections available through the API&quot;,
      &quot;variables&quot;: []
    },
    {
      &quot;type&quot;: &quot;text/html&quot;,
      &quot;rel&quot;: &quot;data&quot;,
      &quot;href&quot;: &quot;https://demo.pygeoapi.io/master/collections?f=html&quot;,
      &quot;hreflang&quot;: &quot;en-US&quot;,
      &quot;title&quot;: &quot;List of all collections available through the API as an HTML document&quot;,
      &quot;variables&quot;: []
    },
    {
      &quot;type&quot;: &quot;application/json&quot;,
      &quot;rel&quot;: &quot;search&quot;,
      &quot;href&quot;: &quot;https://demo.pygeoapi.io/master/processjobs&quot;,
      &quot;hreflang&quot;: &quot;en-US&quot;,
      &quot;title&quot;: &quot;Search for available processes&quot;,
      &quot;variables&quot;: []
    },
    {
      &quot;type&quot;: &quot;application/json&quot;,
      &quot;rel&quot;: &quot;profile&quot;,
      &quot;href&quot;: &quot;https://demo.pygeoapi.io/master/oas&quot;,
      &quot;hreflang&quot;: &quot;en-US&quot;,
      &quot;title&quot;: &quot;OGC API landing page&quot;,
      &quot;variables&quot;: []
    }
  ],
  &quot;id&quot;: &quot;f6e6e87d-4e2f-4c7c-8c7f-7a7e7f7a7e7f&quot;,
  &quot;timeStamp&quot;: &quot;2023-01-01T00:00:00+00:00&quot;
}
```

### Declaração de conformidade[](#declaracao-de-conformidade)

Uma implementação de OGC API - Features descreve as capacidades que suporta declarando quais classes de conformidade implementa. A Declaração de Conformidade declara as classes de conformidade de padrões ou especificações comunitárias, identificadas por um URI, às quais a API está conforme. Os clientes podem depois usar esta informação, embora não sejam obrigados a fazê-lo. Acceder à Declaração de Conformidade usando HTTP GET retorna a lista de URIs de classes de conformidade implementadas pelo servidor. As classes de conformidade descrevem o comportamento que um servidor deve implementar a fim de cumprir um ou mais conjuntos de requisitos especificados num padrão.

Abaixo está um extrato da resposta ao pedido
[https://demo.pygeoapi.io/master/conformance](https://demo.pygeoapi.io/master/conformance)

```json
{
  &quot;conformsTo&quot;: [
    &quot;http://www.opengis.net/spec/ogcapi-features-1/1.0/conf/core&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-1/1.0/conf/geojson&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-1/1.0/conf/html&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-1/1.0/conf/odata&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-3/1.0/conf/geojson+jsonld&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-4/1.0/conf/create&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-5/1.0/conf/filter&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-5/1.0/conf/filter-basic-spatial-ops&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-5/1.0/conf/filter-crs&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-5/1.0/conf/filter-free-text&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-5/1.0/conf/filter-item-spatial-relations&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-5/1.0/conf/filter-spatial-ops&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-5/1.0/conf/filter-x-include&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-5/1.0/conf/filter-spatial-relations&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-5/1.0/conf/oas30&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-5/1.0/conf/filter-and-watch&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-5/1.0/conf/filter-watch&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-5/1.0/conf/transactions&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-5/1.0/conf/transactions-creation&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-5/1.0/conf/transactions-deletion&quot;,
    &quot;http://www.opengis.net/spec/ogcapi-features-5/1.0/conf/transactions-update&quot;
  ]
}
```

### Definição da API[](#definicao-da-api)

Dado que o OGC API - Features usa OGC API - Common como bloco de construção, consulte o aprofundamento [OGC API - Common](../common.pt/) para uma explicação detalhada de uma implementação de exemplo.

### Coleções de entidades[](#colecoes-de-entidades)

Os dados oferecidos através de uma implementação de OGC API - Features estão organizados numa ou mais coleções de entidades. O recurso Coleções fornece informação sobre e acesso à lista de coleções disponíveis.

Um exemplo de resposta para este pedido:

[https://demo.pygeoapi.io/master/collections](https://demo.pygeoapi.io/master/collections)

```json
{
  &quot;collections&quot;: [
    {
      &quot;id&quot;: &quot;ne_10m_urban_areas&quot;,
      &quot;type&quot;: &quot;collection&quot;,
      &quot;title&quot;: &quot;Natural Earth 1:10m Urban Areas&quot;,
      &quot;description&quot;: &quot;Natural Earth 1:10m Urban Areas&quot;,
      &quot;keywords&quot;: [
        &quot;ne&quot;,
        &quot;10m&quot;,
        &quot;urban&quot;,
        &quot;areas&quot;
      ],
      &quot;links&quot;: [
        {
          &quot;href&quot;: &quot;https://demo.pygeoapi.io/master/collections/ne_10m_urban_areas&quot;,
          &quot;rel&quot;: &quot;self&quot;,
          &quot;type&quot;: &quot;application/json&quot;,
          &quot;title&quot;: &quot;JSON representation of the collection&quot;
        },
        {
          &quot;href&quot;: &quot;https://demo.pygeoapi.io/master/collections/ne_10m_urban_areas/items&quot;,
          &quot;rel&quot;: &quot;item&quot;,
          &quot;type&quot;: &quot;application/geo+json&quot;,
          &quot;title&quot;: &quot;GeoJSON representation of the items in the collection&quot;
        }
      ]
    },
  ]
}
```

### Coleção de entidades[](#colecao-de-entidades)

Para obter uma descrição de uma coleção específica, utilize o endpoint /collections/{collectionId}.

Um exemplo de resposta para este pedido:

[https://demo.pygeoapi.io/master/collections/ne_10m_urban_areas](https://demo.pygeoapi.io/master/collections/ne_10m_urban_areas)

```json
{
  &quot;id&quot;: &quot;ne_10m_urban_areas&quot;,
  &quot;type&quot;: &quot;collection&quot;,
  &quot;title&quot;: &quot;Natural Earth 1:10m Urban Areas&quot;,
  &quot;description&quot;: &quot;Natural Earth 1:10m Urban Areas&quot;,
  &quot;keywords&quot;: [
    &quot;ne&quot;,
    &quot;10m&quot;,
    &quot;urban&quot;,
    &quot;areas&quot;
  ],
  &quot;links&quot;: [
    {
      &quot;href&quot;: &quot;https://demo.pygeoapi.io/master/collections/ne_10m_urban_areas&quot;,
      &quot;rel&quot;: &quot;self&quot;,
      &quot;type&quot;: &quot;application/json&quot;,
      &quot;title&quot;: &quot;JSON representation of the collection&quot;
    },
    {
      &quot;href&quot;: &quot;https://demo.pygeoapi.io/master/collections/ne_10m_urban_areas/items&quot;,
      &quot;rel&quot;: &quot;item&quot;,
      &quot;type&quot;: &quot;application/geo+json&quot;,
      &quot;title&quot;: &quot;GeoJSON representation of the items in the collection&quot;
    }
  ],
  &quot;properties&quot;: {},
  &quot;extent&quot;: {
    &quot;spatial&quot;: {
      &quot;bbox&quot;: [
        [
          -180,
          -90,
          180,
          90
        ]
      ]
    },
    &quot;temporal&quot;: {
      &quot;interval&quot;: [
        [
          null,
          null
        ]
      ],
      &quot;trsName&quot;: &quot;http://www.opengis.net/def/trsname&quot;
    }
  },
  &quot;itemType&quot;: &quot;http://www.opengis.net/def/ogcapi/ogcapi-features-1/feature&quot;
}
```

### Itens[](#itens)

Para listar os itens de uma coleção, utilize o endpoint /collections/{collectionId}/items.

Um exemplo de resposta para este pedido:

[https://demo.pygeoapi.io/master/collections/ne_10m_urban_areas/items?limit=1](https://demo.pygeoapi.io/master/collections/ne_10m_urban_areas/items?limit=1)

```json
{
  &quot;type&quot;: &quot;FeatureCollection&quot;,
  &quot;features&quot;: [
    {
      &quot;type&quot;: &quot;Feature&quot;,
      &quot;id&quot;: &quot;1&quot;,
      &quot;geometry&quot;: {
        &quot;type&quot;: &quot;Polygon&quot;,
        &quot;coordinates&quot;: [
          [
            [
              -73.999500,
              40.715700
            ],
            [
              -73.999500,
              40.715700
            ]
          ]
        ]
      },
      &quot;properties&quot;: {
        &quot;SCALERANK&quot;: 1,
        &quot;FEATURECl&quot;: &quot;Admin-2 capital&quot;,
        &quot;NAME&quot;: &quot;New York City&quot;,
        &quot;NAME_ASLI&quot;: &quot;New York City&quot;,
        &quot;ADMIN_CODE&quot;: &quot;US.NY&quot;,
        &quot;ADMIN_CODE_ASLI&quot;: &quot;US.NY&quot;,
        &quot;WRATU&quot;: 1,
        &quot;POCPREFIX&quot;: &quot;City of&quot;,
        &quot;POCPRE_ASLI&quot;: &quot;City of&quot;,
        &quot;GOLDEN1&quot;: &quot;New York&quot;,
        &quot;GOLDEN1_ASLI&quot;: &quot;New York&quot;,
        &quot;GOLDEN2&quot;: null,
        &quot;GOLDEN2_ASLI&quot;: null,
        &quot;GOLDEN3&quot;: null,
        &quot;GOLDEN3_ASLI&quot;: null,
        &quot;LABELRANK&quot;: 1,
        &quot;REMARK&quot;: &quot;City and Borough&quot;
      }
    }
  ],
  &quot;numberMatched&quot;: 1,
  &quot;numberReturned&quot;: 1,
  &quot;timeStamp&quot;: &quot;2023-01-01T00:00:00+00:00&quot;,
  &quot;link:&quot;: [
    {
      &quot;href&quot;: &quot;https://demo.pygeoapi.io/master/collections/ne_10m_urban_areas/items?limit=1&quot;,
      &quot;rel&quot;: &quot;self&quot;,
      &quot;type&quot;: &quot;application/geo+json&quot;,
      &quot;title&quot;: &quot;This request, as GeoJSON&quot;
    }
  ]
}
```

### Item único[](#item-unico)

Para obter um item único de uma coleção, utilize o endpoint /collections/{collectionId}/items/{itemId}.

Um exemplo de resposta para este pedido:

[https://demo.pygeoapi.io/master/collections/ne_10m_urban_areas/items/1](https://demo.pygeoapi.io/master/collections/ne_10m_urban_areas/items/1)

```json
{
  &quot;type&quot;: &quot;Feature&quot;,
  &quot;id&quot;: &quot;1&quot;,
  &quot;geometry&quot;: {
    &quot;type&quot;: &quot;Polygon&quot;,
    &quot;coordinates&quot;: [
      [
        [
          -73.999500,
          40.715700
        ],
        [
          -73.999500,
          40.715700
        ]
      ]
    ]
  },
  &quot;properties&quot;: {
    &quot;SCALERANK&quot;: 1,
    &quot;FEATURECl&quot;: &quot;Admin-2 capital&quot;,
    &quot;NAME&quot;: &quot;New York City&quot;,
    &quot;NAME_ASLI&quot;: &quot;New York City&quot;,
    &quot;ADMIN_CODE&quot;: &quot;US.NY&quot;,
    &quot;ADMIN_CODE_ASLI&quot;: &quot;US.NY&quot;,
    &quot;WRATU&quot;: 1,
    &quot;POCPREFIX&quot;: &quot;City of&quot;,
    &quot;POCPRE_ASLI&quot;: &quot;City of&quot;,
    &quot;GOLDEN1&quot;: &quot;New York&quot;,
    &quot;GOLDEN1_ASLI&quot;: &quot;New York&quot;,
    &quot;GOLDEN2&quot;: null,
    &quot;GOLDEN2_ASLI&quot;: null,
    &quot;GOLDEN3&quot;: null,
    &quot;GOLDEN3_ASLI&quot;: null,
    &quot;LABELRANK&quot;: 1,
    &quot;REMARK&quot;: &quot;City and Borough&quot;
  },
  &quot;link:&quot;: [
    {
      &quot;href&quot;: &quot;https://demo.pygeoapi.io/master/collections/ne_10m_urban_areas/items/1&quot;,
      &quot;rel&quot;: &quot;self&quot;,
      &quot;type&quot;: &quot;application/geo+json&quot;,
      &quot;title&quot;: &quot;This request, as GeoJSON&quot;
    }
  ]
}
```

## Resumo[](#resumo)

OGC API - Features especifica um padrão para Web APIs que fornecem acesso a dados geoespaciais vetoriais. Diferentes formas de dados geoespaciais são suportadas, como entidades vetoriais, atributos e relações. Este aprofundamento forneceu uma visão geral do padrão e os vários Recursos e endpoints que são suportados. Mostra também um exemplo de como aceder a um endpoint OGC API - Features, usando um cliente JavaScript.
