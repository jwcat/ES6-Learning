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

