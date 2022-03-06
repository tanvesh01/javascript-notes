## Objects
Dont use objects when you care about the order of properties, js compilers are diffrent, you never know.
 
```js
const person = new Object({
	name : "Tanvesh",
	age : 19
})
// or
const person = {
	name : "Tanvesh",
	age : 19,
	"cool-dude" : true, // names with spaces can be used like these too
	"reallty cool" : false.
	"11111" : true
} // literal syntax

person['cool-dude'] // access cool-dude 
```
when the property name and variable name you are setting it to are same, then you can

```js
const age = 19

const person = {
	name : "Tanvesh",
	age, // i.e age : age
}

// To add a new property to person

person.job = "web";

console.log(person)

> {
	name : "Tanvesh",
	age : 19,
	job : "web"
}
```

But `person` is a const but we care changing it! Its because we are not overwrting the binding to `person`, we are just changing values inside it.

If we try to set `person` to a new object then, js will throw an error.

You can also `freeze` an object, after that you won't be able to add, change or remove properties of that object.

```js
const personFreezed = Object.freeze(person);
personFreezed.age = 21;

console.log(personFreezed)

> {
	name : "Tanvesh",
	age : 19,
	job : "web"
}

```

**Deleting a property from an object**
```js
delete person.age;
```

---
### Methods 
Function inside an object is a Method. 
```js
const person = {
	name : "Tanvesh",
	sayHello : function(){
		return this.name;
	}
	// or
	sayHello(){
		return this.name;
	}, // method shorthand
	// or 
	sayHello : () => {
		return "hey"; // here `this` is not available
	}
}

// Here this refers to the object person
```
when we access `sayHello` we do, `person.sayHello`, so anything that is left of that `.` is referred by `this`.

---
## Object Reference vs. value
```js
const p1 = {
	name: "wes"
}
const p2 = {
	name: "wes"
}

p1 === p2
> false // what?! they are the exact same!
```
Its false because, comparing two objects is done by refrence to the object itself and not by their value. 

---
#### Making copies of Object and Arrays
```js
const p3 = p1;
p3.name = "lazy"

console.log(p3.name)
console.log(p1.name)

>"lazy"
>"lazy"
```

Above even though only p3 was changed, p1 changed its name property too!

Its because 
```js
const p3 = p1;

Here we are just copying the refrence of p1 into p3. So any change on p3 will also reflect on p1. We are not making a NEW object "p3".
```
---
#### making copies the right way
You can use the spread operator to make a new object and then copy the values into that object.

```js
const p3 = {...p1};
p3.name = "lazy"

console.log(p3.name)
console.log(p1.name)

>"lazy"
>"wes"
```

**But** the spread operator does "shallow copy". So if there's an object inside p1's property, that object will still be copied by refrence, into p3. Same problems will happen this object.

We can do something like "deep clone" to copy all of the objects by value and not by reference.

You can use `Lodash` for this.

---
#### Merging Objects

```js
const p1 = {
	name: "wes"
}
const p2 = {
	last: "bos"
}

const p3 = {...p1, ...p2}; // Spreading both seprated by comma.
console.log(p3)

> { name : "wes", last : "bos"}
```

The order of objects (here `p1` and `p2`) when spreading, matters. p2 will overwrite any property that has the same name in p1 as in p2.

---
#### Passing Objects into functions

```js
const p1 = {
	name: "wes"
}

const do = (data) => {
	data.name = "Tanvesh"
	console.log(data)
}

do(p1);
console.log(p1)

> {name :"Tanvesh"}
> {name : "Tanvesh"} // p1's value also changed.
```

Here we are passing the object as a refrence, that's why `p1`'s value changed too!

#### Looping through key of objects
use For in loop for this
```js
const obj = {
	name : "Tanvehs",
	age : 19,
	gender : "m"
}

for(const prop in obj){
	console.log(props)
}

> name
> age
> gender
```