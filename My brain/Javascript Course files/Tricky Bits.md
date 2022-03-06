Stuff from Namaste javascripts is here 
[[Variables and Statements]]
## How Execution context works
-----
```js
var x = 1;
a();
b();
console.log(x)

function a(){
	var x = 10;
	console.log(x)
}

function b(){
	var x = 100;
	console.log(x)
}
```

>EC = Execution Context  GEC = Global Execution Context

Functions created with `function` keyword are stored first in Global Execution context's memory with its defination. 

Variables with `var` keyword are also stored first in Global Execution context's memory but without any value, so without any code being executed yet `x` 's value here would be `undefined` because its declared with no value.

when the first line runs x's value is set to 1.

When the `a` function runs, js makes a whole new execution context for just `a` which is independent of GEC. In this EC, again `x` is created in memory with undefined value and is set to 10 afterwards. `console.log` checks for x in its own EC first, and finds x's value to 10 and prints 10. 
Then this EC is popped out of call stack and the variables inside it are also destroyed, so you can't acess them outside

Same thing happens with `b`.

After the whole code is executed, even the G6EC is removed from the call stack.

```js
var x = "something";
function name() {
	console.log(x);	
	var x = "tanvesh";
}
name();
```
When name func is executed, Within its EC, x is created with undefined value. so this will print undefined. But no x was defined inside this name function, then "something" would have been printed

Image from Namaste Javascript Video
![[Pasted image 20220212132704.png]]

#### `this` keyword
Whenever a js program is run, a Global object is created and an GEC is created.
In the case of browsers this Global Object is the window object. 

In the Global space, `this` points to Global Object.
**Global Space** is whatever that is *not* inside a function


# Scope
----
**Lexical Enviroment** is the local memory of function + the lexical enviroment of its parent.
So when inside function a variable is used but is not found in its local memory then js moves on to find it in the lexical enviroment of its parent. if found then it'll use that value or move on to lexical Env of the parent. *again*

This keeps happeing until the variable is found or it reaches the Global context.
This is like a chain known as **Scope Chain**

## Hoisting `let`  and  `const`

`let` and `const` variables are actually hoisted, because they are stored in memory just like  `var` variables are given `undefined`. But we still can't access until we have given it a value.

```js
console.log(a); // This will give an error
let a = 10;
var b = 100;
```
This will give an RefrenceError

until these `let` and `const` variables are given any value these variables cant be accessed, this time of getting into to actually be accessible is known as Temporal Deadzone

```js
var a = 100;
{
	var a = 10; // or even, a = 10
	let b = 20;
	let c = 30;
}
console.log(a); // 10
console.log(b); // error
console.log(c); // error
```
In the block scope we can also change the values of `var` variables defined in the global scope, this is known as shadowing.

When js sees a block with let and const variables, it assigns a diffrent space for these variables, so they can only be accessed inside the block  
Thats why let and const are called **block scoped**

When `var` is defined and initialized inside a block 


## Closures
---
Functions bundled up with its lexical enviroment is known as closures. 

so if we return a Function from a Function, then the function being returned will have its memory space + the lexical enviroment of its parent Function
```js
function x(){
	var a = 7;
	function z(){
		console.log(a)
	}
	a = 1000;
	return z;
}

var y = x();
y()
``` 
Here when `y` runs i.e `z` will still have the lexical env of `x`
so it will print `1000` as `a` was updated in x's Execution Context
```js
for(var i = 1; i<= 5; i++){
	setTimeout(function(){
		console.log(i)
	}, i * 1000)
}
```
This prints 6, 5 times. this happens because of closures.
The function inside setTimeout will have `i` in its lexical env. But it has the refrence to i, so when becuase of `for` loop i's value change to 6, after executing all setTimeouts.
and as the callback function will run after sometime, it will get value of 6.
```js
for(var i = 1; i<= 5; i++){
	function close(x){
		setTimeout(function(){
				console.log(x)
			}, x * 1000)
		}
	}
	close(i)
}

```
now timeout will get the latest value


## Prototype

Every object in JavaScript has a built-in property, which is called its **prototype**. The prototype is itself an object, so the prototype will have its own prototype, making what's called a **prototype chain**. The chain ends when we reach a prototype that has `null` for its own prototype.


## Wes bos stuff (`not that good tbh`)
---
----
Global variables are available everywhere.
`var` variables are attached to `window`, so you can access them from window

Anything in the global scope are attached to `window` object, except `const` and `let` variables
```js
function sayHi(){
	console.log("Hi")
}

window.sayHi()  
> "Hi"
```

Any variable defined inside a function, are only available inside that function. But you can access the global variables inside a function.

```js
if(1===1){
	var x = "Tanvesh"
}

if(1===1){
	const y = "sarve"
}

console.log(x);
> "Tanvesh"

console.log(y);
> error
```

A variable created inside a block, will **not** be accessible outside it. Always try to use `const` or `let` because they are block scoped and can only be accessed inside it.

The **`var` statement** declares a function-scoped or globally-scoped variable, optionally initializing it to a value.

## Lexical Scoping

Js does not care, where the function is run, but it cares where it is defined. Looking up a variable in Function (when not defined in its scope) happens from the place of its defination.

```js
const dog = "Snickers";

function logDog(){
	console.log(dog) 
	
	This still looks up in global scope, rather than the scope where it is run;
	If there was a argument here, then it would have been locally scoped;
}

function go(){
	const dog = "bunny";
	logDog();
}

go()

> "Snickers" 
```
----
## Hoisting

Functions defined with a `function` keyword can be called before they are even defined. Because Js, moves them up for you in the file. 

```js
sayHi(); // Both the functions called before their defination

function sayHi(){
	console.log('hey!');
	console.log(add(1, 2))
}

function add(x, y){
	return x + y;
}

> "hey!"
> 3
```
Any other type of function will not be hosted up. 
```js
const age = function(){
	This will not be hoisted, same for arrow functions too;
} 
```
`var` variables are hoisted up in a different way. Only their defination is hoisted up but not the setting of that variable. So accessing this variable before it defination will return `undefined`

```js
console.log(age)
var age = 10;

> undefined
```
---
## Closures
Pretty GOOD docs [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
```js
function outer() {
	 const outerVar = "Outer var";
	 function inner() {
		 const innerVar = "Inner var";
		 console.log(outerVar);
		 console.log(innerVar);
 	 }
	 return inner;
 }

const innerFunction = outer(); 

Even though the outer Function has already run here but javascript will keep the outerVar in memory so that it is still available to the inner()

> "Outer var"
> "Inner var"
```
Another GREAT example

```js
function createGame(gameName){
	const score = 0;
	return function win(){
		score++;
		return `${gameName} score : ${score}`
	}
}

const football = createGame("Football");
const cricket = createGame("Cricket"); 
// Everytime this will run, a new score variable will be created

football();
football();

cricket();
cricket();

> "Football score : 1" 
> "Football score : 2"

> "Cricket score : 1"
> "Cricket score : 2"

Here because of closure, the score variable is stored and increased.

```

### Debouncing
When you want to introduce a delay between the firing of a function
```js
function debounce(fn, delay) {
	let timer;	
	return function() => {
		clearTimeout(timer)	
		timer = setTimeout(() => {
				fn.apply(this, arguments)
		}, delay)
	}
}
```
