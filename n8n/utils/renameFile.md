# Renomear um arquivo binario

1. Crie um nó do tipo CODE
2. Mode: Run Once for Each Item
3. Adicione o código:
```
$input.item.binary.data.fileName =  "novo-nome.tex";

return $input.item;
```

## Nó de modelo (copy+paste)
```
{
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "xx"
  },
  "nodes": [
    {
      "parameters": {
        "mode": "runOnceForEachItem",
        "jsCode": "$input.item.binary.data.fileName =  \"novo-nome.ext\";\n\nreturn $input.item;"
      },
      "id": "646bc502-5eb5-44eb-b1ee-faa678a8aeb3",
      "name": "renameFile",
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        1940,
        540
      ]
    }
  ],
  "connections": {},
  "pinData": {}
}
```