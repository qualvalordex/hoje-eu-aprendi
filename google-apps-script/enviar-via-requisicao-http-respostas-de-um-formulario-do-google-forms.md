No começo de tudo, aprendi como criar e vincular um script a um app do Google (i. e. Forms, Docs, Sheets). Existe um [overview](https://developers.google.com/apps-script/overview) de como criar esses scripts e mais detalhes sobre o funcionamento do serviço podem ser vistos na [documentação](https://developers.google.com/apps-script/reference).

O script criado nesse mini-aprendizado foi o seguinte:

```js
function onFormSubmitHandler(event) {
  // Form ID é obtido da URL:
  // https://docs.google.com/forms/d/{form-id}/edit
  let form = FormApp.openById("form-id");
  let formResponses = form.getResponses();

  // Obter o total de respostas do formulário
  let countResponses = formResponses.length;

  // Pegar somente a última resposta
  let lastResponse = formResponses[countResponses - 1];
  let lastResponseItems = lastResponse.getItemResponses();

  // Extrair as respostas a cada item da última resposta do formulário
  let reporter = lastResponseItems[0].getResponse();
  let contact = lastResponseItems[1].getResponse();
  let description = lastResponseItems[2].getResponse();

  // Definir URL e mensagem que será enviada no Discord
  let uri =
    "https://discord.com/api/webhooks/{discord-webhook-id}/{discord-webhook-token}";
  let message = `Você tem um novo bug reportado:\n- Reportador: ${reporter}\n- Contato: ${contact}\n- Descrição do bug: ${description}`;

  // Montar o payload da requisição HTTP
  let options = {
    method: "post",
    payload: {
      content: message,
    },
  };

  // Efetuar a requisição HTTP
  var response = UrlFetchApp.fetch(uri, options);
}
```

Essa função é ativada toda vez que o usuário envia respostas em um formulário criado na minha conta. Adicionei um "algo a mais" fazendo uma requisição HTTP para o [Webhook Resource](https://discord.com/developers/docs/resources/webhook) do Discord. Assim, sempre que eu receber um _Bug Report_ serei notificado no meu servidor!
