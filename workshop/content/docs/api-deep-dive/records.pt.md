---
title: Records
---

[


    [


# OGC API - Records[](#ogc-api-records)

Público-alvo
Estudantes que estão familiarizados com serviços web e APIs, e querem ter
uma visão geral do padrão OGC API - Records

Objetivos de Aprendizagem
No final do módulo os estudantes serão capazes de:

Explicar o que é o padrão OGC API - Records
Descrever o que pode ser feito com implementações OGC API - Records
Compreender os principais recursos ofereidos por implementações de OGC API - Records

## Introdução[](#introducao)

[OGC API - Records](https://ogcapi.ogc.org/records) é um padrão que fornece descoberta e acesso a metadados sobre recursos geoespaciais.

O OGC API - Records permite a descoberta de dados geoespaciais através de uma interface baseada em registos, suportando esquemas de metadados como ISO 19115 e Dublin Core.

Note
Este módulo de tutorial não tem a intenção de ser uma substituição ao
OGC API - Records padrão. O tutorial
foca intencionalmente num subconjunto de capacidades a fim de fazer com que o
estudante comece a usar o padrão.

### Visão geral de Recursos[](#visao-geral-de-recursos)

O OGC API - Records define os recursos listados na tabela seguinte:

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
    Lista de classes de conformidade

    Definição da API
    GET
    /api
    Definição OpenAPI da API

    Coleções
    GET
    /collections
    Lista de coleções de registos

    Coleção
    GET
    /collections/{collectionId}
    Detalhes de uma coleção específica

    Registos
    GET
    /collections/{collectionId}/items
    Lista de registos disponíveis

    Registo
    GET
    /collections/{collectionId}/items/{recordId}
    Detalhes de um registo específico

## Resumo[](#resumo)

OGC API - Records especifica um padrão para Web APIs que fornecem descoberta e acesso a metadados sobre recursos geoespaciais. Este aprofundamento forneceu uma visão geral do padrão e os vários Recursos e endpoints que são suportados.
