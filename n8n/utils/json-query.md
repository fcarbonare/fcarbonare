# JSON query

https://jmespath.org/

[].comment

[].{comment: comment, replies: replies[].reply}

```
{{ $jmespath($json.comments,'[].{comment: comment, replies: replies[].reply}') }}
```