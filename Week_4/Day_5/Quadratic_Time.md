## Problem

- Comparing results from adding two numbers from a list of `n` numbers

## Quadratic Time

- Method: Take the first number and add to every other number in the list, then comparing results (ignore repeated additions)

- Number of comparisons have to do = `(n^2 + n) / 2`

- If we double the `n`, number of comparison will quadruple because of exponential

## Linear Time

- Method:

  1. Compare the smallest and largest number together
  2. If result is the one you're looking for, stop
  3. If result is larger, go back to step 1 with 2nd largest number
  4. If result is smaller, go back to step 1 with second smallest number

- Number of comparison have to do = `n`

- If we double `n`, number of comparison will only double, therefore complexity scales **linearly** in comparison to input
