# Primitive Data Types

### *What are they?*
Primitives are essential building blocks of data because they represent the simplest possible type of data that our software can have.

## The Six Primitive Types in JavaScript

* `undefined`
* `null`
* `boolean`
* `string`
* `number`
* `symbol` (introduced in ES6)

## Objects Are Not Primitives
* Anything not in that list is an object
* Arrays and functions are sub-category of objects
* Objects (including arrays, functions, and other types of objects) have *properties*.

### The six primitive types, plus `object`, make up the **seven fundamental types** of JavaScript

--

## Primitive Type don't have Properties ... but they have Corresponding Objects!
*(Note: excluding `symbol` which has weird rules)*

Example:
```javascript
typeof(true); 
// "boolean" 
typeof(Boolean(true)); 
// => "boolean" 
typeof(new Boolean(true));
// => "object"
/*  
  It is generally considered bad practice to use primitive object constructors (as shown in the final line above). 
*/
```
* Constructors are like regular functions.

* Two types of constructors in JavaScript : 
  1. built-in constructors like `Array` and `Object`
  2. create your own object constructor by invoking with the word `new`


* Each object has methods associated with them based on what constructor was used

### Why does `'someString.length` work?
Remember **type coercion** with loose equality `==` ? Similar thing is being done with the string!

The `someString` is **coerced to a string object** in order to access the property length. However, `someString` is still a primitive data type.

JavaScript temporarily turns primitive types into objects in order to make them act like objects.