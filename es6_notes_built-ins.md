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

### Looping over Sets
Using the SetIterator:
```
const iterator = months.values();
iterator.next();
//Output: Object {value: 'January', done: false}
```
Using a `for...of` Loop:
```
const colors = new Set(['red', 'orange', 'yellow', 'green', 'blue', 'violet', 'brown', 'black']);
for (const color of colors) {
  console.log(color);
}

/*
Output:
red 
orange 
yellow 
green 
blue 
violet 
brown 
black
*/
```


## WeakSets
A WeakSet is just like a normal Set with a few key differences:
1. a WeakSet can only contain objects
2. a WeakSet is not iterable which means it can’t be looped over
3. a WeakSet does not have a .clear() method
Ex:
```
const student1 = { name: 'James', age: 26, gender: 'male' };
const student2 = { name: 'Julia', age: 27, gender: 'female' };
const student3 = { name: 'Richard', age: 31, gender: 'male' };

const roster = new WeakSet([student1, student2, student3]);
console.log(roster);

// Output: WeakSet {Object {name: 'Julia', age: 27, gender: 'female'}, Object {name: 'Richard', age: 31, gender: 'male'}, Object {name: 'James', age: 26, gender: 'male'}}
```
example from quiz:
```
/*
 * Programming Quiz: Using Sets (3-2)
 *
 * Create the following variables:
 *     - uniqueFlavors and set it to a new WeakSet object
 *     - flavor1 and set it equal to `{ flavor: 'chocolate' }`
 *     - flavor2 and set it equal to an object with property 'flavor' and value of your choice!
 *
 * Use the `.add()` method to add the objects `flavor1` and `flavor2` to `uniqueFlavors`
 * Use the `.add()` method to add the `flavor1` object (again!) to the `uniqueFlavors` set
 */

const uniqueFlavors = new WeakSet();

const flavor1 = {flavor: 'chocolate'};
const flavor2 = {flavor: 'vanilla'};

uniqueFlavors.add(flavor1);
uniqueFlavors.add(flavor2);
uniqueFlavors.add(flavor1);

console.log(uniqueFlavors);
```

## Maps
Map is an object that lets you store key-value pairs where both the keys and the values can be objects, primitive values, or a combination of the two
Ex:
```
const employees = new Map();
console.log(employees);

// Output: Map {}
```
Add key-values by using the Map’s .set() method.
```
const employees = new Map();

employees.set('james.parkes@udacity.com', { 
    firstName: 'James',
    lastName: 'Parkes',
    role: 'Content Developer' 
});
employees.set('julia@udacity.com', {
    firstName: 'Julia',
    lastName: 'Van Cleve',
    role: 'Content Developer'
});
employees.set('richard@udacity.com', {
    firstName: 'Richard',
    lastName: 'Kalehoff',
    role: 'Content Developer'
});

console.log(employees);

// Output: Map {'james.parkes@udacity.com' => Object {...}, 'julia@udacity.com' => Object {...}, 'richard@udacity.com' => Object {...}}
```

`.delete()` method removes key-value pairs
```
employees.delete('julia@udacity.com');
employees.delete('richard@udacity.com');
console.log(employees);

// Output: Map {'james.parkes@udacity.com' => Object {firstName: 'James', lastName: 'Parkes', role: 'Course Developer'}}
```

`.clear()` method removes all key-value pairs

`.has()` method to check if a key-value pair exists
```
const members = new Map();

members.set('Evelyn', 75.68);
members.set('Liam', 20.16);
members.set('Sophia', 0);
members.set('Marcus', 10.25);

console.log(members.has('Xavier'));
console.log(members.has('Marcus'));

// Output:
// false
// true
```

`.get()` method
```
console.log(members.get('Evelyn'));
// Output: 75.68
```

### Looping Through Maps
#### 1. Using the MapIterator:
```
let iteratorObjForKeys = members.keys();
iteratorObjForKeys.next();
// Output: Object {value: 'Evelyn', done: false}
```
use the `.values()` method to access the Map’s values
```
let iteratorObjForValues = members.values();
iteratorObjForValues.next();
// Output: Object {value: 75.68, done: false}
```

