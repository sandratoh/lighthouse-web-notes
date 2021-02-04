# JavaScript Functions As Objects

## In Javascript, functions are **first-class objects**

#### What it means:
1. Functions can be stored in variables and passed around
2. Functions can do everything that other objects can do (i.e having properties assigned to them)

## Callback Functions

#### A call back function is:
* a function passed (by reference) into another function (the *'receiver'* function)

#### Interaction between receiver func and callback func:
* *Receiver* function accept behaviours to perform by calling the *callback* function
* *Receiver* function can call the *callback* function anytime and as many times as it wants

#### Example
```javascript
// The second argument/parameter is expected to be a (callback) function
const findWaldo = function(names, found) {
  for (let i = 0; i < names.length; i++) {
    let name = names[i];
    if (name === "Waldo") {
      found();   // execute callback
    }
  }
}

const actionWhenFound = function() {
  console.log("Found him!");
}

findWaldo(["Alice", "Bob", "Waldo", "Winston"], actionWhenFound);
```
In the example, the function `actionWhenFound` is the *callback* function. It is first defined, then passed as an argument to another function `findWaldo`. `findWaldo` then becomes the *receiver* function of this callback.