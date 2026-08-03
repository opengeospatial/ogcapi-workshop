---
title: Segurança e OGC APIs
---

# Segurança e OGC APIs

As OGC APIs são desenhadas usando tecnologias modernas a fim de reduzir a barreira aos dados, serviços e processos geoespaciais.

## SSL/TLS

As OGC APIs podem ser implementadas usando HTTP ou HTTPS. Recomenda-se fortemente implementar quaisquer serviços usando HTTPS para que os clientes
possam validar e verificar a autenticidade dos seus serviços conforme necessário. Dependendo de como o seu sistema está arquitetado, isto pode significar
aplicar Secure Sockets Layer/Transport Layer Security (SSL/TLS) no seu serviço host, ou se tiver uma arquitetura de implementação multicamadas,
aplicando como parte dos seus serviços front-end, momento em que a comunicação interna/interna pode ou não estar implementada
usando HTTP.

## Controlo de acesso

Os Padrões Abertos e APIs não são apenas para Dados Abertos. Implementar controlo de acesso (autenticação, autorização) é um componente crítico
de muitas infraestruturas e sistemas a fim de manter a integridade de dados, autoridade e confiança. Exemplos de necessidade de controlo de acesso em
OGC APIs incluem (mas não se limitam a):

- proteger todos os endpoints
- proteger apenas endpoints específicos
- permitir capacidades de inserção/atualização/eliminação de itens numa coleção
- permitir capacidades de inserção/atualização/eliminação em coleções

Dado que existem preocupações, implementações e arquiteturas de controlo de acesso para muitos domínios, é melhor aproveitar os padrões da indústria
para implementação. Uma vez que os padrões OGC API aproveitam a especificação OpenAPI para descrições de serviço, pode usar o
[Objeto de Esquema de Segurança](https://spec.openapis.org/oas/v3.0.3#security-scheme-object) do OpenAPI para descrever (não implementar!) o(s) mecanismo(s) de controlo de acesso para
toda a API bem como para um caminho/operação específica da API.

Os esquemas de segurança OpenAPI suportados incluem:

- Chave de API (`apiKey`)
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

Controlo de acesso usando uma chave de API:
```json
"security": {
  "default": {
    "type": "apiKey",
    "name": "api-key",
    "in": "query",
    "description": "Por favor consulte https://example.org/contact-us para mais informação"
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
    "description": "Por favor consulte https://example.org/contact-us para mais informação",
    "scopes": {
        "read:roads": "ler coleção de estradas",
        "write:roads": "modificar estradas na coleção de estradas"
  }
}
```

!!! note
    A implementação do acima pressupõe que os mecanismos de controlo de acesso necessários estão em lugar.
