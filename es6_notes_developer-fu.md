## ES6 Specification
The specification (commonly shortened to "spec") for ES6:
http://www.ecma-international.org/ecma-262/6.0/index.html

## Supported Features
* Google Chrome - https://www.chromestatus.com/features#ES6
* Microsoft Edge - https://developer.microsoft.com/en-us/microsoft-edge/platform/status/?q=ES6
* Mozilla Firefox - https://platform-status.mozilla.org/

ECMAScript Compatibility Table:
http://kangax.github.io/compat-table/es6/

## Polyfills
Ex:
```
if (!String.prototype.startsWith) {
  String.prototype.startsWith = function (searchString, position) {
    position = position || 0;
    return this.substr(position, searchString.length) === searchString;
  };
}
```

## Transpiling
The most popular JavaScript transpiler is called Babel: https://babeljs.io/
