# Pipedrive

Ferramentas standalone em HTML para extrair dados de configuração do Pipedrive via API. Basta abrir o arquivo no browser, colar o API token e copiar o resultado em Markdown.

O token é enviado diretamente para `api.pipedrive.com` e nunca é armazenado ou repassado.

> **Como obter o API token:** Pipedrive → Settings → Personal preferences → API

## Ferramentas

| Ferramenta | Descrição |
| ---------- | --------- |
| [Custom Fields Extractor](pipedrive-field-extractor.html) | Lista todos os campos customizados (Deals, Persons, Organizations, Leads, Activities, Products) com nome, tipo e API key. Gera também uma tabela com as opções de campos do tipo enum, set, varchar_auto, user, org e people. |
| [Config Extractor](pipedrive-config-extractor.html) | Lista Pipelines, Stages (com pipeline de origem) e Activity Types com seus respectivos IDs e configurações. |
