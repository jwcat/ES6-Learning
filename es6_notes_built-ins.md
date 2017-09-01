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

## Proxies
-use the Proxy constructor - `new Proxy();`
-takes two items:
* the object that it will be the proxy for
* an object containing the list of methods it will handle for the proxied object, called handler
Ex:
```
var richard = {status: 'looking for work'};
var agent = new Proxy(richard, {});

agent.status; // returns 'looking for work'
```

### Get Trap
The `get` trap is used to "intercept" calls to properties:
```
const richard = {status: 'looking for work'};
const handler = {
    get(target, propName) {
        console.log(target); // the `richard` object, not `handler` and not `agent`
        console.log(propName); // the name of the property the proxy (`agent` in this case) is checking
    }
};
const agent = new Proxy(richard, handler);
agent.status; // logs out the richard object (not the agent object!) and the name of the property being accessed (`status`)
```

#### Accessing the Target object from inside the proxy
```
const richard = {status: 'looking for work'};
const handler = {
    get(target, propName) {
        console.log(target);
        console.log(propName);
        return target[propName];
    }
};
const agent = new Proxy(richard, handler);
agent.status; // (1)logs the richard object, (2)logs the property being accessed, (3)returns the text in richard.status
```

#### Having the proxy return info, directly
```
const richard = {status: 'looking for work'};
const handler = {
    get(target, propName) {
        return `He's following many leads, so you should offer a contract as soon as possible!`;
    }
};
const agent = new Proxy(richard, handler);
agent.status; // returns the text `He's following many leads, so you should offer a contract as soon as possible!`
```

### Set Trap
-used for intercepting code that will change a property
```
const richard = {status: 'looking for work'};
const handler = {
    set(target, propName, value) {
        if (propName === 'payRate') { // if the pay is being set, take 15% as commission
            value = value * 0.85;
        }
        target[propName] = value;
    }
};
const agent = new Proxy(richard, handler);
agent.payRate = 1000; // set the actor's pay to $1,000
agent.payRate; // $850 the actor's actual pay
```

### Other Traps
1. the get trap - lets the proxy handle calls to property access
2. the set trap - lets the proxy handle setting the property to a new value
3. the apply trap - lets the proxy handle being invoked (the object being proxied is a function)
4. the has trap - lets the proxy handle the using in operator
5. the deleteProperty trap - lets the proxy handle if a property is deleted
6. the ownKeys trap - lets the proxy handle when all keys are requested
7. the construct trap - lets the proxy handle when the proxy is used with the new keyword as a constructor
8. the defineProperty trap - lets the proxy handle when defineProperty is used to create a new property on the object
9. the getOwnPropertyDescriptor trap - lets the proxy handle getting the property's descriptors
10. the preventExtenions trap - lets the proxy handle calls to Object.preventExtensions() on the proxy object
11. the isExtensible trap - lets the proxy handle calls to Object.isExtensible on the proxy object
12. the getPrototypeOf trap - lets the proxy handle calls to Object.getPrototypeOf on the proxy object
13. the setPrototypeOf trap - lets the proxy handle calls to Object.setPrototypeOf on the proxy object

## Generators
### Pausable Functions
```
function* getEmployee() {
    console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        console.log( name );
    }

    console.log('the function has ended');
}
```
_asterisk indicates that this function is actually a generator_

### Generators & Iterators
When a generator is invoked - it creates and returns an iterator. This iterator can then be used to execute the actual generator's inner code.
```
const generatorIterator = getEmployee();
generatorIterator.next();
```

Produces the code we expect:
```
the function has started
Amanda
Diego
Farrin
James
Kagure
Kavita
Orit
Richard
the function has ended
```

### The Yield Keyword
`yield` is what causes the generator to pause
```
function* getEmployee() {
    console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        console.log(name);
        yield;
    }

    console.log('the function has ended');
}
```

```
const generatorIterator = getEmployee();
generatorIterator.next();
```
Logs the following to the console:
```
the function has started
Amanda
```

It's paused! But to really be sure, let's check out the next iteration:
`generatorIterator.next();`

Logs the following to the console:
`Diego`

### Yielding Data to the "Outside" World
```
function* getEmployee() {
    console.log('the function has started');

    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];

    for (const name of names) {
        yield name;
    }

    console.log('the function has ended');
}

const generatorIterator = getEmployee();
let result = generatorIterator.next();
result.value // is "Amanda"

generatorIterator.next().value // is "Diego"
generatorIterator.next().value // is "Farrin"
```

### Sending Data into/out of a Generator
- yield keyword is used to pause a generator and used to send data outside of the generator, and then the .next() method is used to pass data into the generator
```
function* getEmployee() {
    const names = ['Amanda', 'Diego', 'Farrin', 'James', 'Kagure', 'Kavita', 'Orit', 'Richard'];
    const facts = [];

    for (const name of names) {
        // yield *out* each name AND store the returned data into the facts array
        facts.push(yield name); 
    }

    return facts;
}

const generatorIterator = getEmployee();

// get the first name out of the generator
let name = generatorIterator.next().value;

// pass data in *and* get the next name
name = generatorIterator.next(`${name} is cool!`).value; 

// pass data in *and* get the next name
name = generatorIterator.next(`${name} is awesome!`).value; 

// pass data in *and* get the next name
name = generatorIterator.next(`${name} is stupendous!`).value; 

// you get the idea
name = generatorIterator.next(`${name} is rad!`).value; 
name = generatorIterator.next(`${name} is impressive!`).value;
name = generatorIterator.next(`${name} is stunning!`).value;
name = generatorIterator.next(`${name} is awe-inspiring!`).value;

// pass the last data in, generator ends and returns the array
const positions = generatorIterator.next(`${name} is magnificent!`).value; 

// displays each name with description on its own line
positions.join('\n');
```