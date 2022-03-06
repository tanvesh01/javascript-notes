## IF blocks
```js
if(condition){
	if condition is true, then this runs
}
```

Instead of having `if else` blocks :

```js
function some(x){
	if (x){
		return y // When function returns, it stops the execution of that function here only, so no need of a else if block
	}
	return z // If x is false, this will run automatically
}
```

You can also execute a function instead of condition.

```js
function getSome(){
	return true;
}

if(getSome()){
	console.log("It was true!")
}
```

Almost never use `==` double equals, it can lead to bugs.

**Where `===` comes in handy**
When we want to check if a varaible is either `null` or `undefined`.

```js
x = null;

x == undefined // does not check the type
> true

x === undefined // checks the type
> false
```

## Truthy and Falsey values
- empty array
- empty object

**Truthy values**
- 1
- -10
- full string
- a string of "0"

**Falsey Values**
1. 0
2. undefined variable
3. Variable set to null
4. a variable set to `"hello" - 10` NaN
5. empty string

In if blocks, you can use values of diffrent types instead of booleans, in place of condition. Any varaible like a string can be used as a condition and js will try coerse it into `truthy` or `falsey`

```js
const normalString = "tanvesh";
const emptyString = "";

if(emptyString){
	return "This will not run"
	
}

if(normalString){
	return "This will run!"
}

>"This will run!"
```

Because An empty string always converts into `falsey` and non-empty to `truthy` 

`[].length` when 0, is falsey. (*Array of length 0*)
`[2, 4].length` when 2, is true. (*Array of length 2*)

**Checking if an object is empty**

```js
const ob = {};

Object.key(ob);
> []

Object.key(ob).length;
> 0 // which is falsey, so object is empty
```

## Ternary Statements
A short hand of If block basically
```js
const word = count === 1 ? 'item' : "everything";
//           condition  ?  when true : when false;
```

**AND AND Trick!**

```js
function check1(){
	console.log("1");
	return true;
}
function check2(){
	console.log("2");
	return true;
}
function check3(){
	console.log("3");
	return true;
}
// Here js will go from left to right, executing these functions
if(check1() && check2() && check3()){
	console.log("all passed!")
}
```

If any of these functions returns false, the condition will become false, and it will not execute the next functions inside the condition.

```js
function check1(){
	console.log("1");
	return true;
}
function check2(){
	console.log("2");
	return false;
}
function check3(){
	console.log("3");
	return true;
}
// Here js will go from left to right, executing these functions
if(check1() && check2() && check3()){
	console.log("all passed!")
}else{
	console.log("something failed")
}

> "1"
> "2"
> "something failed"

// Here 3 did not print, because check2() returned false, so js had no need to check other functions ahead
```

##### Abusing this for Ternary statements
```js
const isAdmin = true;

// js goes from left to right, if current one is true they only will execute the next one.
// =================>
isAdmin && showAdminBar();
```

js checks, if `isAdmin` is true then moves to the next condition, which is a function is this case `showAdminBar()`, so executes this.

This is super cool for writing short hand conditions. 

In react you could do
```jsx
{isAdmin && <AdminBar />}
// if isAdmin is true, then <AdminBar /> is rendered
```

```js
const ob = {}

ob.num = ob.num + 2 || "y";
// ob.num + y will result into NaN, because ob.num is undifined. 
NaN means falsy, then js will go on "y", becuase there's an OR there.
```

## Intervals and Timers
`setInterval` is used to run a piece of code every fixed interval, like every 3secs

`setTimeout` is used to run a piece of code after a fixed interval, like after 3secs. 
code runs only once in this case.

Both of these functions are globally scoped and available everywhere

**Asynchronous nature of js**
```js
function buzz(){
	console.log("buz")
}

console.log("start");
setTimeout(buzz, 500); // Js comes back to execute this after 500ms
console.log("end")

>"start"
>"end"
>"buz"
```
js executes everything but waits for `setTimeout` to finish up, and THEN executes its callback

```js
setInterval(buzz, 2000);
// will excute buzz every 2 seconds
```

#### How to stop the Timer ?!

To stop `setTimeout` or `setInterval`, you have to save a referance to them first.
```js
const timer = setTimeout(buzz, 1000);
// will run after once second
// To delete this :

clearTimeout(timer);

const interval = setInterval(buzz, 3000);
// will run every 3 seconds
// To delete this :

clearInterval(timer);
```

`clearInterval` is also globally scoped and available everywhere.