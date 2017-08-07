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