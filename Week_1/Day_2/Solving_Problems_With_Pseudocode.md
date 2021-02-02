# Solving Problems With Pseudocode

## Step 1: Understand the Problem
* What is the input  to  the problem?
  * Know the types of input you are dealing with and how to handle them
* What is the expected output of the program?
  * Helps you recognize patterns that can be generalized into a solution
  * Gives a sample output that you can use later to verify you codes against

--

## Step 2: Try Writing a Pseudocode First
* Before you start writing codes, describe in words what the solution you're going to implement.
  * Often in **pseudocode** (or 'almost' code)
* Separate from *what* you want to *how* you want to do it
* Break down your steps, and add in more pseudocode along your thought process
* Example - Loopy Lighthouse
  * Starting psuedocode
    ```
    Loop from 100 to 200:
      Let num = the current step in the loop
      Print num
    End loop
    ```
  * Ending psuedocode
    ```
      Loop from 100 to 200:
    Let num = the current step in the loop
    If num % 3 is equal to 0:
      Print "Loopy"
    Else if num % 4 is equal to 0:
      Print "Lighthouse"
    Else if num % 3 is equal to 0 and num % 4 is equal to 0:
      Print "LoopyLighthouse"
    Otherwise
      Print num
    End if
    End loop
    ```
--
## Step 3: Simulate Program Execution
* Go through your pseudocode line by line, and review simulated output.
* Adjust pseudocode if simulated output is different from expected output (from Step 1).
* Example - Loopy Lighthouse
  * Adjust conditions order so correct conditions are run/skipped
    ```
      Loop from 100 to 200:
    Let num = the current step in the loop
    If num % 3 is equal to 0 and num % 4 is equal to 0:
      Print "LoopyLighthouse"
    Else if num % 3 is equal to 0:
      Print "Loopy"
    Else if num % 4 is equal to 0:
      Print "Lighthouse"
    Otherwise
      Print num
    End if
    End loop
  ```

--
## Step 4: Translate Solution to JavaScript
* Use pseudocode as skeleton for your JavaScript codes and convert using correct syntax
* Last but not least: *test the codes*!

--

## Step 5: Refactor Your Codes
* Improve performance, readability, or code re-use by refactoring your codes
* Start with the basic: finding patterns and minimizing duplicate code
* Remember not to sacrifice code readability over length