# Using Effects

## Syntax

```jsx
useEffect(() => {
  // content to be executed when the useEffect is in effect

  // return a way to stop the running code (cleanup function)
}, ["Variables that you want to look at and re-execute the effect when changed"])
```

## Setting State

Two ways to use `useState` Hook function

Method 1: Passing new state value directly to function
```jsx
const [likes, setLikes] = useState(0);
return <button onClick={() => setLikes(likes + 1)} />
```

Method 2: Pass previous value to get current state to function (*Use this when working with effects!*)
```jsx
const [likes, setLikes] = useState(0);
return <button onClick={() => setLikes(prev => prev + 1)} />
```

Second approach allows us to ensure each call to function will be using current state value to increment

## What is `prev`?

* Recall `useState` Hook returns an array of two output
  * Eg: `const [likes, setLikes] = useState(0)`

* The `setStates` function from `useState` Hook:
  * Can take either a value or callback that will execute => returned value from cb becomes new state
  * Has a parameter that holes the value of current state BEFORE the `setStates` function is triggered by react
    * We call this parameter `prev` by convention

> When our operations depend on previous state, we must use incorporate the `prev` parameter in our `setStates` function

# CleanUp Operations in useEffect

* Two classicifications of side effects:
  1. Require clean up: (eg. timers, event listeners, socket connections, etc.)
  2. Does not require clean up

Without cleanup phase: many timeouts running concurrently, background will flash and counts go down immediately
```jsx
useEffect(() => {
  if (likes > 0) {
    setTimeout(() => setLikes(prev => prev - 1), 1000);
  }
}, [likes]);
```


With cleanup phase: counts will go down one second after the last state change
```jsx
useEffect(() => {
  if (likes > 0) {
    const timeout = setTimeout(() => setLikes(prev => prev - 1), 1000);
    return () => clearTimeout(timeout); // clears the timer set above
  }
}, [likes]);
```

> Notice how the condition `if (likes > 0 ) {}` is inside the `useEffect` and NOT outside it because of Hook Rule #1. See [Client Request and Side Effects](/Week_7/Day_3/Client_Requests_and_Side_Effects.md)

* `return` a function from the effect method that react calls during cleanup phase
  * Eg: `clearTimeout` clears `setTimeout`
  * Eg: `clearInterval` clears `setInterval`
  * Eg: `document.removeEventListener('click', callbackFunction)` clears `document.addEventListener('click', callbackFunction)`

* React will call the clean up function before it runs the new effect

* If there is already a clean up operation running, react will clear it, and call a new one

## Infinite Render Bug

* When using `useEffect` or create any effects, we must remember to identify and declare any dependencies (second argument of `useEffect` method), otherwise, react will infinitely render
  * In the case of API calls, it will continously make the API request

* Adding a state as a dependency will ensure our `useEffect` only execute if that state changes

* To never rerun an effect, pass an **empty array** `[]` as dependency. This configuration prevents the infinite loop that we would observe without any dependencies.
