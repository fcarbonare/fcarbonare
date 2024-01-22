# Extract all links
```
SELECT 
  ARRAY_DISTINCT(
    REGEXP_EXTRACT_ALL(
      data, '(?:(http(s)?:\/\/.)[-a-zA-Z0-9@:%._\+~#=]{2,256}\.[a-z]{2,6}\b([-a-zA-Z0-9@:%_\+.~#?&\/\/=]*))'
    )
  ) AS links 
FROM 
  "blanc-bi"."website_check" 
limit 
  10;

```

# Filter extracted links by domain - instagram / facebook
```
SELECT 
  host, 
  FILTER(ARRAY_DISTINCT(
    REGEXP_EXTRACT_ALL(
      data, '(?:(http(s)?:\/\/.)[-a-zA-Z0-9@:%._\+~#=]{2,256}\.[a-z]{2,6}\b([-a-zA-Z0-9@:%_\+.~#?&\/\/=]*))'
    )
  ), x -> x like '%instagram.com/%') AS instagram,
  FILTER(ARRAY_DISTINCT(
    REGEXP_EXTRACT_ALL(
      data, '(?:(http(s)?:\/\/.)[-a-zA-Z0-9@:%._\+~#=]{2,256}\.[a-z]{2,6}\b([-a-zA-Z0-9@:%_\+.~#?&\/\/=]*))'
    )
  ), x -> x like '%facebook.com/%') AS facebook 
FROM 
  "blanc-bi"."website_check" 
limit 
  100;
```