#### 2. Using a `for...of` Loop
```
for (const member of members) {
  console.log(member);
}
 
// Output:
// ['Evelyn', 75.68]
// ['Liam', 20.16]
// ['Sophia', 0]
// ['Marcus', 10.25]
 ```

_When you use a for...of loop with a Map, you don’t exactly get back a key or a value. Instead, the key-value pair is split up into an array where the first element is the key and the second element is the value..._
Solution:
```
/*
 * Using array destructuring, fix the following code to print the keys and values of the `members` Map to the console.
 */

const members = new Map();

members.set('Evelyn', 75.68);
members.set('Liam', 20.16);
members.set('Sophia', 0);
members.set('Marcus', 10.25);

for (const member of members) {
    const [a, b] = member;
    console.log(a, b);
}
```

#### 3. Using a forEach Loop
```
members.forEach((value, key) => console.log(value, key));

// Output:
// 'Evelyn' 75.68
// 'Liam' 20.16
// 'Sophia' 0
// 'Marcus' 10.25
 ```

 ## Weakmaps
A WeakMap is just like a normal Map with a few key differences:
- a WeakMap can only contain objects as keys,
- a WeakMap is not iterable which means it can’t be looped and
- a WeakMap does not have a .clear() method.
Ex:
```
const book1 = { title: 'Pride and Prejudice', author: 'Jane Austen' };
const book2 = { title: 'The Catcher in the Rye', author: 'J.D. Salinger' };
const book3 = { title: 'Gulliver’s Travels', author: 'Jonathan Swift' };

const library = new WeakMap();
library.set(book1, true);
library.set(book2, false);
library.set(book3, true);

console.log(library);

// Output: WeakMap {Object {title: 'Pride and Prejudice', author: 'Jane Austen'} => true, Object {title: 'The Catcher in the Rye', author: 'J.D. Salinger'} => false, Object {title: 'Gulliver’s Travels', author: 'Jonathan Swift'} => true}
```
### Garbage Collection
If you set an object to null, then you’re essentially deleting the object.
```
book1 = null;
console.log(library);

// Output: WeakMap {Object {title: 'The Catcher in the Rye', author: 'J.D. Salinger'} => false, Object {title: 'Gulliver’s Travels', author: 'Jonathan Swift'} => true}
```

## Promises
Created with the new Promise constructor function - new Promise(). 
A promise will let you start some work that will be done asynchronously and let you get back to your regular work. 
When you create the promise, you must give it the code that will be run asynchronously. You provide this code as the argument of the constructor function:
```
new Promise(function () {
    window.setTimeout(function createSundae(flavor = 'chocolate') {
        const sundae = {};
        // request ice cream
        // get cone
        // warm up ice cream scoop
        // scoop generous portion into cone!
    }, Math.random() * 2000);
});
```

### Indicated a Successful Request or a Failed Request
By passing two functions into our initial function. Typically we call these resolve and reject.
```
new Promise(function (resolve, reject) {
    window.setTimeout(function createSundae(flavor = 'chocolate') {
        const sundae = {};
        // request ice cream
        // get cone
        // warm up ice cream scoop
        // scoop generous portion into cone!
        if ( /* iceCreamConeIsEmpty(flavor) */ ) {
            reject(`Sorry, we're out of that flavor :-(`);
        }
        resolve(sundae);
    }, Math.random() * 2000);
});
```

### Promises Return Immediately
a Promise will immediately return an object
```
const myPromiseObj = new Promise(function (resolve, reject) {
    // sundae creation code
});
```

That object has a .then() method on it that we can use to have it notify us if the request we made in the promise was either successful or failed. The .then() method takes two functions:

1. the function to run if the request completed successfully
2. the function to run if the request failed to complete
```
mySundae.then(function(sundae) {
    console.log(`Time to eat my delicious ${sundae}`);
}, function(msg) {
    console.log(msg);
    self.goCry(); // not a real method
});
```

