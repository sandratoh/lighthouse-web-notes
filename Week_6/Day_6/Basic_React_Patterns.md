# Basic React Patterns

* Passing Children with JSX
* Event Handling
* Managing State
* Controlled Components/Inputs
* Conditional Rendering
* Fragments

## Children
* Pattern: Using the children key of the props object

* Sometimes a component does not have any *children*

* When it does, the component can access them using `props.children`

```jsx
function Button(props) {
  return <button>{props.children}</button>;
}

function Application(props) {
  return (
    <main>
      <Button>Reset</Button>
    </main>
  );
}
```

## Event Handling
* Can attach event handlers to React elements and pass a reference to a function directly
```jsx
function Button(props) {
  return (
    <button onClick={(event) => console.log("Button Clicked")}>
      {props.children}
    </button>
  );
}
```

* Can also use technique below if function requries multiple expressions on multiple lines
```jsx
function Button(props) {
  function onClicked(event) {
    console.log("Button Clicked");
  };

  return <button onClick={onClicked}>{props.children}</button>;
}
```

* To make component more configurable, move the `onClick` event to `Button` component instead. 
* Need to put the `onClick` event on a `button` element using this method so something is accepting the event
```jsx
function Button(props) {
  return <button onClick={props.onClick}>{props.children}</button>;
}

function Application(props) {
  return (
    <main>
      <Button onClick={(event) => console.log("Button Clicked from Application")}>
        Reset
      </Button>
    </main>
  );
}
```

## Managing State
* State allos us to retain info across multiple render

* Use 'hooks' to store states in React

* Need to `import` the `useState` hook into the module, make sense to `import` it with `React`
  ```jsx
  import React, { useState } from 'react';
  ```

* `useState` function:
  * Parameter: receives initial state as argument
  * Output: returns an array
    * First element - the current value for the state
    * Second element - a function that can update the state and cause a render

```jsx
function Application(props) {
  const [count, setCount] = useState(0);

  return (
    <main>
      <Button onClick={(event) => setCount(count + 1)}>Increment</Button>
      <h1>Button was clicked {count} times.</h1>
    </main>
  )
}
```

> The `useState` hook uses array destructuring syntax to return two different values. The pair of values returned in the array are related. One is used to get a value and the other is used to set a value.

## Controlled Components
* Certain HTML **form** elements maintain their state
  * `<input>`
  * `<textarea>`
  * `<select>`

* *Controlled components* - form data is handled by a React component that controls the values of input elements

* *Uncontrolled components* - form data handled by the DOM

```jsx
function Application(props) {
  const [name, setName] = useState("");

  return (
    <main>
      <input
        value={name}
        onChange={(event) => setName(event.target.value)}
        placeholder="Please enter your name"
      />
      <h1>Hello, {name}.</h1>
    </main>
  );
}
```

* the `<input>` element becomes a controlled componenet when we provide a `value` prop and an `onChange` event handler that can update the value

> **TL;DR:** We use the controlled component pattern because it:
> * Allows us to choose our own way to manage state for a component - create componenet that are easier to reuse since they don't assume where state is store
> * Reduces the distinct sources of state, making our app less complex
> * Allows us to set or reset the value of an `input` field by changing the state that controls it - more declarative

## Conditional Rendering
* Using a condition to decide which React element to return

* Get familiar with the logical `&&` and ternary operator

```jsx
function Application(props) {
  const [name, setName] = useState("");

  return (
    <main>
      <input
        value={name}
        onChange={(event) => setName(event.target.value)}
        placeholder="Please enter your name"
      />
      { name && <h1>Hello, {name}.</h1> }
    </main>
  );
}
```

* Better to use ternary operator for certain situations - if rendering one of two elements based on state (i.e login/logout button based on `isLoggedIn` state)

```jsx
{ isLoggedIn ? <Logout /> : <Login /> }
```

## Fragments
* Recall that components can only return one element - also true when evaluating expressions conditionally

* Will run into SynTaxError conditionally setting a component like below example
  ```jsx
  function Application(props) {
    const [name, setName] = useState("");

    function reset() {
      setName("");
    }

    return (
      <main>
        <input
          value={name}
          onChange={(event) => setName(event.target.value)}
          placeholder="Please enter your name"
        />
        {name && (
            <h1>Hello, {name}.</h1>
            <Button onClick={reset}>Reset</Button>
        )}
      </main>
    );
  }
  ```

* Use `React.Fragment`to wrap new components

  1. Import component: `import React, { Fragment } from 'react'`

  2. Using the imported React reference: `<React.Fragment></React.Fragment>`

  3. `Fragment` shorthand: `<></>`

```jsx
function Application(props) {
  const [name, setName] = useState("");

  function reset() {
    setName("");
  }

  // Create fragment
  React.createElement(
    Fragment,
    null,
    React.createElement("h1", null, "Hello, ", name, "."),
    React.createElement(Button, { onClick: reset }, "Reset")
  );

  return (
    <main>
      <input
        value={name}
        onChange={(event) => setName(event.target.value)}
        placeholder="Please enter your name"
      />
      {name && (
        <Fragment>
          <h1>Hello, {name}.</h1>
          <Button onClick={reset}>Reset</Button>
        </Fragment>
      )}
    </main>
  );
}
```
