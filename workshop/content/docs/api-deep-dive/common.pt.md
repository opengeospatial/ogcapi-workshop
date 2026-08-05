---
title: OGC API - Common
---

# OGC API - Common

!!! abstract "Público-alvo"
    Estudantes que estejam familiarizados com serviços web e APIs, e queiram ter
    uma visão geral da norma OGC API - Common

!!! abstract "Objetivos de Aprendizagem"
    Após a conclusão do módulo, os estudantes serão capazes de:

    - Explicar o que é a norma OGC API - Common
    - Descrever o que pode ser feito com a OGC API - Common como bloco de construção

## Introdução

A [OGC API - Common](https://ogcapi.ogc.org/common) especifica blocos de construção que são partilhados pela maioria ou por todas as normas da OGC API, a fim de garantir a consistência em toda a família de APIs. No decorrer do desenvolvimento de Arquiteturas Orientadas a Recursos e APIs Web, algumas práticas revelaram-se comuns a todas as normas OGC API. A finalidade desta norma é documentar essas práticas. Também serve como uma **base comum** sobre a qual todas as OGC APIs serão construídas.

!!! note
    Este módulo de tutorial não tem a intenção de substituir a própria norma **OGC API - Common - Parte 1: Core** ou da candidata a norma **OGC API - Common - Parte 2: Geospatial Data**. O tutorial
    foca-se intencionalmente num subconjunto de capacidades com o propósito de ser uma iniciação à utilização da norma. Consulte a [norma **OGC API -
    Common - Parte 1: Core**](https://docs.ogc.org/is/19-072/19-072.html) e a [candidata a norma **OGC API - Common - Parte 2: Geospatial Data**](https://docs.ogc.org/DRAFTS/20-024.html) para mais detalhes.

### Antecedentes

> História

  A norma OGC API Common serve como a norma "OWS Common" para APIs Orientadas a Recursos da OGC. A carta de formação do grupo de trabalho da OGC API - Common foi criada em 2020 e a OGC API - Common - Parte 1: Core foi aprovada em fevereiro de 2023.

> Versões

  A versão 1.0.0 da **OGC API - Common - Parte 1: Core** é a versão
  atual mais recente 

#### Utilização

Esta norma identifica recursos, captura classes de conformidade e especifica requisitos que são aplicáveis a todas as normas da OGC API. Deve ser incluída como referência normativa por todos essas normas.

* A norma **OGC API - Common - Parte 1: Core** define os recursos e operações que DEVEM ter em comum todas as normas OGC API. Esta norma define os requisitos mínimos para que uma API seja descoberta e utilizada por qualquer cliente.
* A candidata a norma **OGC API - Common - Parte 2: Geospatial Data** fornece uma ligação comum entre a página de aterragem da API e os detalhes específicos do recurso. Essa ligação inclui metadados que descrevem as coleções de recursos alojados, parâmetros comuns para selecionar subconjuntos dessas coleções e modelos URI para identificar os mesmos.
* A candidata a norma **OGC API - Common Parte 3/OGC API - Features - Parte 5: Schemas** permite descrever o esquema lógico associado a uma coleção de dados geoespaciais.
* A candidata a norma **OGC API - Common Parte 4: Discovery within many collections** estende o endpoint ```/collections``` definido na Parte 2 com parâmetros de consulta para recuperar apenas um subconjunto das coleções; útil para implementações de API onde um grande número de coleções está disponível.

Além disso, a OGC API - Common fornece alguma informação não normativa através do [Guia do Utilizador da OGC API - Common](https://docs.ogc.org/DRAFTS/20-071.html).

#### Relação com outras normas

A imagem abaixo mostra a arquitetura de recursos na OGC API. A OGC API - Common fornece uma base comum a todas as OGC APIs.

![imagem](../assets/images/resources-ogcapi.png){width="100.0%"}

<!-- A especificação [OpenAPI](https://www.openapis.org/) é utilizada para definir os blocos de construção de API reutilizáveis. -->

### Visão geral dos Recursos

**A OGC API - Common - Parte 1: Core** define os recursos listados na
tabela seguinte:

<table>
  <tr>
    <th>Recurso</th>
    <th>Método</th>
    <th>Caminho</th>
    <th>Finalidade</th>
  </tr>
  <tr>
    <td>Página de aterragem</td>
    <td>GET</td>
    <td>/</td>
    <td>Recupera a página de aterragem. A finalidade da página de aterragem é fornecer aos clientes um ponto de partida para usar a API. Qualquer recurso exposto através de uma API pode ser acedido seguindo caminhos ou ligações a partir da página de aterragem. A página de aterragem inclui três elementos de metadados; título, descrição e atribuição. Apenas o título é obrigatório. Estes três elementos descrevem a API como um todo. Os clientes podem esperar encontrar metadados que sejam mais específicos do recurso à medida que seguem ligações e caminhos a partir da página de aterragem.</td>
  </tr>
  <tr>
    <td>Declaração de conformidade</td>
    <td>GET</td>
    <td>/conformance</td>
    <td>Fornece uma lista declarando os módulos que são implementados pela API. Estes módulos são chamados Classes de Conformidade. A lista de Classes de Conformidade é fundamental para compreender e utilizar uma OGC API Web da OGC.</td>
  </tr>
  <tr>
    <td>Definição da API</td>
    <td>GET</td>
    <td>/api</td>
    <td>Recupera a definição da API, que descreve as capacidades fornecidas por essa API. Este recurso pode ser utilizado por programadores para compreender a API, por clientes de software para ligar ao servidor, e por ferramentas de desenvolvimento para apoiar a implementação de servidores e clientes. Note que o uso de /api no servidor é opcional e a definição da API pode estar alojada num servidor completamente separado.</td>
  </tr>
</table>

A finalidade da norma em rascunho **OGC API - Common - Parte 2: Geospatial Data** é fornecer uma ligação comum entre a página de aterragem da API e os detalhes específicos do recurso. A tabela abaixo define os recursos listados nesta parte.

<table>
  <tr>
    <th>Recurso</th>
    <th>Método</th>
    <th>Caminho</th>
    <th>Finalidade</th>
  </tr>
  <tr>
    <td>Coleções</td>
    <td>GET</td>
    <td>/collections</td>
    <td>Recupera informação que descreve o conjunto de Coleções suportadas.</td>
  </tr>
  <tr>
    <td>Coleção</td>
    <td>GET</td>
    <td>/collections/{collectionId}</td>
    <td>Recupera informação descritiva sobre uma Coleção específica.</td>
  </tr>
</table>

Fornecendo uma **base comum**, a OGC API - Common destina-se a ser implementada por normas "a jusante" da OGC API
de forma uniforme e consistente. Exemplos de recursos da OGC API - Common serão apresentados no contexto de outras normas da OGC API.

## Resumo

A OGC API - Common documenta o conjunto de práticas comuns e requisitos partilhados que emergiram do desenvolvimento de Arquiteturas Orientadas a Recursos e APIs Web dentro da OGC. A norma define recursos e mecanismos de acesso que são úteis para um cliente que procura compreender as ofertas e capacidades de uma API, bem como uma ligação entre a página de aterragem da API e os detalhes específicos do recurso. Neste aprofundamento, proporcionámos uma visão geral das normas e olhamos para os recursos na parte 1 e parte 2 (em rascunho).
