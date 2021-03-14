# React & JavaScript

## Closures

#### Lexical Scoping

* *lexical scoping* - describes how a parser reolves variable names when functions are nested

* *lexical* - refers to the location where a varaible is declared within the source code to determine where that variable is available

* Nested functions have access to variables declared in their outer scope

#### Closures

* Functions in JS form *closures* - combination of a function and the lexical environment within which that function was declared

* Example
  ```javascript
  function makeAdder(x) {
    return function(y) {
      return x + y;
    };
  }

  var add5 = makeAdder(5); // lexical env: x = 5
  var add10 = makeAdder(10); // lexical env: x = 10

  console.log(add5(2));  // 7
  console.log(add10(2)); // 12
  ```
  * `add5` and `add10` are both closures - they share the same function body definition, but store diff lexical environments

* Allows you to associate data (the lexical environment) with a function that operates on that data

* Like object-oriented programming, associating data (object's properties) with methods

* Can use closures anywhere you would use object with a single 'method'

#### Private Methods with Closures

* Private methods - methods that can only be called by other methods in the same class
  * Restrict access to code
  * Manage global namespace

* Use closures to emulate private methods in JS

* Create a shared lexical environment in the body of an anonymous function

```javascript
var makeCounter = function() {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function() {
      changeBy(1);
    },

    decrement: function() {
      changeBy(-1);
    },

    value: function() {
      return privateCounter;
    }
  }
};

var counter1 = makeCounter();
var counter2 = makeCounter();

alert(counter1.value());  // 0.

counter1.increment();
counter1.increment();
alert(counter1.value()); // 2.

counter1.decrement();
alert(counter1.value()); // 1.
alert(counter2.value()); // 0.
```
Note how the two counters maintain independence from one another

#### Closure Scope Chain

Every closure has three scopes:
* Local scope (own scope)
* Outer functions scope
* Global scope

## Functions
* Function declarations can be 'hoisted', but expressions cannot

* Arrow functions are also expressions

* Arrow functions do NOT create own scope in JS, which also  means they don't create own context for `this`

> The context of `this` inside an arrow function is the same as the `this` on the outside

## Computed Property Names

* Can put an expression inside square brackets `[]`, expression inside gets computered and used as an object's property name

Not using computer property names
```javascript
var STATUS_SUCCESS = "STATUS_SUCCESS";
var STATUS_FAILURE = "STATUS_FAILURE";

var messages = {};

messages[STATUS_SUCCESS] = "Updated";
messages[STATUS_FAILURE] = "Error";
```

Using computer property names
```javascript
const STATUS_SUCCESS = "STATUS_SUCCESS";
const STATUS_FAILURE = "STATUS_FAILURE";

const messages = {
  [STATUS_SUCCESS]: "Updated",
  [STATUS_FAILURE]: "Error"
};
```

## ...Spread vs ...Rest

* `...` **spread** used when creating new arrays or objects from existing arrays/objects

* `...` **rest** syntax is used on the LEFT side of `=` operation.

  * Used to destructure objects or arrays instead of building

* Examples:
  ```javascript
  const profile = { first: 'Michael', last: 'Jackson', occupation: 'developer' }
  const { occupation, ...rest } = profile
  occupation // developer
  rest // { first: 'Michael', last: 'Jackson' }
  ```

  ```javascript
  function myFunction(first, last, ...rest) {
  return rest
  // first two parameters are 'first' and 'last', rest are added to 'rest' as an array
  }

  console.log(myFunction('Michael', 'Jackson', 'Developer', 'California'))
  // output: ['Developer', 'California']
  ```

* Variable name doesn't have to be `rest`, can name it however you like => `...whatever`

## Short Circuiting with &&

* Most programming languages **short-circuit**:
  * when the expression before && is false, second expression will be skipped by program and never execute

* Reasoning: if the first expression is false, then there's no point in checking the second expression because one thing being false means the end result has to be false

```javascript
// This will cause an error if `users` is not an array
function findById(users, id) {
  return users.find(item => item.id === id)
}

// Now we are returning the person if `users` is an array
// If `users` is not an array, we the value whatever is before
// && which is `false` in that case
function findById(users, id) {
  return Array.isArray(users) && users.find(item => item.id === id)
}
```

## Optional Chaining with `?.`

* Similar to the `&&` short-circuiting operator
  * normal `.` accessor operator with an additional feature that checks for truthy value

* Example:
  1. Evalute `users` to see if it's truthy. If it isn't, return `undefined` without doing `.length`

  2. If truthy, then continue with the rest of the `.length` expression

  **Short-circuiting method**
  ```javascript
  users && users.length
  ```
  **Optional Chaining method**
  ```javascript
  users?.length
  ```


