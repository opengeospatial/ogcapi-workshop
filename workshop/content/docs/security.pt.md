---
title: Segurança e OGC APIs
---

# Segurança e OGC APIs

As OGC APIs são desenhadas utilizando tecnologias modernas a fim de baixar a barreira de entrada para dados, serviços e processos geoespaciais.

## SSL/TLS

As OGC APIs podem ser implementadas usando HTTP ou HTTPS. Recomenda-se fortemente a implementação de quaisquer serviços usando HTTPS para que os clientes
possam validar e verificar a autenticidade dos vossos serviços de acordo. Dependendo de como o vosso sistema é arquitetado, isto pode significar
aplicar Secure Sockets Layer/Transport Layer Security (SSL/TLS) no vosso serviço de alojamento, ou, se tiverdes uma arquitetura de implementação multicamada,
aplicando como parte dos vossos serviços front-end, altura em que a comunicação interna/interna pode ou não ser implementada
usando HTTP.

## Controlo de acesso

Os Padrões Abertos e APIs não são apenas para Dados Abertos. Implementar controlo de acesso (autenticação, autorização) é um componente crítico
de muitas infraestruturas e sistemas a fim de manter a integridade dos dados, autoridade e confiança. Exemplos de requisitos de controlo de acesso em
OGC APIs incluem (mas não estão limitados a):

- proteger todos os endpoints
- proteger apenas endpoints específicos
- permitir capacidades de inserção/atualização/eliminação de itens numa coleção
- permitir capacidades de inserção/atualização/eliminação de coleções

Dado que questões de controlo de acesso, implementações e arquiteturas existem para muitos domínios, é melhor aproveitar os padrões da indústria
para implementação. Dado que os padrões OGC API aproveitam a especificação OpenAPI para descrições de serviços, pode usar o OpenAPI
[Security Scheme Object](https://spec.openapis.org/oas/v3.0.3#security-scheme-object) para descrever (não implementar!) o(s) mecanismo(s) de controlo de acesso para a
API inteira, bem como para um caminho/operação específica da API.

Os esquemas de segurança OpenAPI suportados incluem:

- Chave API (`apiKey`)
- Autenticação HTTP (`http`)
- Fluxos comuns OAuth2 (`oauth2`)
- OpenID Connect Discovery (`openIdConnect`)


Controlo de acesso usando autenticação HTTP Basic:
```json
"security": {
  "default": {
    "type": "http",
    "scheme": "basic",
    "description": "Por favor entre em contacto para informação de acesso"
  }
}
```

Controlo de acesso usando uma chave API:
```json
"security": {
  "default": {
    "type": "apiKey",
    "name": "api-key",
    "in": "query",
    "description": "Consulte https://example.org/contact-us para mais informações"
  }
}
```

Controlo de acesso usando OAuth2:
```json
"security": {
  "default": {
    "type": "oauth2",
    "authorizationUrl": "https://example.org/oauth/authorize",
    "flow": "implicit",
    "description": "Consulte https://example.org/contact-us para mais informações"
    "scopes": {
        "read:roads": "ler coleção de estradas",
        "write:roads": "modificar estradas na coleção de estradas"
  }
}
```

!!! note
    A implementação do acima pressupõe que os mecanismos de controlo de acesso necessários estão em vigor.
