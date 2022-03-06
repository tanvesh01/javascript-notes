# Functions

---
Function is a block of code, That can be called again and again.
Data given to a function is called an **argument**

```js
Math.floor(argument);
```
---
## Built-in Functions
These Functions comes with Javascript
```js
> parseFloat("20.12121");
20.12121 // Takes a string and returns a Float

> parseInt("20.1");
20 // Takes a String and returns a Int
```
---
## Parameters and Arguments
If we don't give Arguments to a Function, Then js has to reach out of the function body to get the data

Arguments of a function can be a **value, expression, variable or functions (these functions have to return a value tho) too**

![function-definition.jpg](https://github.com/wesbos/beginner-javascript/blob/master/function-definition.jpg?raw=true)

A function first check for a variable inside its body or scope, then reaches out of the body to find it.
```js
function sayHi(firstName) {
	return `Hello ${firstName}`
}

sayHi();
> "Hello undefined"

// because inside sayHi firstName has been declared but has no value yet
```

You can also give arguments a default value, so that when not passed explicitly those arguments will fallback to default values

```js
function sayHi(firstName = "Tanvesh") {
	return `Hello ${firstName}`
}

sayHi();
> "Hello Tanvesh"
```

There can be situations where

```js
function sayHi(first, middle = "sun", last = "sarve"){
	return `Hello ${first} ${middle} ${last}`
}

What if we want to use the default value of middle but want to give a diffrent value to last?

sayHi("Tanvesh", undefined, "sharma");
> "Hello Tanvesh sun sharma"

when middle is undefined the only it will fallback to its default value
```
---
## Different Ways to Declare Functions

```js
Normal Function
function sayHiTo(firstName){
	return `Hi ${firstName}`
}
-------------------------------------------------------------------------------
Anonymous Function (Not valid Javascript when used like this tho )
You don't pass the name of the function here
function (firstName){
	return `Hi ${firstName}`
}
-------------------------------------------------------------------------------
You can store a Function into a variable, then call it by the variable's name
const WhatsUp = function (firstName){
	return `Hi ${firstName}`
}

WhatsUp("Tanvesh");  // "Hi Tanvesh"
-------------------------------------------------------------------------------
Instead of writing function keyword everytime like :point_up_2: above
You could use an arrow function

const WhatsUp = (firstName) => {
	return  `Hi ${firstName}`;
}
-------------------------------------------------------------------------------
When there is a return keyword used, it's called "explicit return"
We can skip writing that too

const WhatsUp = (firstName) => `Hi ${firstName}`;

implicit return, because arrow functions are all about being concise

function add(a, b = 3){
	const total = a + b;
	return total;
}
		to :point_down:

const add = (a, b = 3) => a + b;
```

Functions Declared with the `Function` keywords are **hoisted**. So browser puts these at the top of js files.
And That's why you can all the functions before their defination inside code.

While function stored in a variable, can't be called before their defination, because they are **not hoisted**

#### Returning Objects

```js
const makePerson = (first, last) => {
	return {name : `${first} ${last}`, age : 24}
}

You can make this an implicit return too, with the help of "()"

const makePerson = (first, last) => ({name : `${first} ${last}`, age : 24})

```

#### Running Anonymous functions
Wrapping Anon Functions with "()" runs it, because () runs first in js and the Anon Function will return a Function value.

```js
(function(age){				// this returns a
	return `You are cool! ${age}`	// Function value
})(10) // runs this function 

> "You are cool 10"
```

#### Methods
A JavaScript **method** is a property containing a **function definition**.

```js
const object = {
	// Normal Method
	sayHi : function(){
		console.log("say Hi!")
		// you can use `this` here
	},
	// Arrow method
	whisperHi : () => {
		console.log("say Hi!")
	},
	// New Way of defining a Method
	yellHi(){
		console.log("HEY BROOO!")
	}
};

object.sayHi();
object.yellHi();
```

#### Callback Function
```js
You can pass Anon Functions as callback or Arrow Functions
setTimeout(function(){
	console.log("say hi after 1 second");
} , 1000)
```

#### Pure Functions
Functions that return same value for the some arguments everytime, then its a pure function. These Functions are easier to test as the return predictable values

```js
const add(x, y) => x + y;
```

Functions that returns a `Date` or random numbers are not pure as we never what are they going to return.

So for testing we have to make them pure

```js
// non-pure functions, return non-predictable values
const getRandom = (max, min) => {
	return Math.floor(Math.random() * (max - min) + min);
}

// pure function, as we can pass randomeNumber to get same values everytime
const getRandom = (max, min, randomNumber = Math.random()) => {
	return Math.floor(randomNumber * (max - min) + min);
}
```