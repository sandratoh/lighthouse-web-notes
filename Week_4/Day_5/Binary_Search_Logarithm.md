# Binary Search and Logarithm

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

### Logarithm

> *log<sub>2</sub>n = x* equals *n = 2<sup>x</sup>*

* [Review logarithm here](https://www.khanacademy.org/math/algebra2/exponential-and-logarithmic-functions/introduction-to-logarithms/v/logarithms)

* Inverse of exponential: logarithm function grows very slowly

### Example: Binary search with *n* to power of 2

* If *n* is 128, binary search will require at most (log<sub>2</sub>128 + 1) guesses.

* Calculation: 
  * log<sub>2</sub>128 = 7 because 2<sup>7</sup> = 128
  * 7 + 1 = 8

* Result: at most **8 guesses** for an array of 128 length

### Example: Binary search with *n* **not** being a power of 2

* What to do? => Look at the closest lower power of 2!

* If *n* is 1000, the closest lower power of 2 is 512 = 2<sup>9</sup>

* Estimate: 
  * log<sub>2</sub>1000 will be greater than 9 and less than 10 (calculator shows it's about 9.97)

  * round down if decimal number (9), then +1 = 10

* Result: at most **10 guesses** for an array of 1000 length