# Space Complexity

## Space Complexity vs Time Complexity

**Space complexity**: How much more **memory use (RAM)** do we need as the inputs provided to the code gets larger?

**Time complexity**: How much more **runtime** do we need as the inputs provided to the code gets larger?

Both use the [_Big O Notation_](./Big_O_Notation).

## Rule of Thumb

- Storing values in **variables** always takes up memory (RAM)

- Most primitives (booleans and numbers) take up **O(1) / Constant Space**

  - Eg: `const x = 100` and `const x = 99999999` take up the **same** amount of memory

- Strings, Arrays, and Objects take up **O(n) / Linear Space**

  - Eg: An array with 4 elements take up **twice** the memory of array with 2 elements

## Examples

```js
// O(1) Space Complexity
// -- number variable is constant spaced

const sum = arr => {
  let total = 0;
  arr.forEach(num => {
    total += num;
  });
  return total;
};
```

```js
// O(n) Space Complexity
// -- string variable is linear spaced

const reverseString = str => {
  let reversedStr = '';
  for (let i = 0; i < str.length; i++) {
    reversedStr = str[i] + reversedStr;
  }
  return reversedStr;
};
```

```js
// O(n/2) --> O(n) Space Complexity
// -- Big O Notation applies (remove constants and non-dominant terms)

const keepRandom = arr => {
  let resArr = [];
  arr.forEach(item => {
    if (Math.random() < 0.5) {
      resArr.push(item);
    }
  });
  return resArr;
};
```
