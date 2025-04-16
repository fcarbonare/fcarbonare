# Separando nome e sobrenome (First and Last name)

Nome:

```
{{ $json.body.leads[0].name.split(' ')[0].trim() }}
```

Sobrenome:

```
{{ $json.body.leads[0].name.replace($json.body.leads[0].name.split(' ')[0], '').trim() }}
```