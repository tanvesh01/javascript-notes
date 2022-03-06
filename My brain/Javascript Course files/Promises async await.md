## Promise 
We use Promise when we have to wait for some data to come by or just wait.

You can either `resolve` or `reject` a promise.

to get the values we use `.then` when the promise is resolved and `.catch` when it is rejected 

```js

const makePizza = () => {
	const pizza = new Promise(function(resolve, reject) {
		setTimeout(function(){
			resolve("Pizza!")
		}, 1000)
	})
	// immedieatly return the promise
	return pizza
}

const some = makePizza()

some.then(function(resultPizza){
	console.log(resultPizza)
})

```

You can also chain `.then` when you return a promise from the previous `then`

```js
some.then(function(resultPizza){
	console.log(resultPizza)
	return makePizza()

}).then(function(resultPizza){
	console.log(resultPizza)
	return makePizza()
	
}).then(function(resultPizza){
	console.log(resultPizza)	
})

// all of these will run one by one, after every second

```

### Promise.all
`Promise.all()` takes multiple promises in argument, `then` only returns the results when all the promises inside it are resolved.

```js
const dinnerPromise = Promise.all([pizzaPromise1,pizzaPromise2, pizzaPromise3]);

dinnerPromise.then(function([one, two, three]){
	// this will only run when pizzaPromise1, pizzaPromise2, pizzaPromise3 have 		   // been resolved
})

```

### Promise.race
same as Promise.all, but returns the result of the first promise that got resolved.

---
## Async and Await
instead of `.then` you can use a cleaner approach too. 

Adding the await keyword before a function that returns a promise, will wait for the promise to be resolved, When waiting the execution of the parent function will stopped until this promise is resolved.

```js
async function doSome(){
	await wait(); 
	console.log("asdasd")
}
// log will not run unless the timeout inside wait until the promise has been resolved
```

### Error handling with async and await

When you mark a function as `async` , that function automatically returns a promise.
So, you could use `.then and .catch` on async functions after calling them

```js
async function doSome(){
	await wait(); 
	console.log("asdasd")
}

doSome().then(res => {

}).catch(err => {

}) 
```