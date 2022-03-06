## Arrays
**Only IMP things here**

Array is also an object, it has Methods and holds some data and stuff, just like an object

##### Mutation methods

A **Mutation Method** is when the orignal data changes due to executing this method.

*just like mutant ninja turtles, they are turtles but Mutated*

```js
// Mutation
const num = [1, 2, 3];
num.reverse();
console.log(num)

> [3, 2, 1]
// Here the orignal array changed, so Mutation
```

##### Immutable methods
A **Immutable Method** is when the orignal data does not change due to executing this method.

When we want to take a part out of an existing array, we use `slice`

```js
const num = [1, 2, 3, 4];
const part = num.slice(2, 3)
console.log(part, num)

> [3, 4] [1, 2, 3, 4]
```

Here num does'nt change. part gets a part of the array from 2 to 3 index.

Where as `splice` will change the orignal Array.

---
If You want don't want to change the original array, and use and Mutation method : 

1. Make a copy of the original array
2. execute this method on this copy of array

```js
const num = [1, 2, 3];
const copyNum = [...num] // or even [...num].reverse()
copyNum.reverse()
```

---
If you want to push, instead of using the `push` method, you can :

```js
const num = [1, 2, 3];
const copyNum = [...num, 4] // adds at the back
// or 

const copyNum = [4, ...num]; // adds in front
```

---
To find the index to an element, :

```js
const num = [1, 2, 3];

const index = num.findIndex(num => {
	if(num === 3){
		return true
	}
	return false
	// returning true here means index variable get the index.
	// its kind of like a loop
})

console.log(index);
> 2

// or you can use this syntax

const index = num.findIndex(num => num === 3);
// does the same thing
```

----
You can spread a string inside an array

```js
[...'wes'];

> ['w', 'e', 's']
```

The **Static methods** of Array are on keyword `Array`.

The **Instance methods** are available on the arrays that we create.

[For Ref](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)

----

You can create **arrays from Objects** :

```js
const obj = {
	name: "tanvesh",
	age: 19,
}

Object.entries(obj)

 > [ ["name", "tanvesh"], ["age", 19] ] // key and value in individual arrays

Object.keys(obj) // An array of keys

> (2) ["name", "age"]

Object.values(obj) // An array of values

> (2) ["tanvesh", 19]
```

----

**Some cool callback methods** for Array

`find()` [find](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)

ℹ️ If you keep making functions that does the same thing, but for diffrent strings or values. **Try to create a higher order function, which returns a function**

```js
function findByWord(word) {
 	return function (singleFeedback) {
 			return singleFeedback.comment.includes(word);	
 	}
}
```

`filter()`[filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

`some()` and `every()`

---
### Looping Arrays

##### Map
Map returns an array of same length as it was called upon.
you can chain map functions.

If an array is not in the form you want, you can "massage" it with help of `map` to get the schema you want.

----
###### Filter 
Filter when called on an array, returns an array that may or may not be equal in length of the orignal one.

Inside the callback of filter : 

1. when returned true, we choose that element **to be** in new array
2. when returned false, we choose that element **to not be** in the new array

by new array, we mean the array returned by filter

###### Find

**Find returns a REF**, soo if you change something in this ref, the original array would also change.

same as Filter but returns an item, and if no item found, then returns `undefined`

###### Reduce

The `reduce()` method executes a **reducer** function (that you provide) on each element of the array, resulting in a single output value.

```js
const tallyNumbers = (tally, currentValue) => {
	// whatever you return here, will be stored in the accumalator, which is 
	// tally in this case.
	// currentValue is the value that loop gives of the array
	return tally + currentValue; 
}

const array = [1, 1, 1];

const oneItem = array.reduce(tallyNumbers, 0);
// 0 is the value at which the accumalator will start

console.log(oneItem)
> 3 // gives the value of the accumulator 
```
