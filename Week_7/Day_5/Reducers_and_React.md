# Reducers and React

## Reducers

* The term *reduce* describes the process of **taking multiple values and processing them one by one to create a single value**

* Review `Array.prototype.reduce` function - [MDN doc](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

## Basic `.reduce()` Syntax:

```javascript
arr.reduce(callback( accumulator, currentValue, [, index[, array]] )[, initialValue])
```

`.reduce()` Parameters:
* `callback` - function to run on each element in array

  * Except for the first element, If no `initialValue` is supplied (see `initialValue` section)
  * Takes 4 arguments:
    1. `accumulator` - accumlates the callback's return values, starts with `initialValue`
    2. `currentValue` - current element being processed in the array
    3. `index` (optional) - index of current element being processed in the array
      * If `initialValue` is provided: starts from index `0`
      * If NO `initialValue` provided: starts from index `1`
    4. `array` (optional) - source array the `reduce()` was called upon

* `initialValue` (optional) - value to use as the first argument to the reducer callback function
  * If no value given, first element in the array will be used as the initial `accumulator` value and skipped as `currentValue`
  * If no value given AND array is empty, `TypeError` will be thrown.


```javascript
const values = [3, 5, 7];

const result = values.reduce((accumulator, value) => accumulator + value, 0);

console.log(result); // 15
```

## Application Reducers

* Redux library - https://redux.js.org

* `useReducer` Hook in React - alternative to `useState` Hook (preferred when mangaging more complex state logic)

* `dispatch` - an **action** that describes the change we want to make when we want to alter the state with a *reducer*
  * use *reducer* to handle action and replce current state => leads to re-render of page with updated view

Example
```jsx
function reducer(state, action) {
  if (action.type === "add") {
    return state + action.value;
  }

  if (action.type === "subtract") {
    return state - action.value;
  }

  if (action.type === "multiply") {
    return state * action.value;
  }

  return state;
}

function BoringCalculator() {
  /* Pass a reducer and an initial state */
  const [state, dispatch] = useReducer(reducer, 0);

  /* These functions dispatch actions described as obejcts */
  function add3() {
    dispatch({ type: "add", value: 3 });
  }

  function subtract5() {
    dispatch({ type: "subtract", value: 5 });
  }

  function add7() {
    dispatch({ type: "add", value: 7 });
  }

  function multiply11() {
    dispatch({ type: "multiply", value: 11 });
  }

  /* Attach the actions to the buttons and render the state */
  return (
    <div className="calculator">
      <div className="result">{state}</div>
      <button className="add" onClick={add3}>
        Add 3
      </button>
      <button className="subtract" onClick={subtract5}>
        Subtract 5
      </button>
      <button className="add" onClick={add7}>
        Add 7
      </button>
      <button className="multiply" onClick={multiply11}>
        Multiply 11
      </button>
    </div>
  );
}
```

Example: writing `dispatch` actions in-line with components (harder to read)
```jsx
function reducer(state, action) {
  if (action.type === "add") {
    return state + action.value;
  }

  if (action.type === "subtract") {
    return state - action.value;
  }

  if (action.type === "multiply") {
    return state * action.value;
  }

  return state;
}

function BoringCalculator() {
  const [state, dispatch] = useReducer(reducer, 0);

  return (
    <div>
      <button onClick={() => dispatch({ type: "add", value: 3 })}>Add 3</button>
      <button onClick={() => dispatch({ type: "subtract", value: 5 })}> Subtract 5</button>
      <button onClick={() => dispatch({ type: "add", value: 7 })}>Add 7</button>
      <h2>{state}</h2>
    </div>
  );
}
```