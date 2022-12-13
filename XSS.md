Exaplin Escaping output VS Input Sanitization VS input Validation for XSS prevention.

```JS
function handleMessageSend(messageId, senderEmail, messageContent)  {

  database.save(messageId, senderEmail, messageContent);

}

  

function generateMessageHTML(messageId) {

  let messageContent = database.loadContent(messageId);

  return `<p class="messageContent">${messageContent}</p>`;

}
```


[Password Storage](./Insecure_Password_Storage)