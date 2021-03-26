# Lifecycle and Classes

## Component Lifecycle

### Phase 1: **Mount**
Happens once when we create a component instance

* `constructor`
* `render`
* `componentDidMount`

### Phase 2: **Update**
Occurs everytime component is updated, (can update zero or more times)

* `render`
* `componentDidUpdate`

### Phase 3: **Unmount**
Final phase, happens only once

* `componentWillUnmount`

*More lifecycle methods [here](https://reactjs.org/docs/react-component.html)*


## Side Effects

## Adding Local Storage

`localStorage` synchronization: 

* Lifecycle methods usually placed at the top of class after constructor or state class properties

* Use `JSON.stringify` and `JSON.parse` to convert values

* Check local storage in `Application` tab of Chrome Dev Tools

`scheduler-dashboard Example`: Refreshing browser will load the initial state from `localStorage`
```jsx
class Dashboard extends Component {
  state = { /* do not replace your initial state */ };


  componentDidMount() {
    const focused = JSON.parse(localStorage.getItem("focused"));

    if (focused) {
      this.setState({ focused });
    }
  }

  componentDidUpdate(previousProps, previousState) {
    if (previousState.focused !== this.state.focused) {
      localStorage.setItem("focused", JSON.stringify(this.state.focused));
    }
  }

  render() { /* do not replace your render method */ }
}
```