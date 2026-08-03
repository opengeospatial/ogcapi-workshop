---
title: Contexto e antecedentes
---

# Contexto e antecedentes

O domínio geoespacial tem uma longa história de esforços focados na descoberta, acesso e visualização de dados.

Esta página fornece antecedentes e história dos serviços web geoespaciais, mapeamento web e plataformas de computação distribuída.

## Evolução da API geoespacial

A década de 1990 viu a implementação inicial da Arquitetura Orientada a Serviços (SOA). O primeiro padrão OGC Web Map Service (WMS)
foi publicado em 1999, fornecendo uma abordagem independente de fornecedor para visualizar mapas de dados geoespaciais numa página web.
Os serviços web tinham fortes raízes em [XML-RPC (eXtensible Markup Language over Remote Procedure Call)](http://xmlrpc.com/)
e [CORBA](https://www.omg.org/spec/CCM), e padrões e tecnologias como SOAP, WSDL e UDDI começaram a emergir
como meios para descrever, descobrir e realizar fluxo de trabalho de pedido/resposta via interface web.

A década de 2000 viu o desenvolvimento contínuo de padrões de Serviço Web do OGC como Web Feature Service (WFS), Catalogue Service
for the Web (CSW), Web Coverage Service (WCS), Web Processing Service (WPS), entre outros. Além disso, a Geography Markup Language (GML)
tornou-se um padrão oficial do OGC em apoio da troca de dados (vetoriais) padronizada através da Internet. Os serviços web
eram tipicamente desenhados com o conceito de um modelo de base de dados relacional (RDBMS) como repositório de dados/metadata backend.

No meados dos anos 2000, JavaScript, AJAX e mapas/telhas deslizantes começaram a emergir no domínio do mapeamento web, que proporcionou
padrões de design Web 2.0 que resultaram em mapas mais responsivos em páginas web na Web.

## Realidades das arquiteturas de serviço web

Os padrões de serviço web do OGC proporcionaram abordagens de ponta para descoberta, acesso e visualização de dados. Ao
mesmo tempo, à medida que o conceito de arquitetura web evoluía, várias características dos padrões de serviço web mostraram
espaço para melhoria a fim de evoluir:

- XML: embora o XML fosse/seja um formato de codificação/representação comprovado e extensível, trabalhar com XML num ambiente de desenvolvimento web
  revelou-se incómodo (análise para objetos dedicados). Além disso, a natureza verbosa do XML revelou-se cara
  para trabalhar na Web para transferência de grandes cargas de dados
- Construir uma camada de transporte especializada em cima do HTTP: o HTTP (o protocolo) em si fornecia mecanismos nativos de pedido/resposta
  (códigos de erro, negociação de conteúdo), que eram tipicamente definidos adicionalmente dentro dos padrões de serviço web.
  Por exemplo, uma exceção HTTP 400 comunica nativamente um pedido defeituoso, enquanto uma exceção HTTP 200 indica
  uma resposta bem-sucedida. Os padrões de serviço web eram comumente desenvolvidos onde uma resposta 200 poderia indicar um pedido defeituoso (onde o cliente teria de inspecionar o conteúdo de uma resposta HTTP, em vez do código de estado HTTP real
- Especificações: as especificações de serviço web eram tipicamente completas em funcionalidades e desenvolvidas com uma solução 100% em mente,
  o que provava ser desafiante implementar um servidor ou cliente totalmente compatível, por exemplo
- Desafios web: as especificações de serviço web eram difíceis de implementar para desenvolvedores web e tipicamente requeriam
  experiência especializada em domínio geoespacial para interpretar e compreender os requisitos de especificação. Além disso, os serviços web eram difíceis de integrar com motores de busca principais da Internet

## Ser "webby": um novo paradigma

Em 2017, a W3C publicou as [Spatial Data on the Web Best Practices](https://www.w3.org/TR/sdw-bp), que forneceram
recomendações sobre formatos de dados, identificadores, acesso, licenças e proveniência. O objetivo desta boa prática era
fornecer uma linha de base de recomendações para integrar dados e serviços geoespaciais com práticas e
padrões de design principais da Web. Além disso, o OGC publicou o OGC API Whitepaper descrevendo, discutindo APIs e próximos passos
para o OGC na altura. Ficou óbvio que era necessário um "recomeço limpo", a fim de que as OGC APIs se tornassem mais
"da Web" e reduzissem a barreira para não especialistas do domínio.

Um novo paradigma emergiu, que destacou os seguintes conceitos:

- ser "webby" (humanos, motores de busca)
- amigável para desenvolvedores
- desenvolvimento de especificações leve
- mudar de orientado a serviços para orientado a recursos: remover o uso do HTTP como túnel:
    - orientado a serviços: `/ows?request=GetFeature&typename=roads&featureid=5`
    - orientado a recursos: `/api/collections/roads/items/5`
- desenvolvimento de especificações modular
  - especificações de núcleo e extensão, permitindo implementação e adoção com baixa barreira para o mercado massivo/a Web
 
Em 2018, o OGC começou a realizar vários hackathons, começando o trabalho no WFS3 (agora OGC API - Features - Part 1: Core), bem como uma Weather on the Web
API (agora OGC API - Environmental Data Retrieval). Isto representou as origens do movimento OGC API!

Os processos de desenvolvimento e trabalho de desenvolvimento de padrões do OGC evoluíram durante este tempo. As especificações OGC API começaram a ser
desenvolvidas em repositórios públicos no GitHub, permitindo que qualquer pessoa do público discutisse e colaborasse para um dado padrão OGC API
abertamente no GitHub. Além disso, as próprias especificações começaram a ser desenvolvidas em AsciiDoc (um formato aberto para documentação/markup), e
postas disponíveis como páginas HTML (e PDF). As ferramentas colaborativas usadas pelo OGC também proliferaram, como Gitter/Element bem como Discord.

!!! note
    Os padrões do OGC, embora desenvolvidos principalmente no GitHub, são votados pela adesão do OGC.

## Resumo

Os Serviços Web Geoespaciais e APIs têm sido uma atividade de longa duração no domínio geoespacial. Os padrões OGC API são desenhados com base nas lições
aprendidas de esforços passados, e construídos para ter baixa barreira, com foco em recursos (dados/conteúdo!) usando práticas e princípios modernos de desenvolvimento web.
