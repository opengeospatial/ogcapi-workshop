---
title: Tiles
---

```json
[


    [


# OGC API - Tiles[](#ogc-api-tiles)

Público-alvo
Estudantes que estão familiarizados com serviços web e APIs, e querem ter
uma visão geral do padrão OGC API - Tiles

Objetivos de Aprendizagem
No final do módulo os estudantes serão capazes de:

Explicar o que é o padrão OGC API - Tiles
Descrever o que pode ser feito com implementações OGC API - Tiles
Compreender os principais recursos ofereidos por implementações de OGC API - Tiles

## Introdução[](#introducao)

[OGC API - Tiles](https://ogcapi.ogc.org/tiles) é um padrão que fornece
uma família de interfaces leves para acesso a dados em tiles.
O padrão aborda dois conceitos fundamentais: tile matrix sets e tile sets.
Um tile matrix set define um sistema de coordenadas, uma escala e uma grade de tiles para um conjunto de dados.
Um tile set é um conjunto de tiles resultantes da aplicação de um tile matrix set a um conjunto de dados.

Note
Este módulo de tutorial não tem a intenção de ser uma substituição ao
OGC API - Tiles padrão. O tutorial
foca intencionalmente num subconjunto de capacidades a fim de fazer com que o
estudante comece a usar o padrão. Por favor consulte o [OGC API -
Tiles padrão](https://docs.ogc.org/is/20-035/20-035.html) para mais detalhes.

### Antecedentes[](#antecedentes)

História

A versão 1.0.0 foi publicada em 2021-01-15.

Versões

A versão 1.0.0 do OGC API - Tiles - Parte 1: Núcleo é a versão mais recente atual

#### Utilização[](#utilizacao)
O OGC API - Tiles define os seguintes conceitos fundamentais:

Tile: uma porção de dados geoespaciais num formato específico (por exemplo, PNG, JPEG, MVT) numa posição e escala específicas.

Tile Matrix: uma grade de tiles num sistema de coordenadas 2D dado, associada a uma escala específica e partição de espaço (e.g.: esquema de tiling).

Tile Matrix Set: esquema de tiling consistindo num conjunto de tile matrices definidos em diferentes escalas cobrindo aproximadamente a mesma área e tendo um sistema de coordenadas comum. Um Tile Matrix tem um identificador alfanumérico único no Tile Matrix Set. Algumas implementações baseadas em tiles preferem usar o número do nível de zoom. 

Tile Set: conjunto de tiles resultante da aplicação de tiling a dados de acordo com um determinado esquema de tiling.

Note

Um tile matrix pode ser implementado como um conjunto de ficheiros de imagem (e.g., PNG ou JPEG) numa pasta, cada ficheiro representando um único tile.
Em alguns padrões o conceito de Tile Matrix Set é chamado de imagem piramidal.

### Antecedentes[](#antecedentes_1)

História

O padrão OGC API - Tiles é um sucessor do padrão OGC Web Map
  Tile Service (WMTS), focando em blocos de construção REST reutilizáveis simples que podem ser descritos usando a especificação OpenAPI. Enquanto o WMTS se focava em tiles de mapas, o padrão OGC API -
  Tiles foi desenhado para suportar qualquer forma de dados em tiles.

Versões

A versão 1.0.0 do OGC API - Tiles - Parte 1: Núcleo é a versão mais recente atual

Suite de testes

Uma suite de testes está disponível para:

[OGC API - Tiles - Parte 1](https://github.com/opengeospatial/ets-ogcapi-tiles10)

Implementações

Implementações podem ser encontradas na [página de implementações](https://github.com/opengeospatial/ogcapi-tiles/blob/master/implementations.adoc).

#### Utilização[](#utilizacao_1)
Existem pelo menos duas formas de abordar uma implementação do Padrão OGC API - Tiles.

Ler a página inicial, procurar ligações, segui-las e descobrir novas ligações até encontrar o recurso desejado
Ler um documento de definição de API Web que especifica uma lista de caminhos e modelos de caminho para recursos.

Uma vez que descobriu os recursos relevantes, depois recupere a lista de esquemas de tiling disponíveis do recurso
/tileMatrixSets para identificar o esquema de tiling de interesse. Recupere os detalhes do esquema de tiling específico com /tileMatrixSets/{tileMatrixSetId}.

Uma vez que identificou um esquema de tiling de interesse, pode recuperar metadados de tile set para esse esquema de tiling através de
/tiles/{tileMatrixSetId} e também recuperar tiles individuais com
/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}

#### Relação com outros padrões OGC[](#relacao-com-outros-padroes-ogc)
Embora o Padrão OGC API - Tiles seja desenhado como um bloco de construção que pode ser aproveitado por (ou com) outros Padrões OGC API adicionando precisões sobre tipos específicos de dados disponíveis como tiles (e.g., padrão OGC API - Features, e padrões candidatos OGC API - Maps e OGC API - Coverages), as classes de conformidade definidas neste Padrão são ainda concretas o suficiente para tornar possível suportar distribuição e requisição de vários tipos de dados em tiles, incluindo coberturas, entidades vetoriais e mapas, confiando estritamente no conteúdo aqui e no padrão OGC Two Dimensional Tile Matrix Set and Tile Set Metadata 2.0.

### Visão geral de Recursos[](#visao-geral-de-recursos)

O OGC API - Tiles - Parte 1: Núcleo define os recursos listados na tabela seguinte.

    Recurso
    Método
    Caminho

    Página inicial
    GET
    /

    Declaração de conformidade
    GET
    /conformance

    Definição da API
    GET
    /api

    Tile matrix sets
    GET
    /tileMatrixSets

    Tile matrix set
    GET
    /tileMatrixSets/{tileMatrixSetId}

    Tileset do conjunto de dados
    GET
    /tiles

    Metadados do tileset do conjunto de dados
    GET
    /tiles/{tileMatrixSetId}

    Tile de entidade do conjunto de dados
    GET
    /tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}

### Exemplo[](#exemplo)

Este [servidor de demonstração](https://demo.ldproxy.net/zoomstack/)
publica dados em tiles de entidades através de uma interface que é conforme com OGC API - Tiles.

Um exemplo de pedido que pode ser usado para recuperar dados, referenciados ao WebMercatorQuad, da coleção OS Zoomstack é
[https://demo.ldproxy.net/zoomstack/tiles/WebMercatorQuad/0/0/0?f=mvt](https://demo.ldproxy.net/zoomstack/tiles/WebMercatorQuad/0/0/0?f=mvt)

Neste caso os dados são codificados no formato Mapbox Vector Tiles (MVT).

Uma vez descarregados, uma aplicação cliente pode depois exibir ou processar os dados.

## Recursos[](#recursos)

### Página inicial[](#pagina-inicial)

Dado que o OGC API - Tiles usa OGC API - Common como bloco de construção, consulte o aprofundamento [OGC API - Features](../features.pt/#pagina-inicial) para uma explicação detalhada de uma implementação de exemplo.

### Declarações de conformidade[](#declaracoes-de-conformidade)

Dado que o OGC API - Tiles usa OGC API - Common como bloco de construção, consulte o aprofundamento [OGC API - Features](../features.pt/#declaracao-de-conformidade) para uma explicação detalhada de uma implementação de exemplo.

### Definição da API[](#definicao-da-api)

Dado que o OGC API - Tiles usa OGC API - Common como bloco de construção, consulte o aprofundamento [OGC API - Features](../features.pt/#definicao-da-api) para uma explicação detalhada de uma implementação de exemplo.

### Coleções[](#colecoes)

Dado que o OGC API - Tiles usa OGC API - Common como bloco de construção, consulte o aprofundamento [OGC API - Features](../features.pt/#colecoes-de-entidades) para uma explicação detalhada de uma implementação de exemplo.

### Coleção[](#colecao)

Dado que o OGC API - Tiles usa OGC API - Common como bloco de construção, consulte o aprofundamento [OGC API - Features](../features.pt/#colecao-de-entidades) para uma explicação detalhada de uma implementação de exemplo.

### Esquemas de Tiling[](#esquemas-de-tiling)

Este endpoint recupera uma lista de ligações para as descrições dos tile matrix sets suportados pela OGC Web API. Estes podem ser um ou muitos dos tile matrix sets bem conhecidos listados no Apêndice D de [OGC Two Dimensional Tile Matrix Set and Tile Set Metadata](https://docs.ogc.org/is/17-083r4/17-083r4.html#toc48), ou personalizados.

Como exemplo, podemos ver um extrato da resposta a este pedido:
[https://demo.ldproxy.net/daraa/tileMatrixSets?f=json](https://demo.ldproxy.net/daraa/tileMatrixSets?f=json)

  &quot;tileMatrixSets&quot;: [
    {
      &quot;title&quot;: &quot;Google Maps Compatible for the World&quot;,
      &quot;id&quot;: &quot;WebMercatorQuad&quot;,
      &quot;uri&quot;: &quot;http://www.opengis.net/def/tilematrixset/OGC/1.0/WebMercatorQuad&quot;,
      &quot;links&quot;: [
        {
          &quot;rel&quot;: &quot;self&quot;,
          &quot;title&quot;: &quot;Tile matrix set &#39;WebMercatorQuad&#39;&quot;,
          &quot;href&quot;: &quot;https://demo.ldproxy.net/daraa/tileMatrixSets/WebMercatorQuad&quot;
        }
      ]
    },
    {
      &quot;title&quot;: &quot;CRS84 for the World&quot;,
      &quot;id&quot;: &quot;WorldCRS84Quad&quot;,
      &quot;uri&quot;: &quot;http://www.opengis.net/def/tilematrixset/OGC/1.0/WorldCRS84Quad&quot;,
      &quot;links&quot;: [
        {
          &quot;rel&quot;: &quot;self&quot;,
          &quot;title&quot;: &quot;Tile matrix set &#39;WorldCRS84Quad&#39;&quot;,
          &quot;href&quot;: &quot;https://demo.ldproxy.net/daraa/tileMatrixSets/WorldCRS84Quad&quot;
        }
      ]
    }
  ]

Se acrescentarmos o id do tile matrix set a esta url, obteremos a descrição de um tile matrix set específico, como podemos ver no exemplo abaixo, gerado com este pedido:

[https://demo.ldproxy.net/daraa/tileMatrixSets/WebMercatorQuad?f=json](https://demo.ldproxy.net/daraa/tileMatrixSets/WebMercatorQuad?f=json)

{
  &quot;title&quot;: &quot;Google Maps Compatible for the World&quot;,
  &quot;id&quot;: &quot;WebMercatorQuad&quot;,
  &quot;crs&quot;: &quot;http://www.opengis.net/def/crs/EPSG/0/3857&quot;,
  &quot;wellKnownScaleSet&quot;: &quot;http://www.opengis.net/def/wkss/OGC/1.0/GoogleMapsCompatible&quot;,
  &quot;uri&quot;: &quot;http://www.opengis.net/def/tilematrixset/OGC/1.0/WebMercatorQuad&quot;,
  &quot;tileMatrices&quot;: [
    {
      &quot;id&quot;: &quot;0&quot;,
      &quot;tileWidth&quot;: 256,
      &quot;tileHeight&quot;: 256,
      &quot;matrixWidth&quot;: 1,
      &quot;matrixHeight&quot;: 1,
      &quot;scaleDenominator&quot;: 559082264.028717,
      &quot;cellSize&quot;: 156543.033928041,
      &quot;pointOfOrigin&quot;: [
        -20037508.3427892,
        20037508.3427892
      ],
      &quot;cornerOfOrigin&quot;: &quot;topLeft&quot;
    }
  ]
}
```

Note que para além dos metadados descritivos, a resposta também contém uma lista detalhada de tile matrices disponíveis.

## Resumo[](#resumo)

OGC API - Tiles especifica um padrão para Web APIs que fornecem tiles de informação geoespacial. Diferentes formas de informação geoespacial são suportadas, como tiles de entidades vetoriais ("vector tiles"), coberturas, mapas (ou imagens) e potencialmente eventualmente tipos adicionais de tiles de informação geoespacial. Este aprofundamento forneceu uma visão geral do padrão e os vários Recursos e endpoints que são suportados. Mostra também um exemplo de como aceder a um endpoint OGC API - Tiles, usando um cliente JavaScript.
