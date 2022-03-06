At ever render react's algorithm has to match two virtual doms

###### Roles of keys 
If we are rendering a list of elements by looping over an array and we dont have unique keys on every element. If we re-order that list, react will not be able to identify that only a part of the list has changed and not the whole list, and it will destroy all the nodes of list and create them again

###### How Reconcilation work in React
On the next state or props update, that `render()` function will return a different tree of React elements. React then needs to figure out how to efficiently update the UI to match the most recent tree.

The Diffing algorithm will help react in deciding which part of the old tree to update

###### How does this diffing algorithm work?

**When the Element type is diffrent** during comparision, React will "*tear down*" the old tree from this point and build the new tree from scratch.

How does tearing down of component works?
![[Pasted image 20220211173229.png]]
`componentWillUnmount()` -> *component unmounts and DOM element gets destroyed* -> *New DOM nodes are created* ->  `UNSAFE_componentWillMount()` => `componentDidMount()`

**When the DOM Element is of the same type** then React compares the attributes on the element, if they are diffrent then it will only update the atrributes that changed

**When the Component Elements of the Same Type**, the Instance stays the same so that the current state of the component is preserved. React then updates the props of the same instance of component to match the new component