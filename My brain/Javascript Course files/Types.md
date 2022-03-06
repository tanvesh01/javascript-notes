# Types
---
To get the `Type` of a variable or a value, you could do

```js
const age = 19;
const name = "Tanvesh"
----------------------------------------- console -----------------------
typeof name // returns "string"
typeof age // returns "number"
```

## String

```js
const name = 'Tanvesh'; // Single Quotes
const middle = "Sanjay"; // Double Quotes
const last = `Sarve`; // Back Ticks
```

When using Double or Single Quotes, mixing both of these can mess things up : 

```js
const mixing = "She is not \"cool\""
```

When using backticks it does'nt matter : 

```js
const backMixing = `She is sooo "cool"`
```

back ticks can also do **multiline**!

```js
const multiLine = `
	Hey
	this
	is
	wes
`
```

when you put a variable inside a string its called **Interpolation**

```js
const name = "Tanvesh"
const result = `=> ${name} is very very smart` // Interpolation
const concat = "=>" + name + "is very very smart"; // Concatation 
```

**Interpolation** can also be used to put variables inside html strings

```js
const name = "Tanvesh"
const someRandomHTML = `
	<div>
		<h1>${name}</h1>
	</div>
`
```
Will return
```html
<div>
	<h1>Tanvesh</h1>
</div>
```
---
## Number

Never try to use `Number` with a `string` ,weird things will happen
```js
1 + "1"
> "11"
```
Use `Math` in js to calculate things. Refer to mdn for `Math` [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math)

There is also `Infinity` and `-Infinity` too. Both of them are Number type

Then there is `NaN`

```js
10 / 'dog'
> NaN

typeof NaN
> "number"
```
---
## Objects
Everything is Js is **Objects**, will talk about this later too
Using Objects when no. things have to grouped

```js
const person = {
	// key : value
	first : "Tanvesh",
	last : "Sarve",
	age : 19
}

console.log(person.age) // 19
```
---
## Null and Undefined
Two ways to express **nothing** in Js.

`undefined` is returned when a variable is declared but **not set to a value**

`null` is a value of nothing. 

```js
let somethingUndefined; // will return undefined if not set to any value
const somethingNull = null; // have to set expicitly

console.log(somethingUndefined);
console.log(somethingNull);

> undefined
> null
```

Another example 

```js
const cher = {
	first : 'cher'
}

const teller = {
	first : 'Raymond',
	last : null
}

cher.last => undefined
teller.last => null
```
---
## Booleans

A variable which is either **true or false**

Booleans can be calculated with the help of `===`, `==`, `<` and `>`

**Diffrence b/w `===` and `==`**
`===` will check that the **values** and the **type** of both variables are same
`==` will only check for the **values**.

Almost **never** use `==`, is bad practice and can lead to errors later on