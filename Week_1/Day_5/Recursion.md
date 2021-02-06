# Recursion

## Intro to Recursion
**What is recursion?**
* *A function that calls itself until it doesn't*
* An alternative to traditional looping
* It does the same thing, but in a slightly different way
* Some languages don't have any `for` or `while` loops, and recursion is the only way of repeating codes

## Recursion By Example

### `for` Loop
```javascript
for (let number = 0; number <= 12; number += 2) {
  console.log(number);
}
```

### `while` loop
```javascript
let number = 0;
while (number <= 12) {
  console.log(number);
  number += 2;
}
```

### `recursion` loop
```javascript
1.| function countEvenToTwelve(number) {
2.|   if (number <= 12) {
3.|     console.log(number);
4.|     countEvenToTwelve(number+2);
5.|   }
6.| }
7.| countEvenToTwelve(0);
```

**Explanation**
* Recursive function calling itself on line 4 to execute code over and over again *(kind of like a loop)*
* Function continues calling itself until it hits its condition `number <= 12`
  * **recursive case** : as long as it is true, the function will continue to call itslf
* As soon as `number > 12`, the function stops calling itself, and the looping ends
  * **base case**: if this is true, the function will not call itself (when the problem can be resolved without further recursion)
* Each time `countEvenToTwelve` calls itself (on line 4), it passes in a different input value, increment by its parameter
* In a properly designed recursive function, with each recursive call, the input must gradually resolve toward (get closer to) the base case

**Infinte Loop** (*Avoid!!!*)
* Like `while` loop, every recursive function **must** stop calling itself at some point (`if` statements), or...
* Infinite loop happens (and your program may crash)
* Example below has recursive function that never stops calling itself
  ```javascript
  function countUpFrom(number) {
    console.log(number);
    countUpFrom(number+1);
  }
  countUpFrom(1);
  ```
* The example will return `RangeError: Maximum call stack size exceeded` AKA **`Stack Overflow`**!!