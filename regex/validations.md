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

### Social URLs

Instagram:
```
^(http(s)?:\/\/)(www\.)?instagram\.com\/(.*)
```

Linkedin personal profile:
```
^(http(s)?:\/\/)(www\.)?linkedin\.com\/in\/(.*)
```

Linkedin company profile:
```
^(http(s)?:\/\/)(www\.)?linkedin\.com\/company\/(.*)
```

Facebook:
```
^(http(s)?:\/\/)(www\.)?facebook\.com\/(.*)
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

## Ferramenta online para testar e debugar regex:
- [Regex101](https://regex101.com/)
