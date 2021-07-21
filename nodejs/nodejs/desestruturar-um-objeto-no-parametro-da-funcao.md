Suponha que exista o objeto

```js
const resposta = {
  statusCode: 200,
  body: {
    message: "Hello worrld!",
  },
};
```

Caso nossa função trabalhe somente com o `statusCode`, podemos fazer a desestruturação diretamente no parâmetro:

```js
const funcao = ({ statusCode }) => {
  console.log(statusCode);
};
```
