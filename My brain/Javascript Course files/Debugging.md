# Debugging Tools
---
## Console Methods
- When you have an array of objects, try doing `console.table(Array)`.
- When you want to count no. of times a Function has run, use `console.count(String)` 
- You can group multiple `console.log`s	into one, by using `console.group()`
```js
const doSomething = () => {
	console.group("Group") // These String have to be same
	console.log("some-1")
	console.log("some-2")
	console.log("some-3")
	console.groupEnd("Group") //  These String have to be same
}
```
---
### CallStack
In a Stacktrace, `at <anonymous>:1:1` means that its an anon Function

### Grabbing Elements
Selecting an element and typing `$0` will return you the element in the console.

### Breakpoints
Pause js from running
```js
const doSomething = () => {
	debugger; // <- Breakpoint
	console.log("some-1")
	console.log("some-2")
	console.log("some-3")
}
```

### Break on Attribute
Whenever an attribute of an element is changed, it adds a breakpoint and stops the execution