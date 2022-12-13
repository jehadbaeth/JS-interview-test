Explain the following code segemtn:

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


[Promises and Async Calls](./Promises_and_async)
