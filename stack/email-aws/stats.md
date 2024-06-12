# Como acompanhar principais eventos como entrega, abertura e cliques

## Estatísticas gerais pelo ID da mensagem

*Data de entrega*

```
SELECT 
    sesmaster.mail.messageid, 
    MIN(from_iso8601_timestamp(sesmaster.delivery."timestamp")) as delivered_at
FROM 
    "database"."sesmaster" 
WHERE 
    sesmaster.delivery IS NOT NULL 
GROUP BY
    sesmaster.mail.messageid
ORDER BY 
    delivered_at DESC 
LIMIT 10
```

*Data da primeira abertura*
Além de trazer o primeiro evento de abertura, filtro os useragents de bots conhecidos

```
SELECT 
    sesmaster.mail.messageid, 
    MIN(from_iso8601_timestamp(sesmaster.open."timestamp")) as opened_at
FROM 
    "database"."sesmaster" 
WHERE 
    sesmaster.open IS NOT NULL and
    NOT REGEXP_LIKE(sesmaster.open.useragent, '360Spider|acapbot|acoonbot|ahrefs|alexibot|asterias|attackbot|backdorbot|becomebot|binlar|blackwidow|blekkobot|blexbot|blowfish|bullseye|bunnys|butterfly|careerbot|casper|checkpriv|cheesebot|cherrypick|chinaclaw|choppy|clshttp|cmsworld|copernic|copyrightcheck|cosmos|crescent|cy_cho|datacha|demon|diavol|discobot|dittospyder|dotbot|dotnetdotcom|dumbot|emailcollector|emailsiphon|emailwolf|exabot|extract|eyenetie|feedfinder|flaming|flashget|flicky|foobot|g00g1e|getright|gigabot|go-ahead-got|gozilla|grabnet|grafula|harvest|heritrix|httrack|icarus6j|jetbot|jetcar|jikespider|kmccrew|leechftp|libweb|linkextractor|linkscan|linkwalker|loader|masscan|miner|majestic|mechanize|mj12bot|morfeus|moveoverbot|netmechanic|netspider|nicerspro|nikto|ninja|nutch|octopus|pagegrabber|planetwork|postrank|proximic|purebot|pycurl|python|queryn|queryseeker|radian6|radiation|realdownload|rogerbot|scooter|seekerspider|semalt|siclab|sindice|sistrix|sitebot|siteexplorer|sitesnagger|skygrid|smartdownload|snoopy|sosospider|spankbot|spbot|sqlmap|stackrambler|stripper|sucker|surftbot|sux0r|suzukacz|suzuran|takeout|teleport|telesoft|true_robots|turingos|turnit|vampire|vikspider|voideye|webleacher|webreaper|webstripper|webvac|webviewer|webwhacker|winhttp|wwwoffle|woxbot|xaldon|xxxyy|yamanalab|yioopbot|youda|zeus|zmeu|zune|zyborg') 
GROUP BY
    sesmaster.mail.messageid
ORDER BY 
    opened_at DESC 
LIMIT 10
```

*Data do primeiro click abertura*
Além de trazer o primeiro evento de click, filtro os useragents de bots conhecidos

```
SELECT 
    sesmaster.mail.messageid, 
    MIN(from_iso8601_timestamp(sesmaster.click."timestamp")) as clicked_at,
    count(sesmaster.click."link") as click_count
FROM 
    "database"."sesmaster" 
WHERE 
    sesmaster.click IS NOT NULL and
    NOT REGEXP_LIKE(sesmaster.click.useragent, '360Spider|acapbot|acoonbot|ahrefs|alexibot|asterias|attackbot|backdorbot|becomebot|binlar|blackwidow|blekkobot|blexbot|blowfish|bullseye|bunnys|butterfly|careerbot|casper|checkpriv|cheesebot|cherrypick|chinaclaw|choppy|clshttp|cmsworld|copernic|copyrightcheck|cosmos|crescent|cy_cho|datacha|demon|diavol|discobot|dittospyder|dotbot|dotnetdotcom|dumbot|emailcollector|emailsiphon|emailwolf|exabot|extract|eyenetie|feedfinder|flaming|flashget|flicky|foobot|g00g1e|getright|gigabot|go-ahead-got|gozilla|grabnet|grafula|harvest|heritrix|httrack|icarus6j|jetbot|jetcar|jikespider|kmccrew|leechftp|libweb|linkextractor|linkscan|linkwalker|loader|masscan|miner|majestic|mechanize|mj12bot|morfeus|moveoverbot|netmechanic|netspider|nicerspro|nikto|ninja|nutch|octopus|pagegrabber|planetwork|postrank|proximic|purebot|pycurl|python|queryn|queryseeker|radian6|radiation|realdownload|rogerbot|scooter|seekerspider|semalt|siclab|sindice|sistrix|sitebot|siteexplorer|sitesnagger|skygrid|smartdownload|snoopy|sosospider|spankbot|spbot|sqlmap|stackrambler|stripper|sucker|surftbot|sux0r|suzukacz|suzuran|takeout|teleport|telesoft|true_robots|turingos|turnit|vampire|vikspider|voideye|webleacher|webreaper|webstripper|webvac|webviewer|webwhacker|winhttp|wwwoffle|woxbot|xaldon|xxxyy|yamanalab|yioopbot|youda|zeus|zmeu|zune|zyborg') 
GROUP BY
    sesmaster.mail.messageid
ORDER BY 
    clicked_at DESC 
LIMIT 10
```

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

## Estatísticas de envio

```
SELECT
  sesmaster.mail.messageid, sesmaster.eventtype, sesmaster.mail."timestamp",
  MAX(CASE WHEN header.name = 'X-Campaign-Id' THEN header.value END) AS campaignid,
  MAX(CASE WHEN header.name = 'X-User-Id' THEN header.value END) AS userid,
  sesmaster.bounce."bouncetype"
FROM 
    sesmaster
    CROSS JOIN UNNEST(mail.headers) AS t (header)
WHERE 
    header.name IN ('X-Campaign-Id', 'X-User-Id') AND
    eventtype IN ('Delivery','Bounce','Reject')
GROUP BY 
    sesmaster.mail."timestamp", sesmaster.eventtype, sesmaster.mail.messageid, sesmaster.bounce."bouncetype"
```
## Extraindo dados entrega

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