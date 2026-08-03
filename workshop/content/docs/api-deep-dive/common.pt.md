---
title: Common
---

[


    [


# OGC API - Common[](#ogc-api-common)

Público-alvo
Estudantes que estão familiarizados com serviços web e APIs, e querem ter
uma visão geral do rascunho do padrão OGC API - Common

Objetivos de Aprendizagem
No final do módulo os estudantes serão capazes de:

Explicar o que é o padrão OGC API - Common
Descrever o que pode ser feito com OGC API - Common como bloco de construção

## Introdução[](#introducao)

O [OGC API - Common](https://ogcapi.ogc.org/common) especifica blocos de construção que são partilhados pela maioria ou por todos os Padrões OGC API para garantir consistência através da família. No curso do desenvolvimento de Arquiteturas Orientadas a Recursos e Web APIs, algumas práticas provaram ser comuns a todos os padrões OGC API. O objetivo deste padrão é documentar essas práticas. Serve também como uma base comum sobre a qual todas as OGC APIs serão construídas.

Note
Este módulo de tutorial não tem a intenção de ser uma substituição ao
OGC API - Common - Parte 1: Núcleo padrão ou rascunho do padrão OGC API - Common - Parte 2: Dados Geoespaciais. O tutorial
foca intencionalmente num subconjunto de capacidades a fim de fazer com que o
estudante comece a usar o padrão. Por favor consulte o [OGC API -
Common - Parte 1: Núcleo padrão](https://docs.ogc.org/is/19-072/19-072.html) e [OGC API -
Common - Parte 2: Dados Geoespaciais rascunho do padrão](https://docs.ogc.org/DRAFTS/20-024.html) para mais detalhes.

### Antecedentes[](#antecedentes)

História

O padrão OGC API Common serve como o padrão "OWS Common" para OGC APIs Orientadas a Recursos. O estatuto do SWG OGC API - Common foi criado em 2020, OGC API - Common - Parte 1: Núcleo foi aprovado em Fevereiro de 2023.

Versões

A versão 1.0.0 do OGC API - Common - Parte 1: Núcleo é a versão
  mais recente atual

#### Utilização[](#utilizacao)
Esta especificação identifica recursos, captura classes de conformidade, e especifica requisitos que são aplicáveis a todos os padrões OGC API. Deve ser incluído como uma referência normativa por todos esses padrões.

O padrão OGC API - Common - Parte 1: Núcleo define os recursos e operações que DEVEM ser comuns a todos os padrões OGC API. Este padrão define os requisitos mínimos para uma API para ser descoberta e usada por qualquer cliente.
O rascunho do OGC API - Common - Parte 2: Dados Geoespaciais padrão candidato fornece uma conexão comum entre a página inicial da API e detalhes específicos do recurso. Essa conexão inclui metadados que descrevem as coleções de recursos alojados, parâmetros comuns para selecionar subconjuntos dessas coleções, e modelos URI para identificar o acima.
O rascunho do OGC API - Common Parte 3/OGC API - Features - Parte 5: Esquemas padrão candidato permite descrever o esquema lógico associado a uma coleção de dados geoespaciais.
O rascunho do OGC API - Common Parte 4: Descoberta em muitas coleções padrão candidato estende o endpoint /collections definido na Parte 2 com parâmetros de consulta para recuperar apenas um subconjunto das coleções; útil para implementações de API onde um grande número de coleções está disponível.

Adicionalmente, OGC API - Common fornece alguma informação não normativa através do [Guia de Utilizador OGC API-Common](https://docs.ogc.org/DRAFTS/20-071.html).

#### Relação com outros padrões[](#relacao-com-outros-padroes)
A imagem abaixo mostra a arquitetura de recursos no OGC API. O OGC API - Common fornece uma base comum a todas as OGC APIs.

### Visão geral de Recursos[](#visao-geral-de-recursos)

O OGC API - Common - Parte 1: Núcleo define os recursos listados na
tabela seguinte:

<table>
  <tr>
    <th>Recurso</th>
    <th>Método</th>
    <th>Caminho</th>
    <th>Propósito</th>
  </tr>
  <tr>
    <td>Página inicial</td>
    <td>GET</td>
    <td>/</td>
    <td>Recupera a página inicial. O objetivo da página inicial é fornecer aos clientes um ponto de partida para usar a API. Qualquer recurso exposto através de uma API pode ser acedido seguindo caminhos ou ligações a partir da página inicial. A página inicial inclui três elementos de metadados; título, descrição e atribuição. Apenas o título é obrigatório. Estes três elementos descrevem a API como um todo. Os clientes podem esperar encontrar metadados que são mais específicos do recurso à medida que seguem ligações e caminhos a partir da página inicial.</td>
  </tr>
  <tr>
    <td>Declaração de conformidade</td>
    <td>GET</td>
    <td>/conformance</td>
    <td>Fornece uma lista declarando os módulos que estão implementados pela API. Estes módulos são chamados Classes de Conformidade. A lista de Classes de Conformidade é fundamental para compreender e usar uma OGC Web API.</td>
  </tr>
  <tr>
    <td>Definição da API</td>
    <td>GET</td>
    <td>/api</td>
    <td>Recupera a definição da API que descreve as capacidades fornecidas por essa API. Este recurso pode ser usado por desenvolvedores para compreender a API, por clientes de software para se ligarem ao servidor, e por ferramentas de desenvolvimento para apoiar a implementação de servidores e clientes. Note que o uso de /api no servidor é opcional e a definição da API pode ser alojada num servidor completamente separado.</td>
  </tr>
</table>

O objetivo do rascunho do padrão OGC API - Common - Parte 2: Dados Geoespaciais é fornecer uma conexão comum entre a página inicial da API e detalhes específicos do recurso. A tabela abaixo define os recursos listados nesta parte.

<table>
  <tr>
    <th>Recurso</th>
    <th>Método</th>
    <th>Caminho</th>
    <th>Propósito</th>
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

Fornecendo uma base comum, OGC API - Common destina-se a ser implementado por padrões OGC API "a jusante"
de forma uniforme e consistente. Exemplos de recursos OGC API - Common serão mostrados no contexto de outros padrões OGC API.

## Resumo[](#resumo)

OGC API - Common documenta o conjunto de práticas comuns e requisitos partilhados que emergiram do desenvolvimento de Arquiteturas Orientadas a Recursos e Web APIs dentro do OGC. O padrão define recursos e mecanismos de acesso que são úteis para um cliente que procura compreender as ofertas e capacidades de uma API, bem como uma conexão entre a página inicial da API e detalhes específicos do recurso. Neste aprofundamento fornecemos uma visão geral do padrão e olhamos para os recursos na parte 1 e parte 2 (rascunho).
