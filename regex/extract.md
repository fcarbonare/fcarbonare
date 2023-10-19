# Expressões regulares para extração de dados

## Extrair o domínio a partir de uma URL

```
/^(?:https?:\/\/)?(?:[^@\n]+@)?(?:www\.)?([^:\/\n]+)/im
```

Exemplo de uso em JavaScript:

```
var website = "https://github.com/";
var domain = website.match(/^(?:https?:\/\/)?(?:[^@\n]+@)?(?:www\.)?([^:\/\n]+)/im)[1];
console.log(domain);
```

