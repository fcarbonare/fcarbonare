# Pivot data
Transforma o valor de uma key do array em coluna

```
const novoObjeto = { json: {} };
for (const item of $input.all()) {
  novoObjeto.json[ item.json.status ] = item.json.requests;
}

return [novoObjeto];
```

Exemplo de entrada:
```
[
  {
    "status": "pending",
    "requests": 3945
  },
  {
    "status": "accepted",
    "requests": 150
  },
  {
    "status": "declined",
    "requests": 1
  },
  {
    "status": "total_connections",
    "requests": 4096
  }
]
```

Resultado:
```
[
  {
    "pending": 3945,
    "accepted": 150,
    "declined": 1,
    "total_connections": 4096
  }
]
```
