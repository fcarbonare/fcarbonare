# Extract all link
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
