# forEach Loops `Array.prototype.forEach()`

[Read more on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

#### `forEach()` method executes a provided function once or each array element

--

#### Example
Converting between `forEach()` loop and `for` loop

```javascript
// Sample array
const array1 = ['a', 'b', 'c'];

// for each loop
array1.forEach(element => console.log(element));

// for loop
for (let i = 0; i < array1.length; i++) {
  let element = array1[i];
  console.log(element);
}

// same expected output!
```