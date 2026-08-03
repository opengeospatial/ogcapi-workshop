---
title: Visão geral e conceitos principais
---

# Visão geral e conceitos principais

O núcleo das APIs Web pode ser resumido como:

- interfaces: a forma como as "conversas" acontecem entre APIs e os seus clientes
- codificações: os "formatos" dos conteúdos fornecidos por uma API

## Cliente / servidor

Num ambiente típico cliente/servidor, um cliente pede a um servidor para executar uma ação (por
exemplo, requisitar dados), com a capacidade de adicionar instruções adicionais como consulta, filtragem
e qual formato a API deve fornecer como parte da resposta.

A imagem abaixo, retirada de [Introduction to GIS](https://volaya.github.io/gis-book/en/) ilustra
o conceito do ciclo de vida de pedido/resposta entre um cliente e um servidor.

![Client-Server](assets/images/How_internet_works.png){width="80.0%"}

## Arquitetura Web

### REST

REpresentational State Transfer (REST) é um estilo arquitetural para a Web. Os conceitos centrais do REST são:

- verbos HTTP (GET/PUT/POST/DELETE)
- códigos HTTP (200, 201, 404, etc.)
- URIs para identificar recursos
- Negociação de conteúdo (tipos de conteúdo)
- Stateless (sem estado)

Implementar REST resulta numa arquitetura mais simples e com baixa barreira que é baseada em primitivas web. Isto permite que sistemas
e aplicações se foquem mais em requisitos de domínio/negócios.

!!! note "Conheça o seu HTTP!"
    - verbos: <https://http.dev/methods>
    - códigos de estado: <https://http.dev/status>

### JSON

JSON (JavaScript Object Notation) é uma codificação compacta e muito fácil de compreender, que é muito popular entre
desenvolvedores web. O JSON é a codificação primária utilizada em serviços web RESTful e APIs, e é por natureza extensível.

Vamos comparar JSON e XML num exemplo simples:

Um exemplo de documento XML (75 bytes):

```xml
<order>
    <orderID>123</orderId>
    <status>completed</status>
</order>
```

O mesmo documento em JSON (46 bytes):

```json
{
  "orderID": 123,
  "status": "completed"
}
```

Aqui, vemos uma representação mais compacta usando JSON. Além disso, é mais fácil determinar os literais de tipo de dados
subjacentes (inteiros, strings, etc.) através da análise do próprio documento.

!!! note JSON Schema
    O [JSON Schema](https://json-schema.org) é o equivalente em JSON ao W3C XML Schema, fornecendo uma linguagem para definir o modelo de conteúdo de
    um documento JSON. Um documento JSON pode escolher implementar um JSON Schema, ou não, dependendo dos requisitos de uma aplicação dada
    para validação e integridade de dados

## OGC APIs

Esta secção fornece uma visão geral de alto nível do suporte aos padrões OGC API.

!!! cite

    A família de padrões OGC API está a ser desenvolvida para facilitar a qualquer pessoa a disponibilização de dados geoespaciais na web. Estes padrões constroem sobre a herança dos padrões de Serviços Web do OGC (WMS, WFS, WCS, WPS, etc.), mas definem APIs centradas em recursos que aproveitam as práticas modernas de desenvolvimento web. Esta página web fornece informação sobre estes padrões num local consolidado.

    Estes padrões estão a ser construídos como "blocos de construção" que podem ser usados para montar APIs inovadoras para acesso web a conteúdo geoespacial. Os blocos de construção são definidos não apenas pelos requisitos dos padrões específicos, mas também através de prototipagem e testes de interoperabilidade no Programa de Inovação do OGC.

### OGC API - Common

O [OGC API - Common](https://ogcapi.ogc.org/common) é um quadro comum usado em todas as OGC APIs.
OGC API - Common fornece a seguinte funcionalidade:

- baseado em [OpenAPI 3.0](https://spec.openapis.org/oas/latest.html)
- HTML e JSON como codificações dominantes, outras codificações alternativas são possíveis
- endpoints comuns e partilhados como:
    - `/` (página inicial)
    - `/conformance`
    - `/openapi`
    - `/collections`
    - `/collections/foo`
- aspetos comuns como paginação, ligações entre recursos, filtragem básica, parâmetros de consulta (`bbox`, `datetime`, etc.)

OGC API - Common permite que os desenvolvedores de especificações se foquem na funcionalidade chave de uma dada API (i.e. acesso a dados, etc.)
enquanto usam construções comuns. Isto harmoniza os padrões OGC API e permite integração mais profunda com menos código. Isto também
permite que o software cliente de OGC API seja mais streamlined.

Para mais detalhes sobre este padrão, por favor consulte a [secção OGC API - Common](https://ogcapi-workshop.ogc.org/api-deep-dive/common/).

### Padrões Aprovados

Os seguintes padrões OGC API foram aprovados e estão disponíveis para uso. Note que estes padrões têm 1 ou mais "Partes" ou extensões que permitem funcionalidades específicas. A "Parte 1" de um dado padrão representa as capacidades mais básicas. Partes adicionais também podem ser implementadas como [blocos de construção](#blocos-de-construcao-ogc-api).

- [OGC API - Features](https://ogcapi.ogc.org/features) oferece a capacidade de criar, modificar e consultar dados espaciais na Web e especifica requisitos e recomendações para APIs que querem seguir uma forma padrão de partilhar dados de entidades
- [OGC API - Environmental Data Retrieval](https://ogcapi.ogc.org/edr) fornece uma família de interfaces leves para aceder a recursos de dados ambientais. Cada recurso endereçado por uma API EDR mapeia para um padrão de consulta definido
- [OGC API - Maps](https://ogcapi.ogc.org/maps) oferece uma abordagem moderna ao padrão OGC Web Map Service (WMS) para disponibilizar conteúdo de mapas e raster
- [OGC API - Processes](https://ogcapi.ogc.org/processes) permite que ferramentas de processamento sejam chamadas e combinadas a partir de muitas fontes e aplicadas a dados noutros recursos OGC API através de uma API simples
- [OGC API - Tiles](https://ogcapi.ogc.org/tiles) fornece funcionalidade estendida a outros Padrões OGC API para entregar tiles vetoriais, tiles de mapas e outros dados em tiles
- [OGC API - Moving Features](https://ogcapi.ogc.org/movingfeatures) define uma API que proporciona acesso a dados que representam entidades que se movem como corpos rígidos
- [OGC API - Records](https://ogcapi.ogc.org/records) fornece descoberta e acesso a metadados sobre recursos geoespaciais
- [OGC API - Discrete Global Grid Systems](https://ogcapi.ogc.org/dggs) permite que aplicações organizem e acedam a dados organizados de acordo com um Sistema de Grelha Global Discreto (DGGS)
- [OGC API - Connected Systems](https://ogcapi.ogc.org/connectedsystems/) tem como objetivo actuar como uma ponte entre dados estáticos (entidades geográficas e de outro domínio) e dados dinâmicos (observações destas propriedades das entidades, e comandos/actuações que mudam estas propriedades das entidades)

### Blocos de construção OGC API

A abordagem OGC API permite modularidade e "perfilamento" de APIs dependendo dos seus requisitos. Isto significa que pode
misturar e combinar OGC APIs entre si.

![Blocos de construção OGC API](assets/images/ogc-api-building-blocks.png)

Pode ler mais sobre este tópico no [site de blocos de construção](https://opengeospatial.github.io/bblocks/).

### Em desenvolvimento

O esforço OGC API está em rápida evolução. Numerosos padrões OGC API estão em desenvolvimento:

- [Routes](https://ogcapi.ogc.org/routes) fornece acesso a dados de rotas
- [Styles](https://ogcapi.ogc.org/styles) define uma API Web que permite servidores de mapas, clientes bem como editores de estilo visual, gerir e buscar estilos
- [3D GeoVolumes](https://ogcapi.ogc.org/geovolumes) facilita a descoberta eficiente de e acesso a conteúdo 3D em múltiplos formatos baseado numa perspetiva centrada no espaço
- [Joins](https://ogcapi.ogc.org/joins) suporta a junção de dados, a partir de múltiplas fontes, com coleções de entidades ou diretamente com outros ficheiros de entrada

![Padrões OGC API aprovados e candidatos](assets/images/ogcapis-overview.png)

### OpenAPI

Central ao OGC API - Common está a [iniciativa OpenAPI](https://www.openapis.org/about) para ajudar
a descrever e documentar uma API. O OpenAPI define a sua estrutura num documento OpenAPI.
OGC API - Common sugere que este documento esteja localizado em `/openapi`. Por exemplo, com [pygeoapi](https://pygeoapi.io) num navegador
[esta URL](https://demo.pygeoapi.io/master/openapi) abre uma página HTML interativa que facilita
uma consulta à API. Acrescente `?f=json` para ver o documento em JSON. O documento OpenAPI indica quais
os endpoints disponíveis no serviço, quais parâmetros aceita e
que tipos de respostas podem ser esperados. O documento OpenAPI é um conceito semelhante ao Capabilities
XML como parte dos primeiros padrões de Serviços Web do OGC.

!!! question "Análise de Especificação OpenAPI num navegador"

    Uma abordagem comum para interagir com APIs Open usando json é usar um programa como
    [Postman](https://www.postman.com/). Também existem plugins de navegador que permitem definir pedidos de api
    de forma interativa num navegador. Para firefox descarregue o plugin
    [poster](https://pluginsaddonsextensions.com/mozilla-firefox/poster-mozilla-addon). Para Chrome
    e Edge use [Boomerang](https://microsoftedge.microsoft.com/addons/detail/boomerang-soap-rest-c/bhmdjpobkcdcompmlhiigoidknlgghfo?hl=en-US).
    No Boomerang pode criar pedidos web individuais, mas também carregar o documento de especificação open api
    e interagir com qualquer um dos endpoints anunciados.

A comunidade OpenAPI fornece várias ferramentas, como um validador para documentos OAS ou
[gerar código](https://swagger.io/tools/swagger-codegen/) como ponto de partida para desenvolvimento de cliente.

## Padrões de conteúdo e formato

As OGC APIs são tipicamente agnósticas ao formato de dados. Isto significa que uma OGC API pode fornecer qualquer formato de dados
ou metadados (JSON, YAML, XML, HTML, etc.).

JSON é um formato principal que é legível por máquina e fácil de analisar e tratar
por software cliente e ferramentas. JSON é facilmente decodificado/codificado em objetos nativos em numerosas
linguagens de programação (dicionários Python, objetos JavaScript, etc.). O OGC API - Common fornece
formatos JSON uniformes para os vários endpoints que suporta.

Certos padrões OGC API podem especificar formatos específicos de domínio (por exemplo,
GeoJSON para OGC API - Features, GeoTIFF para OGC API - Coverages, ISO 19115/19139 para OGC API - Records, etc.),
dependendo do tipo de dados ou metadados.

## Resumo

As OGC APIs aproveitam os princípios centrais da arquitetura Web, fornecendo suporte para descoberta, acesso, visualização, processamento
de dados geoespaciais, em alinhamento com padrões da indústria para máxima interoperabilidade na Web.
