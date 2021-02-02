# Lotide Library assertEqual
## Usage:
To be able to see a series of success / failures messages printed to console when testing function codes

## Built-in `console.assert()` method:
* JavaScript's built-in function
* [`console.assert` docs](https://developer.mozilla.org/en-US/docs/Web/API/console/assert) on MDN
* **Returns**:
  * writes an error message to console if the assertion is false
  * nothing happens if assertion is true
* **Syntax**:
```JavaScript
console.assert(assertion, obj1 [, obj2, ..., objN]);
console.assert(assertion, msg [, subst1, ..., substN]); // C-like message formatting
```
* **Parameter**:
  * `assertion` = any boolean expression (*Hint*: use comparison operators). If assertion is false, the msg is written to the console.
  * `obj1` ... `objN` = a list of JS objects to output. The string representations of each of these objects are appened together in the order listed and output
  * `msg` = a JS string containing zero or more substitution strings
  * `subst1` ... `substN` = JS objects with which to replace substitution strings within `msg`. This parameter gives you additional control over the format of the output
* **Example**:
```Javascript
const errorMsg = 'the # is not even';
for (let number = 2; number <= 5; number += 1) {
    console.log('the # is ' + number);
    console.assert(number % 2 === 0, {number: number, errorMsg: errorMsg});
    // or, using ES2015 object property shorthand:
    // console.assert(number % 2 === 0, {number, errorMsg});
}
// output:
// the # is 2
// the # is 3
// Assertion failed: {number: 3, errorMsg: "the # is not even"}
// the # is 4
// the # is 5
// Assertion failed: {number: 5, errorMsg: "the # is not even"}
```
## Create own assertion function `assertEqual`
Custom assert function will also log a message to console verifying test cases. Except we can customize it with emoji to make it more colourful and verbose.