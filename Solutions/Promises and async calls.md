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
```
[  
  {"status":"fulfilled","value":"OK"},  
  {"status":"rejected","reason":"Not OK"},  
  {"status":"fulfilled","value":"After not ok"}  
]
```


```
error: Not OK
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

