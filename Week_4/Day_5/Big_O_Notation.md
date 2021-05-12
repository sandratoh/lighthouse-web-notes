# Big O Notation

The official way to determine the _efficiency_ of algorithms - **Big O Notation**

Possible technical interview Q: evaluate the running time of an algorithm using Big O notation.

_Note_: Big O is evaluating worst case scenario, the opposite of `O` is the best case scenario known as Ω (omega)

## Intro

- Syntax: `O()`

- Describes the scalability of an algorithm's steps relative to its input

> As we increase the amount of data, does the algorithm grow _linearly_, _exponentially_, or _logarithmically_?

- Three main things to remember when using Big O notation:

  1. Only care about arbitrarily large input

  - What does the run time look like when we give it an array of one million items?

  2. Drop the non-dominant terms

  - Eg: when our running time is `(n^2+n)/2`, only `n^2` matters, and we can ignore the rest

  3. Drop constant terms

  - Eg: when graphing `(n^3)/2` or `(n^3)*2`, curve is pretty much the same as `n^3`, so we can just get rid of constant `2`

## Arbitrarily Large Input

- For small values, it doesn't really matter which one is faster or more efficient

- Also, it's difficiult to identify the more efficient algorithm

## Drop Non-Dominant Terms

- Certain terms cease to make a difference and becomes _insignificant_ when `n` gets arbitrarily large

- Example:

  - Running time: `100n + n^2`
  - Big O notation: `O(n^2)`

- Big O is only interested in the **highest order term** - the larger the exponential number, the bigger the term

- Example:
  - Running time: `n^0 + n^1 + n^2 + n^3 + n^4`
  - Big O notation: `O(n^4)`

## Drop Constants

- Big O notation is NOT used to describe the exact running time - only how its complexity grows _relative_ to its input

- Constants will not affect an algorithm's _growth rate_

- Example:

  - Algorithm:
    ```javascript
    for (let i = 0; i < array.length; i++) {
      // Do 100 different operations in each iteration
    }
    ```
  - Running time: `102n + 2`
    - Complexity grows linearly, `2` and `102` will stay constant regardless of input
  - Big O notation: `O(n)`

- More Examples

| Running Time        | Growth Rate Pattern   | Big O notation |
| ------------------- | --------------------- | -------------- |
| `3`                 | Constant              | `O(1)`         |
| `2n + 3`            | Linear                | `O(n)`         |
| `100n^2`            | Exponential/Quadratic | `O(n^2)`       |
| `log n + 100000000` | Logarithmic           | `O(log n)`     |

## Computational Complexity

Chart showing from fastest to slowest running time

| Big O notation         | Growth Rate Pattern |
| ---------------------- | ------------------- |
| `O(1)`                 | Constant            |
| `O(log n)`             | Logarithmic         |
| `O(n)`                 | Linear              |
| `O(n log n)`           | Lineararithmic      |
| `O(n`<sup>`2`</sup>`)` | Quadratic           |
| `O(n`<sup>`c`</sup>`)` | Polynomialic        |
| `O(c`<sup>`n`</sup>`)` | Exponential         |
| `O(n!)`                | Factorial           |
| `O(x)`                 | Infinite            |
