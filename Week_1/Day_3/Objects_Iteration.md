# Object Iteration Methods

## Objects and Iteration
* JavaScript *objects* `{key: value}` are *not* iterable in the way that arrays are. 
  * We need to use a `for...in` statement which loops through the properties of an object. (very similar to a `for...of` loop)

* Example
  ```javascript
  var planetMoons = {
    mercury: 0,
    venus: 0,
    earth: 1,
    mars: 2,
    jupiter: 67,
    saturn: 62,
    uranus: 27,
    neptune: 14
  };

  //traverse all the properties of the project using a for...in loop
  for (var planet in planetMoons) {
    var numberOfMoons = planetMoons[planet];
    console.log("Planet: " + planet + ", # of Moons: "+ numberOfMoons);
  };
  ```

  *What happened there?* We accessed the object using a variable, `planetMoons[planet]`. The variable `planet` iterates over each key ("mercury", "venus", ...) using the for-loop.

* Unexpected results can happen with `for...in` loops when objects inherhit properties and method names from their prototype chain.
  * Need an additional filtering step `.hasOwnProperty` when that happens
  * [Read more here](https://stackoverflow.com/questions/684672/how-do-i-loop-through-or-enumerate-a-javascript-object)

  ```javascript
  for (var planet in planetMoons) {
    // additional filter for object properties:
    if (planetMoons.hasOwnProperty(planet)) {
      //  ...
    }
  }
  ```