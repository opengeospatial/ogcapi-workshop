---
title: OGC API - Records
---

# OGC API - Records

!!! abstract "Público-alvo"
    Estudantes familiarizados com serviços web e APIs, que desejam ter
    uma visão geral do standard OGC API - Records

!!! abstract "Objetivos de Aprendizagem"
    Ao concluir o módulo, os estudantes serão capazes de:

    - Explicar o que é o standard OGC API - Records
    - Descrever o que pode ser feito com implementações do OGC API - Records
    - Compreender os principais recursos oferecidos por implementações do OGC API - Records
    - Compreender como obter uma descrição das capacidades de uma
      implementação do OGC API - Records
    - Compreender como fazer pedidos a uma implementação do OGC API - Records
    - Conseguir encontrar um endpoint do OGC API - Records e utilizá-lo através de um cliente

## Introdução

O [OGC API - Records](https://records.developer.ogc.org/) é uma especificação de rascunho multi-parte que oferece a capacidade de
criar, modificar e consultar metadados na Web. A especificação de rascunho permite a
descoberta de recursos geoespaciais ao padronizar a forma como as coleções de informação
descritiva sobre os recursos (metadados) são expostas. A especificação de rascunho também
permite a descoberta e partilha de recursos relacionados que possam ser referenciados a partir
de recursos geoespaciais ou dos respetivos metadados, padronizando a forma como todos os tipos de registos
são expostos e geridos. A Parte 1 cobre o acesso apenas-leitura a registos e capacidades
simples de consulta. Capacidades adicionais que abordam necessidades específicas serão especificadas
em partes adicionais. Capacidades para consultas mais ricas ou para criar, atualizar ou eliminar
registos serão especificadas em partes adicionais.

!!! note
    O OGC API - Records aproveita o [OGC API - Features](features.md#usage) como base, com
    endpoints de URL semelhantes e fluxo de trabalho de pedido/resposta, para o Catálogo Pesquisável e Local.

### Antecedentes

> Histórico

  O trabalho do standard OGC API - Records foi iniciado em 2018 e foi originalmente designado por
  **OGC CAT4.0**. Desde então, seguiu o desenvolvimento do OGC API - Features como base.

> Versões

  A **OGC API - Records - Parte 1: Core** foi submetida ao OGC Architecture Board (OAB)
  e completou a fase de revisão pública. Espera-se que seja finalizada no Q4 de 2024.

> Suite de testes

  Atualmente não existem suites de testes implementadas; estas serão disponibilizadas assim que
  a especificação for aprovada e uma suite de testes executável (ETS) estiver disponível
  conforme o OGC CITE.

> Implementações

  As implementações podem ser encontradas na [página de implementações](https://github.com/opengeospatial/ogcapi-records/blob/master/implementations.md).


#### Utilização

O OGC API - Records suporta 3 padrões principais de implementação:

- Catálogo navegável: navegação e consulta de um conjunto de registos de metadados através de ligações
- Catálogo pesquisável: capacidade da API para consultar e filtrar uma coleção de registos de metadados com base em critérios de pesquisa (bbox, datetime, q, etc.)
- Catálogo de recursos locais: funcionalidade de catálogo pesquisável aplicada ao nível da coleção de uma API

O OGC API - Records suporta também um modelo de consulta central. Ou seja, um conjunto de propriedades comuns de consulta que podem ser utilizadas contra qualquer
servidor OGC API - Records, independentemente do formato/standard de metadados e/ou do design do repositório de metadados subjacente.

!!! note
    Para fins deste aprofundamento, vamos focar-nos no padrão de implementação de catálogo pesquisável.

#### Relação com outros standards

OGC Catalogue Service for the Web (CSW): O standard CSW é mais apropriado quando se trabalha com aplicações cliente que suportam apenas serviços web clássicos da OGC. Note também que o CSW adota um modelo central de metadados baseado no Dublin Core por predefinição. Em contraste, o OGC API - Records inclui recomendações para suportar HTML e GeoJSON como codificações, quando aplicável. As implementações do OGC API - Records podem também opcionalmente suportar formatos de metadados XML, como ISO 19115/19139.


### Visão geral dos recursos

O **OGC API - Records - Parte 1: Core** define os recursos listados na
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
    <td>Coleções de registos</td>
    <td>GET</td>
    <td>/collections</td>
    <td>Este recurso lista as coleções de registos oferecidas através da API.</td>
  </tr>
  <tr>
    <td>Coleção de registos</td>
    <td>GET</td>
    <td>/collections/{collectionId}</td>
    <td>Este recurso descreve a coleção de registos identificada no caminho.</td>
  </tr>
  <tr>
    <td>Acesso a registos</td>
    <td>GET</td>
    <td>/collections/{collectionId}/items</td>
    <td>Este recurso apresenta os registos contidos na coleção.</td>
  </tr>
  <tr>
    <td>Recurso central do registo</td>
    <td>GET</td>
    <td>/collections/{collectionId}/items/{recordId}</td>
    <td>Este recurso apresenta o registo identificado no caminho.</td>
  </tr>
</table>

Como mencionado anteriormente, o OGC API - Records utiliza intensivamente o OGC API - Features como bloco de construção base. Embora o OGC API - Records
permita qualquer modelo de metadados, uma diferença e valor acrescentado chave é a capacidade de descrever um modelo central de registo e elementos consultáveis. Isto
permite interoperabilidade e integração entre catálogos para descrever recursos geoespaciais de forma consistente.

Por exemplo, um repositório de metadados pode ser modelado após o standard ISO 19115 e ser exposto através do OGC API - Records através de
«mapeamento» dos elementos ISO para o modelo central de registo e elementos consultáveis.

O registo central é a unidade atómica de informação num catálogo. Uma descrição completa das propriedades centrais de um registo pode
encontrar-se em <https://docs.ogc.org/DRAFTS/20-004.html#core-properties>. O registo central é uma representação compatível com GeoJSON
com elementos fixos no objeto/bloco `properties`.

### Exemplo

O [servidor de demonstração](https://demo.pygeoapi.io/master) publica metadados de dados geoespaciais através de uma interface que está em conformidade com o OGC API - Records.

Um exemplo de pedido que pode ser utilizado para recuperar dados da coleção de registos de metadados amostrais do Dutch Nationaal georegister é <https://demo.pygeoapi.io/master/collections/dutch-metadata?f=html>

Note que a resposta ao pedido é HTML neste caso.

Alternativamente, os mesmos dados podem ser recuperados no formato GeoJSON, através do pedido <https://demo.pygeoapi.io/master/collections/dutch-metadata?f=json>

Uma aplicação cliente pode, em seguida, recuperar o documento GeoJSON e exibi-lo ou processá-lo.

## Recursos

### Landing page

Dado que o OGC API - Records utiliza o OGC API - Common e o OGC API - Features como blocos de construção, consulte o [OGC API - Features](features.md#landing-page) para
uma explicação detalhada.

### Declarações de conformidade

Dado que o OGC API - Records utiliza o OGC API - Common e o OGC API - Features como blocos de construção, consulte o [OGC API - Features](features.md#conformance-declarations) para
uma explicação detalhada.

### Definição da API

Dado que o OGC API - Records utiliza o OGC API - Common como bloco de construção, consulte o [OGC API - Features](features.md#api-definition) para
uma explicação detalhada de uma implementação de exemplo.

### Coleções de registos

Dado que o OGC API - Records utiliza o OGC API - Common e o OGC API - Features como blocos de construção, consulte o [OGC API - Features](features.md#feature-collections) para
uma explicação inicial detalhada.

As descrições de coleções do OGC API - Records fornecem as seguintes propriedades adicionais:

- Um título obrigatório para a coleção
- Um tipo obrigatório para a coleção
- Um indicador obrigatório sobre o tipo dos itens na coleção (`record`)

Abaixo segue um excerto da resposta ao pedido <https://demo.pygeoapi.io/master/collections?f=json>,
ilustrando um registo de coleção:

```json
{
    "id": "dutch-metadata",
    "type": "Catalog",
    "itemType": "record",
    "title": "Sample metadata records from Dutch Nationaal georegister",
    "description": "Sample metadata records from Dutch Nationaal georegister",
    "keywords":[
        "netherlands",
        "open data",
        "georegister"
    ],
    "links":[
        {
            "type": "application/json",
            "rel": "self",
            "title": "This document as JSON",
            "href": "https://demo.pygeoapi.io/master/collections/dutch-metadata?f=json"
        },
        {
            "type": "application/geo+json",
            "rel": "items",
            "title": "items as GeoJSON",
            "href": "https://demo.pygeoapi.io/master/collections/dutch-metadata/items?f=json"
        }
    ]
}
```

### Coleção de registos

Dado que o OGC API - Records utiliza o OGC API - Common e o OGC API - Features como blocos de construção, consulte o [OGC API - Features](features.md#feature-collection) para
uma explicação inicial detalhada, bem como a descrição das [Coleções de registos](#coleccao-de-registos)..

### Acesso a registos

Dado que o OGC API - Records utiliza o OGC API - Common e o OGC API - Features como blocos de construção, consulte o [OGC API - Features](features.md#features) para
uma explicação detalhada.

Abaixo segue um excerto da resposta ao pedido <https://demo.pygeoapi.io/master/collections/dutch-metadata/items?f=json>

```json
{
  "type": "FeatureCollection",
  "numberMatched": 308,
  "numberReturned": 10,
  "features": [
    {
      "id": "35149dfb-31d3-431c-a8bc-12a4034dac48",
      "type": "Feature",
      "geometry": {
        "type": "Polygon",
        "coordinates": [
          [
            [
              4.690751953125,
              52.358740234375
            ],
            [
              4.690751953125,
              52.6333984375
            ],
            [
              5.020341796875,
              52.6333984375
            ],
            [
              5.020341796875,
              52.358740234375
            ],
            [
              4.690751953125,
              52.358740234375
            ]
          ]
        ]
      },
      "properties": {
        "created": "2021-12-08",
        "updated": "2022-06-10T01:27:47Z",
        "type": "dataset",
        "title": "Kaartboeck 1635",
        "description": "Data uit kaartboeken van de periode 1635 tot 1775. De kaartboeken werden door het waterschap gebruikt om er op toe te zien dat de eigenaren geen water in beslag namen door demping.\nDe percelen op de kaart zijn naar de huidige maatstaven vrij nauwkeurig gemeten en voorzien van een administratie met de eigenaren. bijzondere locaties van molens werven en beroepen worden in de boeken vermeld. Alle 97 kaarten aan een geven een zeer gedetailleerd beeld van de Voorzaan, Nieuwe Haven en de Achterzaan. De bladen Oost en West van de zaan zijn vrij nauwkeurig. De bladen aan de Voorzaan zijn een schetsmatige weergave van de situatie. De kaart van de Nieuwe Haven si weer nauwkeurig te noemen.",
        "providers": [
          "Team Geo, geo-informatie@zaanstad.nl, Gemeente Zaanstad"
        ],
        "externalIds": [
          {
            "scheme": "default",
            "value": "35149dfb-31d3-431c-a8bc-12a4034dac48"
          }
        ],
        "themes": [
          {
            "concepts": [
              "ARGEOLOGIE",
              "MONUMENTEN",
              "KADASTER",
              "KAARTBOEK",
              "KAARTBOECK",
              "HISTORIE"
            ]
          }
        ],
        "extent": {
          "spatial": {
            "bbox": [
              [
                4.690751953125,
                52.358740234375,
                5.020341796875,
                52.6333984375
              ]
            ],
            "crs": "http://www.opengis.net/def/crs/OGC/1.3/CRS84"
          },
          "temporal": {
            "interval": [
              null,
              null
            ],
            "trs": "http://www.opengis.net/def/uom/ISO-8601/0/Gregorian"
          }
        }
      },
      "links": [
        {
          "href": "https://maps-intern.zaanstad.gem.local/geoserver/wms?SERVICE=WMS",
          "rel": "item",
          "title": "geo:kaartboeck",
          "type": "OGC:WMS"
        },
        {
          "href": "https://maps-intern.zaanstad.gem.local/geoserver/wfs?SERVICE=WFS",
          "rel": "item",
          "title": "geo:kaartboeck",
          "type": "OGC:WFS"
        },
        {
          "href": "https://maps-intern.zaanstad.gem.local/geoserver/wfs?SERVICE=WFS&version=1.0.0&request=GetFeature&typeName=geo:kaartboeck&outputFormat=csv",
          "rel": "item",
          "type": "download"
        },
        {
          "href": "https://maps-intern.zaanstad.gem.local/geoserver/wfs?SERVICE=WFS&version=1.0.0&request=GetFeature&typeName=geo:kaartboeck&outputFormat=shape-zip",
          "rel": "item",
          "type": "download"
        }
      ]
    }
```

Note que este documento é um documento GeoJSON válido.

O OGC API - Records suporta os mesmos parâmetros de consulta especificados no OGC API - Features. Além disso, o OGC API - Records adiciona um conjunto central de
elementos consultáveis fixos. Um exemplo de consulta com base numa pesquisa estilo «motor de pesquisa» utilizando o parâmetro **q** é <https://demo.pygeoapi.io/master/collections/dutch-metadata/items?f=json&q=biomassa>

!!! note
    Consulte a especificação OGC API - Records - Parte 1: Core para mais informação sobre elementos consultáveis centrais.


### Recurso central do registo

Dado que o OGC API - Records utiliza o OGC API - Common e o OGC API - Features como blocos de construção, consulte o [OGC API - Features](features.md#feature) para
uma explicação detalhada.

### GeoJSON

A Classe de Requisitos GeoJSON do OGC API - Records especifica uma codificação baseada em GeoJSON para o registo central, com base na RFC7946. Dada a onipresença do GeoJSON, existem inúmeras ferramentas para validar, processar e decodificar/codificar GeoJSON, tornando o GeoJSON do OGC API - Records fácil de incluir em pipelines de processamento de metadados. O OGC API - Records inclui o [JSON Schema](https://github.com/opengeospatial/ogcapi-records/blob/master/core/openapi/schemas/recordGeoJSON.yaml) para a representação GeoJSON e, por conseguinte, pode ser utilizado para validação em tempo de execução ou offline de payloads de metadados. Aplicações baseadas no GeoJSON do OGC API - Records podem estender e restringir o esquema de acordo para fluxos de trabalho específicos do domínio.

## Resumo

O OGC API - Records fornece funcionalidade para trabalhar com dados de metadados na Web. Este aprofundamento proporcionou uma visão geral do standard e dos vários recursos e endpoints suportados.
