# Como acompanhar principais eventos como entrega, abertura e cliques

## Extraindo dados dos headers adicionados aos emails disparados

```
SELECT
  sesmaster.mail.messageid, sesmaster.eventtype,
  MAX(CASE WHEN header.name = 'X-Notification-Type' THEN header.value END) AS notification_type,
  MAX(CASE WHEN header.name = 'X-Message-Id' THEN header.value END) AS message_id,
  MAX(CASE WHEN header.name = 'X-Order-Id' THEN header.value END) AS order_id,
  MAX(CASE WHEN header.name = 'X-Message-To' THEN header.value END) AS message_to
FROM sesmaster
CROSS JOIN UNNEST(mail.headers) AS t (header)
WHERE 
    header.name IN ('X-Notification-Type', 'X-Message-Id', 'X-Message-To', 'X-Order-Id') and
    eventtype NOT IN ('Open','Click')
GROUP BY sesmaster.eventtype, sesmaster.mail.messageid
```

### Links úteis
- [Analyzing Amazon SES event data with AWS Analytics Services](https://aws.amazon.com/blogs/messaging-and-targeting/analyzing-amazon-ses-event-data-with-aws-analytics-services/)
- [Configuring custom domains to handle open and click tracking](https://docs.aws.amazon.com/ses/latest/dg/configure-custom-open-click-domains.html)
- [How to query Athena from N8N](https://community.n8n.io/t/how-to-connect-aws-athena-dbs-to-n8n/19395/4)
- [Get data from Amazon Athena with nodeJS](https://medium.com/@vitaliyye/get-data-from-amazon-athena-with-nodejs-4519ddd2d6c5)