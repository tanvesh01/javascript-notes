## Selecting Elements
`<script>` tags which contains your js code, have to come after all the html, or js won't know what elements are you trying to select

**You can call `querySelector` on any element** not just document. It will always try to find out elements inside the element it is attached too.

```js
const p = document.querySelector('p');
// querySelector will only select 1 element that comes first.

const div = document.querySelectorAll('div');
// querySelectorAll will select all the elements in that page 

const parent = p.closest('div');
// Closest always look up from the element, unlike querySelectors which looks for elements deep down in the DOM. closest will return the closest div of p. So if div is the parent of p, then this div will be returned. 
```

You can convert a NodeList to an array by :
```js
Array.from(any_node_list);
```

---
## Element Properties and Methods
btw `console.dir()` will give you all the properties on that element.

```js
const h2 = document.querySelector("h2");

console.log(h2.textContent);
// This is a getter

h2.textContent = "Hey js is coool"
// this is a setter
```
Diffrence b/w `textContent` and `innerText` is [here](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent#differences_from_innertext)

**Attaching text to the end or start** of the element, [insertAdjacentText](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentText)

```js
const h2 = document.querySelector("h2");

h2.insertAdjacentText('afterbegin', "add this text")
// insertAdjacentText does not cause performance issues, because it does not re render the // whole list

```
`insertAdjacentElement`: Inserts an Element.
`insertAdjacentHTML` : Inserts HTML in the form of string with back ticks 
are available too.


---
## Working with classes
with `classList` property on a element we can add, remove or toggle classes from/on that element
```js
const pic = document.querySelector(".nice");

pic.classList.add(".cool");
pic.classList.remove(".nice");

pic.classList.toggle(".round")
pic.classList.remove(".round")
// toggle removes the class if its already there or adds it if its not there.
```
---
## Built in and custom data Attributes
```js
const pic = document.querySelector(".nice");

pic.alt = "this is a pic"
console.log(pic.alt) // "this is a pic" 

// we can use this too
pic.setAttribute('alt', "just a pic")
console.log(pic.getAttribute('alt')) // "just a pic"

most of these properties are getter and setters
```

You can have custom attributes too

```html
<p data-name="Tan" aria-selected="nope" class="custom" >Hey!</p>
```
```js
const pTag = document.querySelector(".custom")
console.log(pTag.datasets.name)

// any aria attribute in html, can be accessed in js with camelCase
// but you have to use setAttribute to set its value
console.log(pTag.ariaSelected)
> "nope"
```

you can also control css variables from js

```css
.turtle{
	--x : 0; /** x variable **/
	--y : 0;
}
```
```js
element.setAttribute("style", `--x : ${someVariable}`);
```
---
## Creating HTML Elements

You can create HTML elements with Javascript too, with the help of `createElement`.

```js
const myPTag = document.createElement('p');
console.log(mtPTag) // <p></p>

myPTag.classList.add("paragraph");
console.log(mtPTag) // <p class="paragraph" ></p>
```

`appendChild` can be called against every `Node`. 
`appendChild` method adds a node to the end of the list of children of a specified parent node.

```js
document.body.appendChild(myPTag);
```
```html
<body>
	<!-- adds the ptag into body -->
	<p class="paragraph"></p>
</body>
```

	But `appendChild` causes a reflow everytime you call it, and if you do that a lot, there can be perfomance issues. You could create all the elements first and **then** append it to body, so there will only one repaint as only one time, an element has been inserted into the DOM. with the help of document fragment

If we create an element and want to append it in lot of places, we **can't** do that. We have to create a new element everytime we want to append or js will just move position of the same element

```js
const ulTag = document.createElement("ul");
const liTag = document.createElement("li");

for (let i = 1; i < 6; i++) {
// You can't do this!
 liTag.textContent = i.toString();
 ulTag.append(liTag);
}

for (let i = 1; i < 6; i++) {
// You can do this!
 let newLiTag = document.createElement("li");
 newLiTag.textContent = i.toString();
 ulTag.append(newLiTag);
}
```
You can always use `insertAdjacentElement`, in which you can choose the position of the element to be inserted.

---
## HTML from strings using innerHTML

```js
const myHTML = `
	<h1>Hey this is cool too!</h1>
`

const element = document.querySelector(".item");
element.innerHTML = myHTML;
```
This is html is written inside back ticks, so can use variables here too. `${variableHere}`

unless this string has not been set to `innerHTML` or browser have not compiled the HTML inside that string, You can't set or get any property from it, as its just a string.

or 

You can covert the string, into a `Node` (once its a node you can, treat it as a html element) by using 

```js
var tagString = "<div>I am a div node</div>";
var range = document.createRange();

// Make the parent of the first div in the document become the context node
range.selectNode(document.getElementsByTagName("div").item(0));
var documentFragment = range.createContextualFragment(tagString);
document.body.appendChild(documentFragment);
```
---
## XSS
As here we allow any string to be HTML, If someone adds a `<script>`, then they can run js on your page. Which is a major security threat!

This string could be taken from an input box, so anyone could run js on your page!
```js
const myHTML = `
	<h1>Hey this is cool too!</h1>
	<script> crazy js here! </script>
`

const element = document.querySelector(".item");
element.innerHTML = myHTML;
```
---
## Removing Nodes and Traversing

```html
<p>
	"wes" 		1st Node
	<b>bos</b>  2nd Node
	"is great!"	3rd Node
</p>
```
```js
const pTag = document.querySelector("p")
console.log(pTag.childNodes) // gives all the nodes, including text

> NodeList [text, b, text]
```

`firstElementChild` and `lastElementChild` gives first element (not text) node and last element node inside a parent element

`parentElement` gives the parent of that element.

You can chain these meathods, to move up or down in dom. Don't do this :)

Removing an element from the dom is pretty simple, but when you remove an element from the DOM, it remains in the js memory, so you can still access it.

```js
pTag.remove() 
// removed visually but still in memory

console.log(pTag)
// <p> </p>
```