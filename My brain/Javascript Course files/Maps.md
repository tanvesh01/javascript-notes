## Maps
In a map you have a key and a value. A key can be of **any** type! And order is guranteed, it will be in the same order as you inserted in.

```js
const myMap = new Map()
// set()
// get()
// has()
// delete()

myMap.set(100, "number Hundered!");

console.log(myMap.get(100));
> "number Hundered!"
```
Using key inside get, to *get* the value.

These keys can even be an object. Then later on you can use the same object to lookup the value inside the map.

You can also create a map like this :
```js
new Map([1, 2], [3, 4]);

// here 1 and 3 is keys, and 2 and 4 is values. 
```

1. You can't store functions inside map
2. If you care about the order of things then use map for sure
3. You can't really store Maps on the server, because it can't be converted to strings (as of now)