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

## Sets
In ES6, there’s a new built-in object that behaves like a mathematical set and works similarly to an array. This new object is conveniently called a "Set".
	*Sets are not indexed-based - you do not refer to items in a set based on their position in the set
	*items in a Set can’t be accessed individually

### How to Create a Set
```
const games = new Set();
console.log(games);

// Output: Set {}
```
Or,
```
const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);
console.log(games);

// Output: Set {'Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart'}
```

### Modifying Sets
Use `.add()` and `.delete()` methods
Ex:
```
const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);

games.add('Banjo-Tooie');
games.add('Age of Empires');
games.delete('Super Mario Bros.');

console.log(games);

// Output: Set {'Banjo-Kazooie', 'Mario Kart', 'Banjo-Tooie', 'Age of Empires'}
```

To delete all the items from a Set, use `.clear()` method.
```
games.clear()
console.log(games);

// Output: Set {}
```

Note:
_If you attempt to .add() a duplicate item to a Set, you won’t receive an error, but the item will not be added to the Set. Also, if you try to .delete() an item that is not in a Set, you won’t receive an error, and the Set will remain unchanged. Both methods return true if an item is successfully added or deleted from the Set and false if unsuccessful._

### Checking The Length
`.size` property returns the number of items
Sets can’t be accessed by their index like an array, so you use the .size property instead of .length property.

### Checking If An Item Exists
`.has()` method to check if an item exists in a Set, returns `true` or `false`

### Retrieving All Values
`.values()` method to return the values in a Set, returns `SetIterator` object.
```
console.log(months.values());
//Output: SetIterator {'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'}
```

