# N8N: all-in-one para quem precisa lidar com integrações e automações

A automação de marketing e as ferramentas de integração estão revolucionando a maneira como as empresas operam. Estas ferramentas fornecem soluções poderosas, porém fáceis de usar, para automatizar tarefas repetitivas de marketing e integrar múltiplos sistemas e aplicações. O [N8N](https://github.com/n8n-io/n8n) é uma solução open-source bem completa e self-hosted, por tanto econômica para quem tem um pouco de conhecimento técnico para fazer o setup.

Neste repositório registro alguns modelos de automações e trechos de códigos que uso com frequência.

## Modelos de Workflows

| Modelo         | Descrição                 |
| -------------- | ------------------------- |
| [Website Check](samples/websitecheck.md) | Webhook para validar se há um site live em um domínio |

## Templates

| Template       | Descrição                 |
| -------------- | ------------------------- |
| [Stripe → RD Station Marketing](templates/stripe-checkout-rdmkt.md) | Registra pagamentos confirmados no Stripe como evento de pedido no RD Station Marketing |

## Utilidades

| Arquivo        | Descrição                 |
| -------------- | ------------------------- |
| [Binário de/para ASCII](utils/binary-ascii.md) | Convertendo dados binários para ASCII e vice-versa |
| [Gráficos em imagem](utils/chart-images.md) | Gerando imagens de gráficos via QuickChart |
| [Datas](utils/dates.md) | Formatação e tratamento de datas |
| [JSON Query](utils/json-query.md) | Consultando e filtrando JSON com JMESPath |
| [Nomes](utils/names.md) | Separando primeiro nome e sobrenome |
| [Pivot de dados](utils/pivot-data.md) | Transformando valores de uma key em colunas |
| [Renomear arquivos](utils/renameFile.md) | Renomeando arquivo baixado com HTTP Request ou carregados do file system |

## Setup
- [Instalando o N8N na Amazon](setup-aws-lightsail.md)

## Node customizado

Desenvolvi um node customizado para integrar o N8N com o RD Station Marketing. Disponível no NPM: [n8n-nodes-rdstation-marketing](https://www.npmjs.com/package/n8n-nodes-rdstation-marketing)