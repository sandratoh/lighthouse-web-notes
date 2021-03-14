## Throttling and Debouncing

### Throttled Function
* Function is called at most once in a specified time period
  
* Prevent a function from running if it has run 'recently'

* Ensure a function is run regularly at a fixed rate

* Common use: gaming

#### Basic throttle function & implementation
  ```javascript
  // regular call to function handleEvent
  element.on('event', handleEvent);
  // throttle handleEvent so it gets called only once every 2 seconds (2000 ms)
  element.on('event', throttle(handleEvent, 2000));
  ```

### Debounced Function
* Ignore all calls to a function until the calls have stopped for a specified time period, only then will the function be called

* Common use: autocomplete

* Basic debounce function/implementation
  ```javascript
  // regular call to function handleEvent
  element.on('event', handleEvent);
  // debounce handleEvent so it gets called after calls have stopped for 2 seconds (2000 ms)
  element.on('event', debounce(handleEvent, 2000));
  ```