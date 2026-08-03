---
title: Environmental-Data-Retrieval
---

[


    [


# OGC API - Recuperação de Dados Ambientais[](#ogc-api-recuperacao-de-dados-ambientais)

Público-alvo
Estudantes que estão familiarizados com serviços web e APIs, e querem ter
uma visão geral do padrão OGC API - Recuperação de Dados Ambientais

Objetivos de Aprendizagem
No final do módulo os estudantes serão capazes de:

Explicar o que é o padrão OGC API - Recuperação de Dados Ambientais
Descrever o que pode ser feito com implementações OGC API - Recuperação de Dados Ambientais
Compreender os principais recursos ofereidos por implementações de OGC API - Recuperação de Dados Ambientais
Compreender como obter uma descrição das capacidades de uma implementação
Compreender como emitir pedidos a uma implementação de OGC API - Recuperação de Dados Ambientais
Ser capaz de encontrar um endpoint e usá-lo através de um cliente

## Introdução[](#introducao)

[OGC API - Environmental Data Retrieval](https://ogcapi.ogc.org/edr) é um padrão que fornece uma família de interfaces leves para acesso a recursos de Dados Ambientais.

O padrão, que também é chamado de API EDR, aborda duas operações fundamentais; descoberta e consulta. As operações de descoberta permitem que a API seja interrogada para determinar as suas capacidades e recuperar informação (metadados) sobre esta distribuição de um recurso. As operações de consulta permitem que os recursos de Dados Ambientais sejam recuperados da base de dados subjacente com base em critérios de seleção simples.

Note
Este módulo de tutorial não tem a intenção de ser uma substituição ao
OGC API - Environmental Data Retrieval padrão. O tutorial
foca intencionalmente num subconjunto de capacidades a fim de fazer com que o
estudante comece a usar o padrão. Por favor consulte o [OGC API -
Environmental Data Retrieval padrão](https://docs.ogc.org/is/19-086r6/19-086r6.html) para mais detalhes.

### Antecedentes[](#antecedentes)

História

A versão 1.1.0 foi publicada em 2023-07-27.

Versões

A versão 1.1.0 do OGC API - Environmental Data Retrieval é a versão mais recente atual

#### Utilização[](#utilizacao)
OGC API - Environmental Data Retrieval fornece uma família de interfaces de consulta leves para aceder a recursos de dados espácio-temporais requisitando dados numa posição, dentro de uma área, ao longo de uma trajetória ou através de um corredor.

### Visão geral de Recursos[](#visao-geral-de-recursos)

O Padrão OGC API - Environmental Data Retrieval define os recursos listados na tabela seguinte.

Visão geral dos recursos OGC API - EDR

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
    Este recurso fornece metadados sobre a API em si.

    Metadados de coleções
    GET
    /collections
    Metadados descrevendo as coleções de dados disponíveis desta API.

    Metadados de Coleção Única
    GET
    /collections/{collectionId}
    Metadados descrevendo a coleção de dados com o identificador único {collectionId}.

    Itens
    GET
    /collections/{collectionId}/items
    Recupera metadados sobre itens disponíveis.

    Consultar dados
    GET
    /collections/{collectionId}/{queryType}
    Recupera dados de acordo com o padrão de consulta

### Exemplo[](#exemplo)

Este [servidor de demonstração](http://labs.metoffice.gov.uk/edr) publica dados ambientais através de uma interface que é conforme com o padrão OGC API - Environmental Data Retrieval.

Os padrões de consulta suportados incluem:

posição: recuperar dados numa única posição

área: recuperar dados dentro de uma área

cubo: recuperar dados dentro de um cubo 3D

trajetória: recuperar dados ao longo de uma trajetória

corredor: recuperar dados ao longo de um corredor

raio: recuperar dados dentro de um raio

## Resumo[](#resumo)

OGC API - Environmental Data Retrieval especifica um padrão para Web APIs que fornecem acesso a dados ambientais espácio-temporais. Este aprofundamento forneceu uma visão geral do padrão e os vários Recursos e endpoints que são suportados.
