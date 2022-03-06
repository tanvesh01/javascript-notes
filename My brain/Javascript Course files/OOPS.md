## OOPS

#### `new` Keyword
The new keyword creates an instance of something

```js
const date = new Date()

// Here date is an instance of 'Date' 
```

Whenever we use the `new` keyword and call a function after that,  that function is called a constructor function. 

#### `this` Keyword
`this` keyword gives whatever it is bound too.

When used inside a function that is inside an object, then `this` returns the object itself.

When used inside a normal function, that is outside any object, then `this` returns the global scope

Whenever use the keyword `new`, js creates an empty object `{}` and assigns the `this` keyword to this empty object inside the constructor function.

`this` returns the global scope inside a arrow function.

```html
<button class="btn" > click me </button>
```
```js
const buttons = document.querySelector(".btn")

function onClick(){
	console.log(this);
}

buttons.addEventListener("click", onClick)
// this, returns whatever addEventListener is attached to

> <button>

```

**In an arrow Function**

`this` won't work as expected. If this arrow function is not inside a normal function, which is attached to something, then `this` will return the `Window` Object.


```js
function pizza(){
	console.log(this);
}
// here this will return the instance of the function it is inside
> pizza {}
```

this function can also store some data, with the help of **Constructor**, we can pass this data when creating a `new` instance of this function.

so, `this` keyword is used to store info about the object we are creating with the `new` keyword

```js
function Pizza(name, price, id){
	console.log(this);
	// saves the values that are passed in, to this instance of pizza
	this.name = name;
	this.price = price;
	this.id = id;
}

// 
const newPizza = new Pizza("tomato", "149", "2")
console.log(newPizza.name)

> Object {} // this
> tomato
```

Whenever a `new` keyword is used in front of a Function, js creates an empty object and assigns `this` inside the function to this empty object.
