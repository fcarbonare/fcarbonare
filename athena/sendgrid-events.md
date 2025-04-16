# Consultando eventos do SendGrid com AWS Athena

## Configuração

1. Configure a integração do webhook com sua conta SendGrid para armazenar eventos em um bucket S3, seguindo o guia abaixo:  
- [Microserviço para Gerenciar Webhooks de Eventos do SendGrid](https://www.twilio.com/en-us/blog/microservice-template-handle-sendgrid-event-webhooks#Part-2-Serverless-Microservice-for-handling-SendGrid-Event-Webhooks)

2. Configure o AWS Glue para rastrear os dados seguindo este guia:  
[Análise de Entregabilidade de E-mails usando SendGrid e Serviços de Big Data da AWS](https://medium.com/zenofai/email-deliverability-analytics-using-sendgrid-and-aws-big-data-services-136fb4cd0021)


# Doc links
- [SendGrid Event Webhook Reference](https://www.twilio.com/docs/sendgrid/for-developers/tracking-events/event)