# novu_click

```
CREATE OR REPLACE VIEW "sg_novu_click" AS 
SELECT 
    element_at(REGEXP_EXTRACT_ALL("item"."novutransactionid", '(\d+)'), 1) as "connection_id",
    'novu_click' as "meta_key",
    to_iso8601(from_unixtime(MIN("item"."timestamp")/1000)) as "created_at", 
    to_iso8601(from_unixtime(MAX("item"."timestamp")/1000)) as "updated_at", 
    COUNT() as "meta_value"
FROM 
    "data" 
WHERE 
    "item"."event" = 'click' AND
    "item"."novuworkflowidentifier" = '[workflow-name]' AND
    NOT REGEXP_LIKE("item"."useragent", '360Spider|acapbot|acoonbot|ahrefs|alexibot|asterias|attackbot|backdorbot|becomebot|binlar|blackwidow|blekkobot|blexbot|blowfish|bullseye|bunnys|butterfly|careerbot|casper|checkpriv|cheesebot|cherrypick|chinaclaw|choppy|clshttp|cmsworld|copernic|copyrightcheck|cosmos|crescent|cy_cho|datacha|demon|diavol|discobot|dittospyder|dotbot|dotnetdotcom|dumbot|emailcollector|emailsiphon|emailwolf|exabot|extract|eyenetie|feedfinder|flaming|flashget|flicky|foobot|g00g1e|getright|gigabot|go-ahead-got|gozilla|grabnet|grafula|harvest|heritrix|httrack|icarus6j|jetbot|jetcar|jikespider|kmccrew|leechftp|libweb|linkextractor|linkscan|linkwalker|loader|masscan|miner|majestic|mechanize|mj12bot|morfeus|moveoverbot|netmechanic|netspider|nicerspro|nikto|ninja|nutch|octopus|pagegrabber|planetwork|postrank|proximic|purebot|pycurl|python|queryn|queryseeker|radian6|radiation|realdownload|rogerbot|scooter|seekerspider|semalt|siclab|sindice|sistrix|sitebot|siteexplorer|sitesnagger|skygrid|smartdownload|snoopy|sosospider|spankbot|spbot|sqlmap|stackrambler|stripper|sucker|surftbot|sux0r|suzukacz|suzuran|takeout|teleport|telesoft|true_robots|turingos|turnit|vampire|vikspider|voideye|webleacher|webreaper|webstripper|webvac|webviewer|webwhacker|winhttp|wwwoffle|woxbot|xaldon|xxxyy|yamanalab|yioopbot|youda|zeus|zmeu|zune|zyborg') 
GROUP BY
    element_at(REGEXP_EXTRACT_ALL("item"."novutransactionid", '(\d+)'), 1)
ORDER BY
    element_at(REGEXP_EXTRACT_ALL("item"."novutransactionid", '(\d+)'), 1) ASC
```

# novu_open

```
CREATE OR REPLACE VIEW "sg_novu_open" AS 
SELECT 
    element_at(REGEXP_EXTRACT_ALL("item"."novutransactionid", '(\d+)'), 1) as "connection_id",
    'novu_open' as "meta_key",
    to_iso8601(from_unixtime(MIN("item"."timestamp")/1000)) as "created_at", 
    to_iso8601(from_unixtime(MAX("item"."timestamp")/1000)) as "updated_at", 
    COUNT() as "meta_value"
FROM 
    "data" 
WHERE 
    "item"."event" = 'open' AND
    "item"."novuworkflowidentifier" = 'new-connection' AND
    NOT REGEXP_LIKE("item"."useragent", '360Spider|acapbot|acoonbot|ahrefs|alexibot|asterias|attackbot|backdorbot|becomebot|binlar|blackwidow|blekkobot|blexbot|blowfish|bullseye|bunnys|butterfly|careerbot|casper|checkpriv|cheesebot|cherrypick|chinaclaw|choppy|clshttp|cmsworld|copernic|copyrightcheck|cosmos|crescent|cy_cho|datacha|demon|diavol|discobot|dittospyder|dotbot|dotnetdotcom|dumbot|emailcollector|emailsiphon|emailwolf|exabot|extract|eyenetie|feedfinder|flaming|flashget|flicky|foobot|g00g1e|getright|gigabot|go-ahead-got|gozilla|grabnet|grafula|harvest|heritrix|httrack|icarus6j|jetbot|jetcar|jikespider|kmccrew|leechftp|libweb|linkextractor|linkscan|linkwalker|loader|masscan|miner|majestic|mechanize|mj12bot|morfeus|moveoverbot|netmechanic|netspider|nicerspro|nikto|ninja|nutch|octopus|pagegrabber|planetwork|postrank|proximic|purebot|pycurl|python|queryn|queryseeker|radian6|radiation|realdownload|rogerbot|scooter|seekerspider|semalt|siclab|sindice|sistrix|sitebot|siteexplorer|sitesnagger|skygrid|smartdownload|snoopy|sosospider|spankbot|spbot|sqlmap|stackrambler|stripper|sucker|surftbot|sux0r|suzukacz|suzuran|takeout|teleport|telesoft|true_robots|turingos|turnit|vampire|vikspider|voideye|webleacher|webreaper|webstripper|webvac|webviewer|webwhacker|winhttp|wwwoffle|woxbot|xaldon|xxxyy|yamanalab|yioopbot|youda|zeus|zmeu|zune|zyborg') 
GROUP BY
    element_at(REGEXP_EXTRACT_ALL("item"."novutransactionid", '(\d+)'), 1)
ORDER BY
    element_at(REGEXP_EXTRACT_ALL("item"."novutransactionid", '(\d+)'), 1) ASC
```

# novu_delivered

```
CREATE OR REPLACE VIEW "sg_novu_delivered" AS 
SELECT
    element_at(REGEXP_EXTRACT_ALL("item"."novutransactionid", '(\d+)'), 1) as "connection_id",
    'novu_delivered' as "meta_key",
    to_iso8601(from_unixtime(MIN("item"."timestamp")/1000)) as "created_at", 
    to_iso8601(from_unixtime(MAX("item"."timestamp")/1000)) as "updated_at", 
    COUNT() as "meta_value"
FROM    
    "data"
WHERE 
    "item"."event" = 'open' AND
    "item"."novuworkflowidentifier" = 'new-connection'
GROUP BY
    element_at(REGEXP_EXTRACT_ALL("item"."novutransactionid", '(\d+)'), 1)
ORDER BY
    element_at(REGEXP_EXTRACT_ALL("item"."novutransactionid", '(\d+)'), 1) ASC
```