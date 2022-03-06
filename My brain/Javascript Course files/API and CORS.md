## AJAX
Async Javascript and XML

We make request to an endpoint to get back data. 
use `fetch` method to make an request. `fetch` returns a promise as its async.

we can catch an error too

```js
const fetchPromise = fetch("some/url")

fetchPromise.then(res => {
	// We want the response in the form if JSON
	// so we convert res into json, which also returns a promise
	return res.json()
}).then(data => {
	// as the previous .then returned a promise, we can again use .then
	console.log(data)
}).catch(err => {

})

// using async await

const fetchUser = async () => {
	const res = await fetch("some/url");
	const data = await res.json();
	console.log(data)
}

fetchUser().catch(err => {
	// do something with error
})

```

## CORS
CO : Cross origin 
R    : Resource 
S    : Sharing

When there are two domains, and we want to share data between them, if not handled the browser will block this an give us CORS error.

```js
bank.com

 we dont want to share data between them, as someone can execute js from tanvesh.com and get login credentials from bank.com

tanvesh.com
```

##### How to fix this ?
- Run your js files through a server like parcel
- When a server like Node or ruby, calls these apis, the CORS error will not happen. Its is totally allowed. 

So instead of calling the api directly from the frontend in js, we can have **PROXY** server in between our frontend and the api

localhost frontend will send data to => PROXY will make the api request to avoid cors, the send it back to our frontend.