## Modules
Idea of sharing code between files is Modules. Each file is a module in itself.

1. Export some code from the file in which you want to use
2. Then import that code in the file you want to use that

A variable defined inside a module is only available inside it, i.e. only available to functions inside this module

```js
// NAMED exports
const last = "some"
export const returnHi = () =>{
	return `hi`
} 

// do this at last of the file
export {last}
```
```js
// NAMED import
import {last, returnHi} from "./file.js"
```


**When Exported default** it will be the default thing that will gets imported when not using named import
```js
const person = {
	first: "Tanvesh",
	last: "Sarve"
}

export default person
```

```js
import someRandomPerson from "./file.js"
// it does'nt matter what you call this import. 

import someRandomPerson, {last, returnHi} from "./file.js"
// someRandomPerson will import `person` object.
```

You can't export default a variable when declaring it.
```js
export default const some = "sds"
```
❌  you can't do that

to export default `some` you have to go to the bottom of the file

```js
const currencyModule = await import("./file.js");
// we can import module anytime we want, after the page load.
// or even this 
const {local} = await import("./file.js");

```