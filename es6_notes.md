# ES6 Notes

Harmony, ES6, ES2015, are names of the same thing, a Javascript update.

## let and const
* Variables declared with **let** can be reassigned, but can’t be redeclared in the same scope.
* Variables declared with **const** must be assigned an initial value, but can’t be redeclared in the same scope, and can’t be reassigned.

_Using **var** is no longer recommended but can still be used._

## Template Literals
Template literals are essentially string literals that include embedded expressions.
Denoted with backticks ( `` ) instead of single quotes ( '' ) or double quotes ( "" ), template literals can contain placeholders which are represented using ${expression}.

ex:
const myName = 'John';
const greeting = `Hello, my name is ${myName}`;
console.log(greeting);

## Destructuring

### Destructuring values from an array:
const point = [10, 25, -34];
const [x, y, z] = point;
console.log(x, y, z);

_You can also ignore values when destructuring arrays._
_For example, const [x, , z] = point; ignores the y coordinate and discards it._

### Destructuring values from an object
const gemstone = {
  type: 'quartz',
  color: 'rose',
  karat: 21.29
};

const {type, color, karat} = gemstone;
console.log(type, color, karat);

_TIP: You can also specify the values you want to select when destructuring an object._
_For example, let {color} = gemstone; will only select the color property from the gemstone object._
