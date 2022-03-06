React has a Virtual DOM in memory and a copy of Current DOM as an Object in memory too. 

Whenever state or props change, react makes the necessary changes in the Virtual DOM and compares it with the current copy of DOM with its Diffing Algorithm. Once it knows what changes are there, it then figures out minimal things to do to make those changes to the Real DOM.