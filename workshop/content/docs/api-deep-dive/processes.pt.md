---
title: Processes
---

[


    [


# OGC API - Processes[](#ogc-api-processes)

Público-alvo
Estudantes que estão familiarizados com serviços web e APIs, e querem ter
uma visão geral do padrão OGC API - Processes

Objetivos de Aprendizagem
No final do módulo os estudantes serão capazes de:

Explicar o que é o padrão OGC API - Processes
Descrever o que pode ser feito com implementações OGC API - Processes
Compreender os principais recursos ofereidos por implementações de OGC API - Processes
Compreender como submeter e gerir tarefas de processamento

## Introdução[](#introducao)

[OGC API - Processes](https://ogcapi.ogc.org/processes) é um padrão que define uma API para disponibilizar ferramentas de processamento que podem ser chamadas e combinadas a partir de muitas fontes e aplicadas a dados noutros recursos OGC API através de uma API simples.

O OGC API - Processes permite a execução de processos geoespaciais através de uma interface RESTful, suportando padrões assíncronos e síncronos de execução.

Note
Este módulo de tutorial não tem a intenção de ser uma substituição ao
OGC API - Processes padrão. O tutorial
foca intencionalmente num subconjunto de capacidades a fim de fazer com que o
estudante comece a usar o padrão. Por favor consulte o [OGC API -
Processes padrão](https://docs.ogc.org/is/20-037/20-037.html) para mais detalhes.

### Antecedentes[](#antecedentes)

História

A versão 1.0.0 foi publicada em 2021-05-14.

Versões

A versão 1.0.0 do OGC API - Processes - Parte 1: Núcleo é a versão mais recente atual

#### Utilização[](#utilizacao)
O OGC API - Processes define os seguintes conceitos fundamentais:

Processo: uma operação computacional que pode ser invocada remotamente
Execução de Processo (Job): uma instância de um processo em execução
Resultado: a saída de uma execução de processo bem-sucedida

### Visão geral de Recursos[](#visao-geral-de-recursos)

O OGC API - Processes - Parte 1: Núcleo define os recursos listados na tabela seguinte:

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

    Processos
    GET
    /processes
    Lista de processos disponíveis

    Processo
    GET
    /processes/{processId}
    Detalhes de um processo específico

    Executar processo
    POST
    /processes/{processId}/execution
    Executar um processo (modo assíncrono)

    Execução
    GET
    /execution/{executionId}
    Estado de uma execução

    Resultado
    GET
    /execution/{executionId}/results
    Resultados de uma execução

### Exemplo[](#exemplo)

Este [servidor de demonstração](https://demo.pygeoapi.io/master/processes) demonstra a API OGC API - Processes.

### Listar processos[](#listar-processos)
Para listar os processos disponíveis:

[https://demo.pygeoapi.io/master/processes](https://demo.pygeoapi.io/master/processes)

### Detalhes de um processo[](#detalhes-de-um-processo)
Para obter detalhes de um processo específico:

[https://demo.pygeoapi.io/master/processes/hello_world](https://demo.pygeoapi.io/master/processes/hello_world)

### Executar um processo[](#executar-um-processo)
Para executar um processo, envie um pedido POST com os parâmetros de entrada:

curl -X POST \
  -H &quot;Content-Type: application/json&quot; \
  -d &#39;{&quot;arguments&quot;: {&quot;name&quot;: &quot;World&quot;}}&#39; \
  https://demo.pygeoapi.io/master/processes/hello_world/execution

## Resumo[](#resumo)

OGC API - Processes especifica um padrão para Web APIs que fornecem acesso a processos geoespaciais. Este aprofundamento forneceu uma visão geral do padrão e os vários Recursos e endpoints que são suportados.
