# Validar site (Website Domain Check) com N8N

Este modelo de workflow ajuda a validar se um site existe.
Repare que não estou validando se o domínio é valído, mas se no endereço tem um site. Cito isso pois um domínio pode existir, ter emails e etc mas não existir um site. Ou o site estar fora do ar. É justamente isso que este workflow testa, se ao acessar o site há alguma resposta.

# Como usar?
1. Copie e cole o [JSON-modelo](https://raw.githubusercontent.com/fcarbonare/fcarbonare/main/n8n/samples/src/websitecheck.json) em um novo workflow do N8N. Você verá o fluxo abaixo:

![Modelo de workflow para validar um site com N8N](https://github.com/user-attachments/assets/4b2e8f3c-30af-4daf-9447-f1c019445234)

2. Se você quiser salvar o conteúdo (HTML) de retorno do website, edite o útimo node (saveData) e coloque as credenciais e caminho do seu bucket no AWS S3

3. Salve o workflow e ative-o

4. Abra o primeiro node (Webhook) e pegue a URL de produção

5. Faça uma requisição para GET para [URL]?host=[dominio]
Exemplo:
```
https://[url]?dominio=google.com.br
```

# Retornos

Ao checar um domínio o webhook pode retornar as seguintes respostas:

| Response code | Body    | O que significa |
| ------------- | ------- | --------------- |
| 400           | (vazio) | Bad Request, a requisição não contém os parâmetros ou métodos corretos |
| 404           | invalid | O domínio não possui um site live |
| 200           | OK      | Tudo certo, existe um site neste domínio |