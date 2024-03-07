# Funções úteis para lidar com datas

O N8N usa a lib [Luxon](https://moment.github.io/luxon/#/) para tratar datas.

## Formatar data

A partir de variável do node anterior:
```
{{ new DateTime($json.xxx).toFormat('dd/LL/yyyy HH:mm:ss') }}
```

A partir do dia de hoje:
```
{{ $today.toFormat('dd/LL/yyyy') }}
```

- [Veja todas as opções de parâmetros de formatação](https://moment.github.io/luxon/#/formatting?id=table-of-tokens)

## Subtrair dias

A partir de variável do node anterior:
```
{{ new DateTime($json.xxx).minus(1, "day") }}
```

A partir do dia de hoje:
```
{{ $today.minus(1, "month")  }}
```

## Parse data considerando o timezone e formata resultado

```
{{ DateTime.fromISO($json["created_at"]).toFormat("dd/LL/yyyy hh:mm:ss") }}
```
