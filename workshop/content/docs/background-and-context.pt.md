---
title: Antecedentes e contexto
---

# Antecedentes e contexto

O domínio geoespacial tem uma longa história de esforços focados na descoberta, acesso e visualização de dados.

Esta página fornece antecedentes e história dos serviços web geoespaciais, mapeamento web e plataformas de computação distribuída.

## Evolução da API geoespacial

A década de 1990 viu a implementação inicial da Arquitetura Orientada a Serviços (SOA). A primeira norma OGC Web Map Service (WMS)
foi publicado em 1999, fornecendo uma abordagem neutra relativamente ao fornecedor para visualizar mapas de dados geoespaciais numa página
web. Os serviços web tinham raízes fortes em [XML-RPC (eXtensible Markup Language over Remote Procedure Call)](http://xmlrpc.com/)
e [CORBA](https://www.omg.org/spec/CCM), e normas e tecnologias como SOAP, WSDL e UDDI começaram a emergir
como meios para descrever, descobrir e executar fluxos de trabalho de pedido/resposta através de uma interface web.

A década de 2000 viu o contínuo desenvolvimento de normas de Serviços Web da OGC, como Web Feature Service (WFS), Catalogue Service
for the Web (CSW), Web Coverage Service (WCS), Web Processing Service (WPS), entre outros. Além disso, o Geography Markup Language (GML)
tornou-se uma norma oficial da OGC em apoio da troca de dados (vetoriais) normalizada através da Internet. Os serviços web
eram tipicamente desenhados com o conceito de um modelo de base de dados relacional (RDBMS) como repositório de dados/metadados de backend.

A meados da década de 2000, JavaScript, AJAX e mapas interativos/tiles começaram a emergir no domínio do mapeamento web, que proporcionou
normas de design Web 2.0 que resultaram em mapas mais interativos em páginas web através da Web.

## Realidades das arquiteturas de serviços web

As normas de Serviços Web da OGC proporcionaram abordagens de ponta para a descoberta, acesso e visualização de dados. Ao
mesmo tempo, à medida que o conceito de arquitetura Web evoluía, várias características das normas de Serviços Web mostravam
margem para melhorias a fim de evoluir:

- XML: embora o XML tenha sido/seja uma codificação/representação comprovada e extensível, trabalhar com XML num ambiente de desenvolvimento web
  revelou-se trabalhoso (análise para objetos dedicados). Além disso, a natureza verbosa do XML revelou-se dispendiosa
  para trabalhar através da Web para transferência de grandes cargas de dados
- Construir uma camada de transporte especializada sobre o HTTP: o próprio HTTP (o protocolo) fornecia mecanismos nativos de pedido/resposta
  (códigos de erro, negociação de conteúdo), que eram tipicamente definidos adicionalmente dentro das normas de Serviços Web.
  Por exemplo, uma exceção HTTP 400 comunica nativamente um pedido incorreto, ao passo que uma exceção HTTP 200 indica
  uma resposta bem-sucedida. As normas de Serviços Web eram frequentemente desenvolvidas de forma que uma resposta 200 pudesse indicar um pedido incorreto
  (em que o cliente teria de inspecionar o conteúdo de uma resposta HTTP, em vez do código de estado HTTP efetivo)
- Especificações: as especificações de Serviços Web eram tipicamente completas em funcionalidade e desenvolvidas com uma solução a 100% em mente,
  o que se revelou desafiante para implementar um servidor ou cliente totalmente conforme, por exemplo
- Desafios Web: as especificações de Serviços Web eram difíceis de implementar para desenvolvedores web e normalmente requeriam
  experiência especializada em domínios geoespaciais para interpretar e compreender os requisitos da especificação. Além disso, os Serviços Web
  eram difíceis de integrar com motores de pesquisa da Internet mainstream

## Ser web: um novo paradigma

Em 2017, a W3C publicou as [Spatial Data on the Web Best Practices](https://www.w3.org/TR/sdw-bp), que forneceu
recomendações sobre formatos de dados, identificadores, acesso, licenciamento e proveniência. O objetivo desta melhor prática era
fornecer uma linha de base de recomendações para integrar dados e serviços geoespaciais com práticas e
normas de design web mainstream. Além disso, a OGC publicou o OGC API Whitepaper descrevendo, discutindo APIs e próximos passos
para a OGC na altura. Ficou claro que era necessária uma "ruptura total", a fim de as OGC APIs se tornarem mais
"da Web" e com barreiras de entrada mais baixas para não especialistas do domínio.

Um novo paradigma emergiu, destacando os seguintes conceitos:

- ser web (ser "webby") (humanos, motores de pesquisa)
- amigável para desenvolvedores
- desenvolvimento de especificações leve
- passar de orientado a serviços para orientado a recursos: remover o uso do HTTP como túnel:
    - orientado a serviços: `/ows?request=GetFeature&typename=roads&featureid=5`
    - orientado a recursos: `/api/collections/roads/items/5`
- desenvolvimento de especificações modulares
  - especificações centrais e de extensão, permitindo implementação e adoção com barreiras de entrada baixas para o mercado de massa/a Web

Em 2018, a OGC começou a organizar vários hackathons, começando o trabalho no WFS3 (atualmente OGC API - Features - Part 1: Core), bem como uma Weather on the Web
API (atualmente OGC API - Environmental Data Retrieval). Isto representou as origens do movimento da OGC API!

Os processos de desenvolvimento e de trabalho de desenvolvimento de normas da OGC evoluíram durante este período. As especificações da OGC API começaram a ser
desenvolvidas em repositórios GitHub públicos, permitindo a qualquer pessoa do público discutir e colaborar para uma dada norma da OGC API
abertamente no GitHub. Além disso, as próprias especificações começaram a ser desenvolvidas em AsciiDoc (um formato aberto para documentação/markup) e
tornadas disponíveis como páginas HTML (e PDF). As ferramentas colaborativas utilizadas pela OGC também se proliferaram, como Gitter/Element, bem como Discord.

!!! note
    As normas da OGC, embora desenvolvidos primariamente no GitHub, são votados pelos membros da OGC.

## Resumo

Os Serviços Web e APIs Geoespaciais têm sido uma atividade de longa data no domínio geoespacial. As normas OGC API são desenhadas com base nas lições
aprendidas de esforços passados, e construídos para terem barreiras de entrada baixas, com foco em recursos (dados/conteúdo!) utilizando práticas modernas de desenvolvimento web
e princípios.
