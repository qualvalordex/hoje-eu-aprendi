Quando fazemos uma chamada http que retorna um status code fora do range 2xx, o axios ejeta essa resposta como erro.

Exemplo: possuo uma API que consome outra API que retorna status code 404 quando não encontra um registro e preciso retornar esse mesmo código para o meu cliente.

```js
const axios = require("axios");

const options = {
  url: "<path_to_client_service>",
  method: "post",
  data: {
    cpf: "<user_document>",
  },
};

try {
  const request = axios.request(options);
} catch (error) {
  if (error.response.code === 404) {
    return { statusCode: 404, message: "User not found." };
  }
}
```
