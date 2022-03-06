# Variables and Statements
---
```js
var first = "wes";

let age = 400;

const cool = true;
```

When a variable is declared in js, and has not given any value, then it points to `undefined`

## let, const and var
`var` and `let`  variables can be updated after declaration
`const` can't be updated, will result in an error.

Without using strict mode you could do something like this in js, but will throw an error if using it:  `'use strict;'`

```js 
dog = "Tommy" // 
```

#### Scoping in let, const and var
`let` is function Scoped and
`const` and `let` is block scoped

`cosnt` and `let` was introduced in es6 while let has been around for a while.