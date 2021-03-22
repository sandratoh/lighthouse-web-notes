# Difference Patterns with Writing Reducers

## Switch/Case

* Allows us to define common blocks of code for multiple conditions

* Things to watch out for:
  * `break` keyword - missing a keyword could continue switch statement without throwing an error

  * curly brackets `{}` - not mandatory to use them in switch statements, but they are needed to declare block-scoped variables => forgetting to use them may mess up your variables

```javascript
function reducer(state, action) {
  switch (action.type) {
    case "add": {
      return state + action.value;
    }

    case "subtract": {
      return state - action.value;
    }

    default: {
      return state;
    }
  }
}
```

## Object Lookup

* Allows data to be represented as key value pairs - graet for conditional executions

* Benefit over Switch/Case - according to [this article](https://enmascript.com/articles/2018/10/22/why-I-prefer-objects-over-switch-statements):
  1. More strutured
  2. Scales better
  3. Easier to maintain
  4. Easier to test
  4. Safer - has less side effects and risk

* Things to consider when using this pattern:
  * Will be taking some temporal space in memory to store object
  * Could be less fast than switch statements when we don't have many cases to evaluate because...
    * With object lookup: we creat a data and then accessing the key
    * With switch statements: just checking values and returning

```javascript
const reducers = {
  add(state, action) {
    return state + action.value;
  },
  subtract(state, action) {
    return state - action.value;
  }
};

function reducer(state, action) {
  return reducers[action.type](state, action) || state;
}
```

## Using Constants

* Prevent bugs due to incorrect spelling of strings

* Get notified of `ReferenceError` if variable is misused

* Take advantage of [computed property names](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#computed_property_names)

```javascript
const ADD = "ADD";
const SUBTRACT = "SUBTRACT";

function reducer(state, action) {
  switch (action.type) {
    case ADD: {
      return state + action.value;
    }

    case SUBTRACT: {
      return state - action.value;
    }

    default: {
      return state;
    }
  }
}
```