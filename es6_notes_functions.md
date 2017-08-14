# ES6 Notes - Functions

## Arrow functions
ES6 introduces a new kind of function called the arrow function. Arrow functions are very similar to regular functions in behavior, but are quite different syntactically.

Ex:
```
// regular function
const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(function(name) {
  return name.toUpperCase();
});

// arrow function
const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(
  name => name.toUpperCase()
);
```

*Regular functions can be either function declarations or function expressions.
*Arrow functions are function expressions, specifically called - "arrow function expressions"
	- stored in a variable
	- passed as an argument to a function
	- stored in an object's property

### Parentheses and arrow function parameteres
empty parameter list requires parentheses
` const sayHi = () => console.log('Hello Udacity Student!'); `

multiple parameters requires parentheses
```
const orderIceCream = (flavor, cone) => console.log(`Here's your ${flavor} ice cream in a ${cone} cone.`);
orderIceCream('chocolate', 'waffle');
```

### Concise and block body syntax
concise body syntax - has no curly braces surrounding the function body and automatically returns the expression
```
const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map(
  name => name.toUpperCase()
);
```

block body syntax -  more than just a single line of code
```
const upperizedNames = ['Farrin', 'Kagure', 'Asser'].map( name => {
  name = name.toUpperCase();
  return `${name} has ${name.length} characters in their name`;
});
```

### "this" and Arrow Functions
	* With regular functions, the value of this is set based on how the function is called.
	* With arrow functions, the value of this is based on the function's surrounding context.

## Default Function Parameters
ES6 has introduced a new way to create defaults.
It's called default function parameters.
They're placed in the function's parameter list.

Ex:
```
function greet(name = 'Student', greeting = 'Welcome') {
  return `${greeting} ${name}!`;
}

greet(); // Welcome Student!
greet('James'); // Welcome James!
greet('Richard', 'Howdy'); // Howdy Richard!
```

### Defaults and destructuring arrays
You can combine default function parameters with destructuring to create some pretty powerful functions!
Ex:
```
function createGrid([width = 5, height = 5]) {
  return 'Generates a ${width} x ${height} grid';
}

createGrid([]); // Generates a 5 x 5 grid
createGrid([2]); // Generates a 2 x 5 grid
createGrid([2, 3]); // Generates a 2 x 3 grid
createGrid([undefined, 3]); // Generates a 5 x 3 grid

createGrid(); // throws an error
```
So use default function parameters,
```
function createGrid([width = 5, height = 5] = []) {
  return 'Generating a grid of ${width} by ${height}';
}

createGrid(); // Generates a 5 x 5 grid
```

### Defaults and destructuring objects
Ex:
```
function createSundae({scoops = 1, toppings = ['Hot Fudge']}) {
  const scoopText = scoops === 1 ? 'scoop' : 'scoops';
  return 'Your sundae has ${scoops} ${scoopText} with ${toppings.join(' and ')} toppings.';
}

createSundae({}); // Your sundae has 1 scoop with Hot Fudge toppings.
createSundae({scoops: 2}); // Your sundae has 2 scoops with Hot Fudge toppings.
createSundae({scoops: 2, toppings: ['Sprinkles']}); // Your sundae has 2 scoops with Sprinkles toppings.
createSundae({toppings: ['Cookie Dough']}); // Your sundae has 1 scoop with Cookie Dough toppings.

createSundae(); // throws an error
```
So provide a default object to the function,
```
function createSundae({scoops = 1, toppings = ['Hot Fudge']} = {}) {
  const scoopText = scoops === 1 ? 'scoop' : 'scoops';
  return `Your sundae has ${scoops} ${scoopText} with ${toppings.join(' and ')} toppings.`;
}
```