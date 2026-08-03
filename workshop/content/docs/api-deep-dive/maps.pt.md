---
title: Maps
---

[


    [


# OGC API - Maps[](#ogc-api-maps)

Público-alvo
Estudantes que estão familiarizados com serviços web e APIs, e querem ter
uma visão geral do padrão OGC API - Maps

Objetivos de Aprendizagem
No final do módulo os estudantes serão capazes de:

Explicar o que é o padrão OGC API - Maps
Descrever o que pode ser feito com implementações OGC API - Maps
Compreender os principais recursos ofereidos por implementações de OGC API - Maps

## Introdução[](#introducao)

[OGC API - Maps](https://ogcapi.ogc.org/maps) é um padrão que fornece
uma família de interfaces leves para acesso a mapas.
O padrão aborda dois conceitos fundamentais: mapas e estilos.
Um mapa é uma representação visual de dados geoespaciais.
Um estilo define a aparência visual de entidades geoespaciais num mapa.

Note
Este módulo de tutorial não tem a intenção de ser uma substituição ao
OGC API - Maps padrão. O tutorial
foca intencionalmente num subconjunto de capacidades a fim de fazer com que o
estudante comece a usar o padrão. Por favor consulte o [OGC API -
Maps padrão](https://docs.ogc.org/is/20-035/20-035.html) para mais detalhes.

### Antecedentes[](#antecedentes)

História

A versão 1.0.0 foi publicada em 2023-05-25.

Versões

A versão 1.0.0 do OGC API - Maps - Parte 1: Núcleo é a versão mais recente atual

Suite de testes

Uma suite de testes está disponível para:

[OGC API - Maps - Parte 1](https://github.com/opengeospatial/ets-ogcapi-maps10)

#### Utilização[](#utilizacao)
O OGC API - Maps permite que aplicações cliente descubram e acedam a mapas através de uma API REST. Os mapas são descritos usando metadados que incluem informação sobre o tipo de mapa, projeção, extents, e formatos de saída suportados.

### Visão geral de Recursos[](#visao-geral-de-recursos)

O OGC API - Maps - Parte 1: Núcleo define os recursos listados na tabela seguinte:

    Recurso
    Método
    Caminho
    Propósito

    Página inicial
    GET
    /
    Ponto de entrada da API

    Declaração de conformidade
    GET
    /conformance
    Lista de classes de conformidade implementadas

    Definição da API
    GET
    /api
    Definição OpenAPI da API

    Coleções
    GET
    /collections
    Lista de coleções disponíveis

    Coleção
    GET
    /collections/{collectionId}
    Detalhes de uma coleção específica

    Map tilesets
    GET
    /collections/{collectionId}/map/tiles
    Lista de tilesets de mapas para uma coleção

    Map tileset
    GET
    /collections/{collectionId}/map/tiles/{tileMatrixSetId}
    Metadados de um tileset de mapas específico

    Map tile
    GET
    /collections/{collectionId}/map/tiles/{tileMatrixSetId}/{tileMatrix}/{tileRow}/{tileCol}
    Um tile de mapa específico

## Resumo[](#resumo)

OGC API - Maps especifica um padrão para Web APIs que fornecem acesso a mapas e imagens geoespaciais. Este aprofundamento forneceu uma visão geral do padrão e os vários Recursos e endpoints que são suportados.
