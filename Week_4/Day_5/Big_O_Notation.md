# Big O Notation

The official way to determine the *efficiency* of algorithms - **Big O Notation**

Possible technical interview Q: evaluate the running time of an algorithm using Big O notation.

## Intro

* Syntax: `O()`

* Describes the scalability of an algorithm's steps relative to its input

> As we increase the amount of data, does the algorithm grow *linearly*, *exponentially*, or *logarithmically*?

* Three main things to remember when using Big O notation:
  1. Only care about arbitrarily large input
    * What does the run time look like when we give it an array of one million items?
  
  2. Drop the non-dominant terms
    * Eg: when our running time is `(n^2+n)/2`, only `n^2` matters, and we can ignore the rest

  3. Drop constant terms
    * Eg: when graphing `(n^3)/2` or `(n^3)*2`, curve is pretty much the same as `n^3`, so we can just get rid of constant `2`
  
  ## Arbitrarily Large Input

  * For small values, it doesn't really matter which one is faster or more efficient

  * Also, it's difficiult to identify the more efficient algorithm

  