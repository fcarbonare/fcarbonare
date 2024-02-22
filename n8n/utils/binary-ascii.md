# Handling binary and ascii data on code node

## Binary to ASCII:

```
var data = "dGVzdA==";
var data = Buffer.from(data, 'base64').toString('binary');
console.log(data);
// test
```

## ASCII to Binary:

```
var data = "test";
var data = Buffer.from(data, 'binary').toString('base64');
console.log(data);
// dGVzdA==
```
