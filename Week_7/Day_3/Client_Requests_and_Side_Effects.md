# Client Request and Handling Side Effects

## Request as a Side Effect

> When we make requests to an API server, it is considered as a **side effect** of rendering a component.

We manage them with the `useEffect` Hook provided by the React lib

Sequence of operation when user type in search terms
  1. We make the API request
  2. We store retrieved data as state (if previously has a result already, replace the `result` state)
  3. React renders the component

```jsx
function LiveSearch(props) {
  const [term, setTerm] = useState("");
  const [results, setResults] = useState([]);

  return (
    <>
      <SearchBar value={term} onChange={setTerm} />
      <Results results={results} />
    </>
  );
}
```

The request depends on the value of `term` changing, causing the render to occur again. The request is a **side effect** of the `LiveSearch` component function being called by React.

> **Side effect** in computer science is when an operation, function, or expression modifies some state variable value(s) outside its local environment - has an observable effect besides returning a value (the main effect).

Side effects:
  * API calls
  * updates to DOM
  * event listeners, etc.

## React.useEffect

Reading List:

* A Complete Guide to useEffect:
  * https://overreacted.io/a-complete-guide-to-useeffect/

* How to fetch data with React Hooks?:
  * https://www.robinwieruch.de/react-hooks-fetch-data

What is it?

* named export from React
* import by typing `import React, { useEffect } from 'react';`
* allows us to safely manage side effects within component function calls
* React calls the function inside a component's `useEffect` method after render, making adjustment to the DOM after the render has happened

## The Rules of Hooks

### Rule #1
**Don't call Hooks inside loops, conditions, or nested functions.**

Wrong usage:
```jsx
if (results.length > 0) {
  useEffect(() => console.log("Results Set"));
}
```

Correct usage:
```jsx
useEffect(() => {
  if(results.length > 0) {
    console.log("Results Set");
  }
});
```
Need to put the condition **INSIDE** the effect method. (Same thing with `useState` calls, can't put them inside a condition either)

### Rule #2
**Only call Hooks from inside React components.**

Can also call Hooks from w/i custom Hooks, but custom Hooks must also only be called directly by a component.

### Rule #3
**The effect method that we pass to `useEffect` must either return undefined or a function.**

Function will be used for side effect clean up.

*Pro-tip*: Avoid this issue by always declaring your effect as a multiline function

## Dependencies

* Effects are usually dependent on state and props

* We must declare those dependencies in the list

```jsx
useEffect(() => {
  if(results.length > 0) {
    console.log("Results Set");
  }
}, [results]); // Only re-run the effect if results changes
```

Previous example: 
* Don't want to run effect after each render, only run when the `result` changes

* Tell React to skip applying effect if certain values haven't changed between re-renders => pass an array as optional second argument to `useEffect`

## Questions to think about
* Q1: When should we request the data?
  * Request the data when the `term` changes (referring to first example)

* Q2: Where should we store the retrieved data?
  * Store results as state

* Q3: What changes cause us to make the request again?
  * In some cases, we only want to make the request once when we load the app
  * In other cases, we will make the request again when specific state has changed

## Requests

Data fetching pattern steps:
1. Componenet has no `results` when React renders it the first time
2. Component makes async request to API server
3. Data for component is returned in response
4. Component can now be udpated with retrieved data using an action that sets the state

```jsx
function LiveSearch(props) {
  const [term, setTerm] = useState("");
  const [results, setResults] = useState([]);

  useEffect(() => {
    fetch(`/search?term=${term}`).then(setResults);
  }, [term]);

  return (
    <>
      <SearchBar value={term} onChange={setTerm} />
      <Results results={results} />
    </>
  );
}
```

* Request the data **after** the initial render
* When `term` change => component will re-render => effect also run
* Declare effect dependecy: request depends on value of `term`
* Calling `setResults` will update the component and render with the latest results

## Classes

Functions based on class-based component and represent **lifecycle** events
* `componentDidMount`
  - make initial request to function
* `componentDidUpdate`
  - function is called when component updates
  - within function, would check to see if `term` has changed
  - if `term` has changed, would make the API request
* `componentWillUnmount`

