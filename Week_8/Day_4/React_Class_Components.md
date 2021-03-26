# Class Components

## Classes

* With introduction of ES6, React replaced the usage of custom `React.createClass` function with the new Class syntax

* Additional rules apply when we try to declare a React component with an ES6 class

> Reacht class rules
> 1. All class-based React components must `extend` the `React.Component` class
> 2. All class-based React components must override the `render` method of the `React.Component` superclass that they `extend`

Using class API:
```jsx
import React, { Component } from "react";

// Note: imported Component by its name, else can also be written as...

// class Application extends React.Component

class Application extends Component {
 render() {
  return <div></div>;
 }
} 
```

Same component as function:
```jsx
import React, { Component } from "react";

function Application(props) {
  return <div></div>;
}
```

## Constructors
* Not required to override the construtor method, but IF we do:
  * Must call the `super()` method, and 
  * Pass it to the `props` object

> TL;DR: A constructor must call the `super(props)` method.

```jsx
import React, { Component } from "react";

class Application extends Component {
 constructor(props) {
  /* If we add a constructor to our class, we must pass props to the super class */
  super(props);
 }

 render() {
  return <div></div>;
 }
}
```

## Component Instances

* Create a component = Creating a new instance of the class

* The `React.Component` class has common methods and properties that our components inherit:
  * `this.props`
  * `this.state`
  * `this.setState`

```jsx
class Counter extends Component {
 render() {
  return <button onClick={this.props.onClick}>{this.props.count}</button>;
 }
}

class Application extends Component {
 state = {
  count: 0
 };

 increment = event => {
  this.setState(previousState => ({
   count: previousState.count + 1
  }));
 };

 render() {
  return <Counter onClick={this.increment} count={this.state.count} />;
 }
}
```

## Guidelines for Setting State

### 1. Never set state directly: use `setState` instead

**Bad**
```javascript
show = event => {
  this.state = {
    visible: true
  }
};
```

**Good**
```javascript
show = event => {
  this.setState({
    visible: true
  });
}
```

### 2. State updates are merged

Example: Only the value of `visible` is changed, the value of `this.state.unchanged` will remain unaffected and available in `render` method

With Hooks would have to use `setState({...state, show: visible})` to retain the unchanged state.

```javascript
class App extends React.Component {
  state = {
    unchanged: true,
    visible: false
  };

  show = event => {
    this.setState({
      visible: true
    });
  };

  render() {
    return (
      <button onClick={this.show}>
        {this.state.unchanged ? "Unchanged" : "Changed"}{" "}
        {this.state.visible ? "Visible" : "Hidden"}
      </button>
    );
  }
}
```

### 3. State updates are asynchronous

```javascript
 state = {
    visible: false
  };

  show = event => {
    this.setState({
      visible: true
    });

    console.log(this.state.visible); // still false
  };
```

Must use the *second form* of `setState` if our new state depends on our old state:
  * Pass function to `this.setState` using `prev` parameter
  * Function return a new object with deired changes to `this.state`

```javascript
increment = event => {
 this.setState(previousState => ({
  count: previousState.count + 1
 }));
};
```

## Lifecycle (Intro)

* React predefines the available lifecycle methods and calls them during the life of a component

* Lifecycles methods = API we use to perform side effects (eg. data fetching, connecting to WebSocket) in class-based components


## Binding `this`

Medium article: [read this](https://medium.com/free-code-camp/react-binding-patterns-5-approaches-for-handling-this-92c651b5af56)