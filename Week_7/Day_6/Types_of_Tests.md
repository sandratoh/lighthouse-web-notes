# Types of Tests

## Different Categories of Tests

1. Static
2. Unit
3. Integration
4. End-to-End

From top of the list to the bottom:
* Cost increases
* Time increases
* Can handle more complex problems

## Static Testing

* Take some initial configuration, but very little maintence

* Can integrate directly to code editor for immediate feedback

* Common statc analysis:
  * linting - (Eg. ESLint, Prettier)
  * static typing - (Eg.TypeScript, Flow)

### TypeScript

* [TypeScript in 5 minutes](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html) tutorial

#### Extended primitive types in JavaScript:
* `any`     - allow anything
* `unknown` - ensure someone using this type declares what the type is
* `never`   - not possible that this type could happen
* `void`    - a function which returns `undefined` or has no return value

#### Two syntaxes for building types
* `interface`:
  * preferred
  * get better error messages
  * *open*

* `type`:
  * use when you need specific features
  * *closed* - cannot be changed outside of its declaration 

## Unit Testing

* Goal: test a specific function or component in isolation

* Focus on one small, predictable piece of code to increase our confidence that it will work as expected

## Integration Testing

* The process of proving that two or more units of code work together

* Risk of integration testing: overlapping coverage
  * Eg. if testing two units with an integration test, may not want to maintain two additional unit tests

## End-to-End Tesing

* Goal: to get as close to simulated user behaviour as possible

* Higher cost of implementation, maintenance, and runtime

* Possible to reduce maintenance cost through techniques