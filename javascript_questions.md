<h3>JavaScript Security</h3>

1. What is Prototype Pollution?
Prototype pollution is a JavaScript vulnerability that enables an attacker to add arbitrary properties to global object prototypes, which may then be inherited by user-defined objects.

2. What is ‘npm audit’?
The audit command submits a description of the dependencies configured in your project to your default registry and asks for a report of known vulnerabilities.
 
3. Name 3 types of XSS attacks.
Stored, Reflected, and DOM-Based XSS

4. What is Input sanitization?
 Input sanitization is a cybersecurity measure of checking, cleaning, and filtering data inputs from users, APIs, and web services of any unwanted characters and strings to prevent the injection of harmful codes into the system.

<h3>Javascript</h3>

1. What is Object.prototype?
https://portswigger.net/web-security/prototype-pollution/javascript-prototypes-and-inheritance#the-prototype-chain

2. What is a closure in JS?
 A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function's scope from an inner function.
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures


3. Shallow copy vs Deep copy
 A shallow copy constructs a new compound object and then (to the extent possible) inserts references into it to the objects found in the original. A deep copy constructs a new compound object and then, recursively, inserts copies into it of the objects found in the original.

4. What is typescript?
 It enables developers to add type safety to their JS projects. Moreover, TypeScript provides various other features, like interfaces, type aliases, abstract classes, function overloading, tuple, generics, etc

5. Local storage?

6. Window object vs Document object.
 The document object is a property of the window object. The window object represents the browser window. The document object represents the HTML document loaded in that window. The window object has many useful properties like the location object and the setTimeout function.

7. What is the result of executing the following code

	<code>
            const myUser = {
                    name: 'John'
                }

            const mySecondUser = {
                    name: 'John'
                }

            console.log(mySecondUser === myUser)
    </code>

Solution: false.

8. .map vs .filter vs .reduce vs .foreach

filter and foreach: The main difference between forEach and filter is that forEach just loop over the array and executes the callback but filter executes the callback and checks its return value. 

map: almost the same as foreach. The difference is that .map returns a new array and foreach does not.

reduce: Used to reduce the array to one single value.

9. What is EcmaScript (ES6) ?
10. What is eval() function in JS?
11. What is the Event Loop in JS?
12. What is a Promise in JS?
13. == vs ===
  The main difference between the == and === operator in javascript is that the == operator does the type conversion of the operands before comparison, whereas the === operator compares the values as well as the data types of the operands

14. How to print name property value in the console?
<code>
const myCar = {
		name: 'BMW'
	}
</code>
Solution: 
<code>
console.log(myCar[“name”])
console.log(myCar.name)
</code>

15. What is Webpack?
16. What is npm?
npm is the package manager for the Node JavaScript platform
