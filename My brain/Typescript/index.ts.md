# Tuple
An array which already has defined type for a specific postion in it.
```ts
let person: [number, string, boolean] = [1, "tanvesh", true];
let employee: [number, string][];

employee = [
	[1, "asd"],
	[2, "tan"]
]
```

# Enum
With enums you can make constants 

```ts
enum Direction{
	Up,
	Down,
	Left,
	Right
}

enum Direction2{
	Up = "Up",
	Down = "Down",
	Left = "Left",
	Right = "Right"
}

console.log(Direction.Up)
console.log(Direction.Down)

console.log(Direction2.Left)

> 0
> 1
> "Left"
```
By defualt, every values will be from 0 to some number. But you can also give it values.

# Type Assertion
```ts
let cid: any = 1;
let customerId = <number>cid;
// here customerId now will be of number type and cid has to a number

let customId = cid as number;
// we can also do this
```


# Interfaces
```ts
interface UserInterface {
	readonly id: number;
	age?: number;
	name: string;
}
```

you can also have readonly properties in an interface. so if you try changing it, compiler will throw an error.

```ts
interface PersonInterface {
	id: number
	name: string
	register(): string
}

class Person implements PersonInterface {
	id: number;
	name: string;

	constructor(id: number, name: string){
		this.id = id;
		this.name = name;
	}

	register() {
		return `${this.name} is now registered`
	}
}
```

# Generics
Generics are basically Types but with placeholders. So that we can reuse these types.

```ts
function getArray<T>(items: T[]): T[]{
	return new Array().concat(items)
}

let numArray = getArray<number>([1, 2, 3, 4])
let strArray = getArray<string>(["tanves", "last"])
```