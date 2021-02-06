# Modules - Introduction

Modules help DRY up our codes so we don't have to copy & paste our codes in order to share codes between files.

## Every File in Node is a Module!

> Every file run by Node has access to a `module` object

Test it just with this one simple line:

```javascript
console.log(module);
```

Output:

```bash
Module {
  id: '.',
  path: '/vagrant',
  exports: {},
  parent: null,
  filename: '/vagrant/moduleCheck.js',
  loaded: false,
  children: [],
  paths: [ '/vagrant/node_modules', '/node_modules' ]
}
```

This is proof that:
> Each file that Node runs is actually considered a separate module!

## Exporting Modules
> A JS file must 'export' the part that it wants to be `require`-able (AKA 'importable'). Files usually export an object (or a function, which in JS is an object anyway).
* A key aspect of modules: `exports: {}`
  * By default, JS will export an **empty object** for each file
* A file can use functions written in other files, but first must do these steps:
  1. Export codes (otherwise, will return `TypeError` because of empty object)
  2. Import/required into main file (`require` statement)

## Exporting Modules
Syntax requires us to assign defined function to `module.exports`

```javascript
// myModule.js

const sayHelloTo = function(person) {
  console.log(`Hello, ${person}`);
}
// add this line to the end of the file.
module.exports = sayHelloTo;
```

Now the output of `console.log(module)` won't have an empty object for `exports`!

```bash
 Module {
  id: '.',
  path: '/vagrant',
  exports: [Function: sayHelloTo],
  parent: null,
  filename: '/vagrant/moduleCheck.js',
  loaded: false,
  children: [],
  paths: [ '/vagrant/node_modules', '/node_modules' ]
}
```

## Requiring a Module
Basic syntax to import a module from local filesystem using `require`:

```javascript
const sayHelloTo = require('./moduleCheck');
```
* This assumes that we have a file called `myModule.js` in the same directory as the file that is requiring the module

File extension is not necessary, but it would also work:

```javascript
const sayHelloTo = require('./moduleCheck.js');
```
* Common convention omits the `.js` extension, since it's fairly redundant

The imported object gets assigned to the variable `sayHelloTo` in the example above

## Conclusion
* Modules are node's way of organizing code into individual files

* Every js file in node is implicityly a module
  * Can `console.log(module)` and see its detail

* `module.exports` tell node what to export from a file
  * defaults to `{}` (an empty object)

* Can use `require` with relative paths inside same directory (like `./moduleCheck)`)
  * doesn't need the `.js` extension, as that is implied