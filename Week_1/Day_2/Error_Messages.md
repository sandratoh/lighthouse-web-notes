# Common Error Messages and How to Debug

## Syntax Errors

Javascript Codes:

``` Javascript
var rank = "Imperator";
var name = "Furiosa";

console.log(rank name);
```

Terminal Codes:
```
node syntax-error.js
/vagrant/w1d2/syntax-error.js:4
console.log(rank name);
                 ^^^^
SyntaxError: Unexpected identifier
    at exports.runInThisContext (vm.js:73:16)
    at Module._compile (module.js:443:25)
    at Object.Module._extensions..js (module.js:478:10)
    at Module.load (module.js:355:32)
    at Function.Module._load (module.js:310:12)
    at Function.Module.runMain (module.js:501:10)
    at startup (node.js:129:16)
    at node.js:814:3
```

### Breaking down the errors

* First line of error message: 
  ```
  /vagrant/w1d2/syntax-error.js:4
  ```
  Tells us where the error occurred
    * In a file called `/vagrant/w1d2/syntax-error.js`
    
    * At line `4`

* Next three lines of error message:
  ```
  console.log(rank name);
                 ^^^^
  SyntaxError: Unexpected identifier
  ```
  Shows where exactly in the code the error occured, and that we're dealing with a `SyntaxError`.
  * Something seems to be wrong with `name`, which JavaScript is calling an `Unexpected identifier`.

  * Go back to code and find the error is we forgot to separate `rank` and `name` with a comma `,` when logging to console

* Last bit of error message = **stack trace** shows the state of our program when the error occurred (more about this in the future)
    ```
        at exports.runInThisContext (vm.js:73:16)
    at Module._compile (module.js:443:25)
    at Object.Module._extensions..js (module.js:478:10)
    at Module.load (module.js:355:32)
    at Function.Module._load (module.js:310:12)
    at Function.Module.runMain (module.js:501:10)
    at startup (node.js:129:16)
    at node.js:814:3
    ```
  
## Trickier Syntax Errors

Javascript Codes
```javascripting
if (5 > 10) {
  console.log("Impossible!");

console.log("Phew, logical fallacies avoided.");
```

Terminal Error
```
/vagrant/w1d2/syntax-error2.js:6
});
 ^
SyntaxError: Unexpected token )
    at exports.runInThisContext (vm.js:73:16)
    at Module._compile (module.js:443:25)
    at Object.Module._extensions..js (module.js:478:10)
    at Module.load (module.js:355:32)
    at Function.Module._load (module.js:310:12)
    at Function.Module.runMain (module.js:501:10)
    at startup (node.js:129:16)
    at node.js:814:3
  ```

  *What is strange*: error message references line 6, but JavaScript shows only 4 lines of code

  `SyntaxError: Unexpected token )` means when JavaScript expected something that wasn't there (codes may be missing a parenthesis, bracket or curly braces).

## Reference Errors

JavaScript Codes:
```javascript
var firstName = "Jane";
var lastName = "Doe";

console.log(firstName, lasName);
```

Terminal Codes
```
node reference-error.js
/vagrant/w1d2/reference-error.js:4
console.log(firstName, lasName);
                       ^
ReferenceError: lasName is not defined
    at Object.<anonymous> (/vagrant/w1d2/reference-error.js:4:24)
    at Module._compile (module.js:460:26)
    at Object.Module._extensions..js (module.js:478:10)
    at Module.load (module.js:355:32)
    at Function.Module._load (module.js:310:12)
    at Function.Module.runMain (module.js:501:10)
    at startup (node.js:129:16)
    at node.js:814:3
```

### Breaking down the errors
* First line of error tells us error is most likely coming from line 4
* Next few lines points out where in the code the error occured (`lasName` not defined)
* `ReferenceError` occurs when trying to use the value of an undefined variable (common error in day-to-day development).

## Type Errors

Javascript Codes
```javascript
var favouriteMeal = "BREAKFAST";

console.log(favouriteMeal.toLower());
```

Terminal Codes
```
node type-error.js
/vagrant/w1d2/type-error.js:3
console.log(favouriteMeal.toLower());
                          ^
TypeError: undefined is not a function
    at Object.<anonymous> (/vagrant/w1d2/type-error.js:3:27)
    at Module._compile (module.js:460:26)
    at Object.Module._extensions..js (module.js:478:10)
    at Module.load (module.js:355:32)
    at Function.Module._load (module.js:310:12)
    at Function.Module.runMain (module.js:501:10)
    at startup (node.js:129:16)
    at node.js:814:3
```

### Breaking down the error message
* First few lines:
  ```
  /vagrant/w1d2/type-error.js:3
  console.log(favouriteMeal.toLower());
                          ^
  ```
  Broke something at line 3, has something to do with `toLower`
* Error description:
  ```
  TypeError: undefined is not a function
  ```
  Something is `undefined` and we tried to make a function out of it.
  * Look back at code and see we are trying to call two functions (`console.log` and `favouriteMeal.toLower`). JS is telling us one of them is undefined, drawing our attention to `toLower`
  * A quick Google search will show that we simply forgot the name of the prototype function that converts a string to lowercase `.toLowerCase()`

## Summary
* There is a general pattern to fixing code errors.
* Read error messages closely, and carefully, then inspect the suspicious line of code for typos, syntax error or other mistakes
* WE can never avoid introducing errors in our code, but we can get better at fixing them.