# ES6 Built-ins

## Symbols
A symbol is a unique and immutable data type that is often used to identify object properties.
```
const sym1 = Symbol('apple');
console.log(sym1);

// Output: Symbol(apple)
```

```
const bowl = {
  [Symbol('apple')]: { color: 'red', weight: 136.078 },
  [Symbol('banana')]: { color: 'yellow', weight: 183.15 },
  [Symbol('orange')]: { color: 'orange', weight: 170.097 },
  [Symbol('banana')]: { color: 'yellow', weight: 176.845 }
};
console.log(bowl);

// Output: Object {Symbol(apple): Object, Symbol(banana): Object, Symbol(orange): Object, Symbol(banana): Object}
```

## Iteration & Iterable Protocols
	> The iterable protocol is used for defining and customizing the iteration behavior of objects.
	> The iterator protocol is used to define a standard way that an object produces a sequence of values. What that really means is you now have a process for defining how an object will iterate. This is done through implementing the .next() method.

Ex: (from Test)
```
/*
 * Programming Quiz: Make An Iterable Object
 *
 * Turn the `james` object into an iterable object.
 *
 * Each call to iterator.next should log out an object with the following info:
 *     - key: the key from the `james` object
 *     - value: the value of the key from the `james` object
 *     - done: true or false if there are more keys/values
 *
 * For clarification, look at the example console.logs at the bottom of the code.
 */

const james = {
    name: 'James',
    height: `5'10"`,
    weight: 185,
    [Symbol.iterator]: function(){
        let properties = Object.keys(james);
        let count = 0;
        let isDone = false;
        let next = () => {
            if (count == ( properties.length - 1 )){
                isDone = true;
            }
            return{ key: properties[count], value: this[properties[count++]], done: isDone };
        }
        return{next};
    }
};


let iterator = james[Symbol.iterator]();

console.log(iterator.next()); // 'James'
console.log(iterator.next()); // `5'10`
console.log(iterator.next()); // 185

// Output:
/*
{ key: 'name', value: 'James', done: false }
{ key: 'height', value: '5\'10"', done: false }
{ key: 'weight', value: 185, done: true }
*/
```