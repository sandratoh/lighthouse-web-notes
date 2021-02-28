# Complexity: Elementary Operations and Running Time

## Intro to Algorithm Complexity

* **Algorithmic complexity** - how fast or slow a particular algorithm is

* Difficult to measure speed based on time b/c of variety of different computers, languages, and OS, so...

* Measure algorithm speed by counting up all of its **elementary operations** which gives us a **running time** 

> Time complexity (AKA running time) is commonly estimated by counting the number of elementary operations performed by an algorithm. It takes a fixed amount of time to perform an elementary operation.

## Elementary Operations

* Definition: any operation that takes a fixed/constant amount of time to perform, regardless of the data

### Examples 1 - Simple Operations:
```javascript
let result = 0;
result += number1;
result += number2;
console.log(result);
```
* Perform 4 different operations
* Relies on 2 variables
* Regardless of what values are in the variables, the 4 operations will always take the same amount of time... therefore:
* Num of elementary operations = 4
* Running time = 4

### Example 2 - Dynamic Data:
```javascript
let result = 0;

for (let i = 0; i < array.length; i++) {
  let number = array[i];
  result += number;
}

console.log(result);
```
Reorganized example - use `n` to represent the length of an array
```javascript
let result = 0; // 1

for (
  let i = 0; // 1
  i < array.length; // n + 1
  i++ // n
) {
  let number = array[i]; // n
  result += number; // n
}

console.log(result); // 1
```
|`1`                  |`n`                     |`n+1`                |
|---------------------|------------------------|---------------------|
|`let result = 0;`    |`i++`                   | `i < array.length;` |
|`let i = 0;`         |`let number = array[i];`| -                   |
|`console.log(result)`|`result += number`      | -                   |

* Running time calculation:
  * `3 + (n * 3) + n + 1` to
  * `4 + (n * 4)` which is written as...
  * `4n + 4` = runtime

---

## Running Time of Binary Search

* An array of length 8 would need at most four guesses
  * 8 -> 4 -> 2 -> 1 | no further guesses after

* An array of length 16 would need at most five guesses
  * 16 -> 8 -> 4 -> 2 -> 1 | no further guesses after

### Pattern:
> Every time we *double the size* of the array, we need at most *one more guess*

* Given array length of `n` would need at most `m` guesses

* An array length of `2n` would need at most `m+1` guesses

* Repeatedly half the array (starting at `n`) until we get the value 1, plus one => **log<sub>2</sub>*n*** (base-2 logarithm of `n`)