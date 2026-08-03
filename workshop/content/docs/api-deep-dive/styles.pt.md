---
title: Styles
---

[


    [


# OGC API - Styles[](#ogc-api-styles)

Público-alvo
Estudantes que estão familiarizados com serviços web e APIs, e querem ter
uma visão geral do padrão OGC API - Styles

Objetivos de Aprendizagem
No final do módulo os estudantes serão capazes de:

Explicar o que é o padrão OGC API - Styles
Descrever o que pode ser feito com implementações OGC API - Styles
Compreender os principais recursos ofereidos por implementações de OGC API - Styles

## Introdução[](#introducao)

[OGC API - Styles](https://ogcapi.ogc.org/styles) é um padrão que define uma API Web que permite servidores de mapas, clientes bem como editores de estilo visual, gerir e buscar estilos.

Note
Este módulo de tutorial não tem a intenção de ser uma substituição ao
OGC API - Styles padrão. O tutorial
foca intencionalmente num subconjunto de capacidades a fim de fazer com que o
estudante comece a usar o padrão.

### Visão geral de Recursos[](#visao-geral-de-recursos)

O OGC API - Styles define os recursos listados na tabela seguinte:

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

    Coleções de estilos
    GET
    /style-collections
    Lista de coleções de estilos

    Coleção de estilos
    GET
    /style-collections/{styleCollectionId}
    Detalhes de uma coleção de estilos

    Estilos
    GET
    /styles
    Lista de estilos disponíveis

    Estilo
    GET
    /styles/{styleId}
    Detalhes de um estilo específico

## Resumo[](#resumo)

OGC API - Styles especifica um padrão para Web APIs que fornecem gestão e acesso a estilos de mapas. Este aprofundamento forneceu uma visão geral do padrão e os vários Recursos e endpoints que são suportados.
