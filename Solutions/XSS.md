Answer:
escape content:

```JS
import escape from 'lodash.escape';

  

function handleMessageSend(messageId, senderEmail, messageContent)  {

  database.save(messageId, senderEmail, messageContent);

}

  

function generateMessageHTML(messageId) {

  let messageContent = database.loadContent(messageId);

  let escapedContent = escape(messageContent);

  return `<p class="messageContent">${escapedContent}</p>`;

}
```

Input validation

```JS
import escape from 'lodash.escape';

import isEmail from 'validator/lib/isEmail.js';

import isUUId from 'validator/lib/isUUID.js';

  

function handleMessageSend(messageId, senderEmail, messageContent)  {

  if (!isUUId(messageId)) {

    throw new Error("validation of messageId parameter failed");

  }

  

  if (!isEmail(senderEmail)) {

    throw new Error("validation of email parameter failed");

  }

  

  database.save(messageId, senderEmail, messageContent);

}

  

function generateSenderHTML(messageId) {

  let messageSender = database.loadSender(messageId);

  let escapedSender = escape(messageSender);

  return `<div class="messageSender">${escapedSender}</div>`;

}
```


Sanitization:

```JS

import * as DOMPurify from 'dompurify';

  

function handleMessageSend(messageId, senderEmail, messageContent)  {

  database.save(messageId, senderEmail, messageContent);

}

  

function generateMessageHTML(messageId) {

  let messageContent = database.loadContent(messageId);

  let sanitizedContent = DOMPurify.sanitize(messageContent);

  return `<p class="messageContent">${sanitizedContent}</p>`;

}
```


Can we use CSP to prevent XSS here and How?
