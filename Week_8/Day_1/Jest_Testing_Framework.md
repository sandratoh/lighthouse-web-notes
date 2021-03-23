# Jest Testing Framework

## Setup and Teardown

Functions that allow us to run code at certain points of executing a test suite.

1. `beforeAll(fn, timeout)`
2. `beforeEach(fn, timeout)`
3. `afterEach(fn, timeout)`
4. `afterAll(fn, timeout)`

Other global methods and objects that don't need to import or require to use them: [read more here](https://jestjs.io/docs/api)

## `prop-types` Library

> TypeScript and Flow enable static type checking. The `prop-types` library provides runtime validation.

What is it?
* An [optional library](https://www.npmjs.com/package/prop-types) maintained by the React team that we can use to validate component props

* Must install separately

## Testing Matchers

Default Jest testing matchers: [read documentation here](https://jestjs.io/docs/expect)

Common matchers:
* `toBe`
* `toHaveLength`
* `toHaveProperty`
* `toBeGreaterThan`
* `toContain`

### jest-dom Library

* `jest-dom` lib gives DOM specific matchers: [read documentation here](https://github.com/testing-library/jest-dom)
* Example: `toHaveClass`, `toHaveValue`

## Mock Functions

* replaces real functions during testing
  * (scheduler eg. use mock fn to return fake static data for `axio.get()`)
  * remove dependency on HTTP request library

* AKA *'spies'* - allows us to spy on the behaviour of a fn that other code calls during the test

* Passing the mock function to a component would allow us to verify that our component call the actions in the way we expected

* Create a basic mock by calling the `jest.fn()` function

### Example

Check how many times a function been called
```javascript
it("doesn't call the function", () => {
  const fn = jest.fn();
  expect(fn).toHaveBeenCalledTimes(0);
});

it("calls the function", () => {
 const fn = jest.fn();
 fn();
 expect(fn).toHaveBeenCalledTimes(1);
});
```
Check function is called with correct argument
```javascript
it("calls the function with specific arguments", () => {
 const fn = jest.fn();
 fn(10);
 expect(fn).toHaveBeenCalledWith(10);
});
```

Check function return value
```javascript
it("uses the mock implementation", () => {
 const fn = jest.fn((a, b) => 42);
 fn(1, 2);
 expect(fn).toHaveReturnedWith(42);
});
```

## Coverage Report

6 Columns:
1. `File` contains the project files labelled by file/directory name
2. Code `statements` covered during testing
3. Code `branches` covered during testing - eg: `if ... else` are two separate branches
4. `Functions` called during testing
5. `Lines` of code executed during testing
6. Untested line numbers