## Event Listener
```js
const button = document.querySelector(".button")
// getting the button

button.addEventListener('click', function(){
	 console.log("clicked")
})
// an anon Function will run onClick of the button

function handleClick(){
	console.log("clicked");
}

button.addEventListener('click', handleClick);
// or just pass the function
// just dont call the functionm inside this, unless it returns another function.
```
You can pass a third argument to `addEventListener`, an object of **options**
If you pass `{once : true}`, then that Listener can only be added once on that element, even if you call `addEventListener` again and again

---
**Removing** Event listener
These areguments have to be EXACTLY SAME, for this to work!
```js
button.removeEventListener('click', handleClick);
// These areguments have to be EXACTLY SAME, for this to work!
```

You can't remove an event listener, when using an anon function, because you can't reference it again. 

So if you want to remove an event handler afterwards, use an arrow function stored in a variable or a name Function.

---
#### Adding Event Listener to multiple elements

```js
const manyButtons = document.querySelectorAll(".many")
// This will return an NodeList
```
Just loop over this is NodeList with the help of `forEach`
```js
manyButtons.forEach(function(btnByJs){  // we get the buttons in argument by js
	btnByJs.addEventListener("click", handleClick) 
	// these are the same buttons which were inside that NodeList
})
```
---
## EventTarget
If there are bunch of buttons, then how do we know that what button was clicked?
Event object will help us
```js
function handleClick(event){ // argument by js
	console.log(event.target); // returns the element we are clicking on
}
manyButtons.forEach(function(btnByJs){  // we get the buttons in argument by js
	btnByJs.addEventListener("click", handleClick) 
	// these are the same buttons which were inside that NodeList
})
```

Diffrence b/w **`currentTarget` and `target`**

Basically, [events bubble](http://www.javascripter.net/faq/eventbubbling.htm) by default so the difference between the two is:

-   `target` is the element that triggered the event (e.g., the user clicked on)
-   `currentTarget` is the element that the event listener is attached to.

See a simple explanation on this [blog post](http://www.qc4blog.com/?p=650).

---
#### Bubbling up / Event Propagation
If there is a click listener on the window and a button inside it. When you click on the button

1. First, callback of click listener on the **button** will fire.
2. then, callback of click listener on the **window** will fire.

This is because of bubbling, as the event bubbles **up** the hirearchy in the DOM.

You can stop this propagation, by using `event.stopPropagation()`. This will stop the propagation as soon as its called.

---
#### Event Delegation
```html
<ul>
	<li>hi</li>
	<li>hi</li>
	<li>hi</li>
	<li>hi</li>
	<li>hi</li>
</ul>
```
In this list of `li`s  ,if we want to listen for clicks on each of them, then we can just select them all and with `forEach` add event listeners to all of them.

**BUT WHAT IF** we keep adding more `li`s to this list, then we would have to run that forEach loop again and again. or lets say these list comes from the server, so we dont how big its going to be

this where **event delegation** comes in.

You just listen for a click on the `<ul />`, then with help `event.target` you decide wheather it was a `<li />` that was clicked. then recognize that `<li />` and do whatever you want.

```js
const ul = document.querySelector("ul")

ul.addEventListener("click", function(event){
	if(event.target.matches('li')){ // check if the thing that's clicked is an li
		// do your thang!
	}
})
```


#### Propagating Down
 
 If you want to propagate down, you can pass `{capture : true}` as third argument in `addEventListener`.  Then it will propagate down. Same as bubble up but in opposite order.
 
 1. First, callback of click listener on the **window** will fire.
2. then, callback of click listener on the **button** will fire.
 
---
### This Keyword in Events

```js
button.addEventListener("click", function(e){
	console.log(this) 
	// =====
	this Keyword will return, whatever it is at the left on addEventListener, 
	in this case, will return button element. 
})
```

---
## Prevent Default
Some HTML elements have default behaviours when you interact with them. You can "Prevent" this behaviours from happening by adding a Listener on that element and calling the `preventDefault()` method given to us by `event`.
```html
<a href="/home" class="link" >Go to home</a>
```

```js
const link = document.querySelector(".link");
link.addEventListener("click", function(event){
	event.preventDefault(); // stops the default behaviour
})
```
----
## Accesibilty
1. `<a>` use it when User needs travel to another page
2. `<button>` use it when user will stay in the same page
3. If there is any other tag which needs to act like a button, give it a `role="button"`, so that it can be accessed from keyboards too. Now you have add a listener for this element too, to listen **some key** from the keyboard 

---

To reset a form use
```js
e.target.reset()
```

### Extras
[Intersection Observer](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)


![Graphical representation of an event dispatched in a DOM tree using the DOM event flow](https://www.w3.org/TR/uievents/images/eventflow.svg)


