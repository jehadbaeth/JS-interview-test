# Promise.allSettled()

Assume the following JS code:


```JS
let promise1 = Promise.resolve("OK");  
let promise2 = Promise.reject("Not OK");  
let promise3 = Promise.resolve("After not ok");  
Promise.allSettled([promise1, promise2, promise3])  
    .then((results) => console.log(results))  
    .catch((err) => console.log("error: " + err));

```

what will be the output and why? 

What will be the output when replacing `promise.allSettled()` with `promise.all()` in line 4?
```hidden
[  
  {"status":"fulfilled","value":"OK"},  
  {"status":"rejected","reason":"Not OK"},  
  {"status":"fulfilled","value":"After not ok"}  
]
```


Assume the following file reading function:

```JS
const fs = require('fs');

const readFileAsyncAwait = async (filePath, encoding) => {
	await fs.readFile(filePath, encoding, (err, data)=>{
		if(err){
			console.log(err);
		}
		console.log(data);
	});
}

readFileAsyncAwait('input.txt', 'utf8');

```


Roughly how would this code look like if we use promises instead of async await instead of promises?

Answer:

```JS
const fs = require('fs');

const readFilePromise = (fileName, encoding) => {
	return new Promise((resolve, reject) => {
		fs.readFile(fileName, encoding, (err, data) => {
			if (err) {
				return reject(err);
			}
			resolve(data);
		});
	});
}

readFilePromise('./input.txt', 'utf8')
	.then(data => {
		console.log(data);
	})
	.catch(err => {
		console.log(err);
	});

```


***

# Event Propagation
https://www.aleksandrhovhannisyan.com/blog/interactive-guide-to-javascript-events/

assume the following HTML 

```HTML
<!DOCTYPE html>
<html>
  <head></head>
  <body>
    <button>Click me!</button>
  </body>
</html>
```

extrapolate and explain the output of the following JS code:

```JS
window.addEventListener('click', (e) => {
  console.log('window', e.eventPhase);
}, { capture: true });

window.addEventListener('click', (e) => {
  console.log('window', e.eventPhase);
});

// Body handler 1
document.body.addEventListener('click', (e) => {
  console.log('body', e.eventPhase);
  // 🛑 Stop propagating!
  e.stopImmediatePropagation();
}, { capture: true });

// Body handler 2: this will never run
document.body.addEventListener('click', (e) => {
  console.log('body', e.eventPhase);
}, { capture: true });

document.querySelector('button').addEventListener('click', (e) => {
  console.log('button', e.eventPhase);
});

```

***
# Optional Chaining
```JS

const car = {}
const carColor = car.name.color
console.log(carColor);
// error- "Uncaught TypeError: Cannot read property 'carColor' of undefined		

//In JavaScript, you can first check if an object exists, and then try to get one of its properties, like this:
const carColor = car && car.name && car.name.color;
console.log(carColor);
//undefined- no error


//Now this new optional chaining operator will let us be even more fancy:

const newCarColor = car?.name?.color;
console.log(newCarColor) 
//undefined- no error
					
//You can use this syntax today using @babel/plugin-proposal-optional-chaining

```

***
# Dynamic import



***

# Functional JS

Question: 

```JS

const myFruits = ['Apple','Orange',[4, 5],'Mango','Banana', [2, 3, ,[7,7, [8, 9, [1, 1]]]],'Apple','Apple','Mango']

var flattenedAndCleanedFruits = myFruits.flat(Infinity).filter((item)=> isNaN(item));

const countMyFruits = flattenedAndCleanedFruits.reduce((countFruits,fruit) => {
 countFruits[fruit] = ( countFruits[fruit] || 0 ) +1;
 return countFruits

},{} )

console.log(countMyFruits)
console.log(...new Set(flattenedAndCleanedFruits))
```


Explanation:

```JS
const myFruits = ['Apple','Orange','Mango','Banana','Apple','Apple','Mango']

//first option
const countMyFruits = myFruits.reduce((countFruits,fruit) => {
  countFruits[fruit] = ( countFruits[fruit] || 0 ) +1;
  return countFruits
 },{} )
 console.log(countMyFruits)
 // { Apple:3, Banana:1, Mango:2, Orange:1 }

```


```JS
const myArray = [2, 3, [4, 5],[7,7, [8, 9, [1, 1]]]];

myArray.flat() // [2, 3, 4, 5 ,7,7, [8, 9, [1, 1]]]

myArray.flat(1) // [2, 3, 4, 5 ,7,7, [8, 9, [1, 1]]]

myArray.flat(2) // [2, 3, 4, 5 ,7,7, 8, 9, [1, 1]]

//if you dont know the depth of the array you can use infinity
myArray.flat(infinity) // [2, 3, 4, 5 ,7,7, 8, 9, 1, 1];
```


```JS
//Mutating way
const muatatedArray = ['a','b','c','d','e'];
muatatedArray.splice(2,1)
console.log(muatatedArray) //['a','b','d','e']

//Non-mutating way
const nonMuatatedArray = ['a','b','c','d','e'];
const newArray = nonMuatatedArray.filter((item, index) => !( index === 2 ));
console.log(newArray) //['a','b','d','e']
```

```JS
const myArray = [1,2,3,4,5,6];

// Use .map() for applying a transformation on each elements

const mutipliedArray = myArray.map((element) => element*2);

console.info(mutipliedArray); // [ 2, 4, 6, 8, 10, 12 ]

// Use .reduce() for merging together each element of the array

const sumOfArray = myArray.reduce((previous, current) => previous+current);

console.info(sumOfArray); // 21

// These methods can be chained together

const sumOfMultipliedArray = myArray.map((el) => el*2).reduce((prev, cur) => prev+cur);

console.info(sumOfMultipliedArray); // 42

```

Remove duplicates without using FP or mutating the array:

```JS
// Get Rid of Duplicates
function removeDuplicates(array) {
    return [...new Set(array)];
}


```

***

# XSS
exaplin Escaping output VS Input Sanitization VS input Validation for XSS prevention.

```JS
function handleMessageSend(messageId, senderEmail, messageContent)  {

  database.save(messageId, senderEmail, messageContent);

}

  

function generateMessageHTML(messageId) {

  let messageContent = database.loadContent(messageId);

  return `<p class="messageContent">${messageContent}</p>`;

}
```

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


***

# Insecure Password Storage

Hashing algorithms
Salting
password entropy

```JS


import * as argon2 from "argon2";
import * as crypto from "crypto";
import * as zxcvbn from "zxcvbn"; 


const hashingConfig = { // based on OWASP cheat sheet recommendations (as of March, 2022)
    parallelism: 1,
    memoryCost: 64000, // 64 mb
    timeCost: 3 // number of itetations
}
 
async function hashPassword(password: string) {
    let salt = crypto.randomBytes(16);
    result = zxcvbn(password);
    if(zxcvbn < 4) 
       throw new Error({'Low Entropy':'Provided Password does not meet the minimum required entropy'});

    return await argon2.hash(password, {
        ...hashingConfig,
        salt,
    })
}
 
async function verifyPasswordWithHash(password: string, hash: string) {
    return await argon2.verify(hash, password, hashingConfig);
}
 
hashPassword("somePassword").then(async (hash) => {
    console.log("Hash + salt of the password:", hash)
    console.log("Password verification success:", await verifyPasswordWithHash("somePassword", hash));
});

```