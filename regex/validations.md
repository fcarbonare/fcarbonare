# Validação de dados com expressões regulares

## Modelos de expressões regulares para validação de dados

### Website

```
^(http(s)?:\/\/.)[-a-zA-Z0-9@:%._\+~#=]{2,256}\.[a-z]{2,6}\b([-a-zA-Z0-9@:%_\+.~#?&\/\/=]*)$
```

### Email

```
^[^\s@]+@[^\s@]+\.[^\s@]+$
```

## Exemplo de uso de validação em JavaScript

```
var email = "user@domain.com";
if ( (/^[^\s@]+@[^\s@]+\.[^\s@]+$/).test(email) )
{
  console.log("Email válido");
}
else
{
  console.log("Email inválido");
}
```
