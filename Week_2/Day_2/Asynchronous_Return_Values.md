# Asynchronous Return Value

### Synchronous functions `returns` Data
* With synchronous functions, we can simply *return* a value
* Program will read from top to bottom, and return after gathering all the data

```javascript
// data in memory
const catBreeds = {
  'Balinese': "Balinese are curious, outgoing, intelligent cats with excellent communication skills. They are known for their chatty personalities and are always eager to tell you their views on life, love, and what you’ve served them for dinner.",
  'Bombay': "The golden eyes and the shiny black coat of the Bombay is absolutely striking. Likely to bond most with one family member, the Bombay will follow you from room to room and will almost always have something to say about what you are doing, loving attention and to be carried around, often on his caregiver's shoulder."
};

// synchronous function to fetch a cat breed
const breedDetails = function(breed) {
  // can simply return it (easy peezee, butter squeezy) ...
  return catBreeds[breed];
};

// get the return value right away from the function
const bombay = breedDetails('Bombay');
console.log(bombay); //=> prints out the description for that breed
```

### Asynchronous Functions Can't `return` Data
Example with WRONG async function logic:

```javascript
// asyncBreeds.js
const fs = require('fs');

const breedDetailsFromFile = function(breed) {
  console.log('breedDetailsFromFile: Calling readFile...');
  fs.readFile(`./data/${breed}.txt`, 'utf8', (error, data) => {
    console.log("In readFile's Callback: it has the data.");
    // ISSUE: Returning from *inner* callback function, not breedDetailsFromFile.
    if (!error) return data;
  });
  // ISSUE: Attempting to return data out here will also not work.
  //        Currently not returning anything from here, so breedDetailsFromFile function returns undefined.
};

// we try to get the return value
const bombay = breedDetailsFromFile('Bombay');
console.log('Return Value: ', bombay); // => will NOT print out details, instead we will see undefined!
```

Output: 
```bash
> node asyncBreeds.js
breedDetailsFromFile: Calling readFile...
Return Value: undefined
In readFile's Callback: it has the data.
```


In example: the **Return Value** console output will NOT display the file data because our `breedDetailsFromFile` function will always return `undefined`

* In async functions, it takes in a callback and *returns undefined immediately*
* Even if it has more work to do after and executes its callback *later*, the previous function has already *finished running* and returned `undefined` before it gets the data

### Asynchronous Functions *Call Back* With Data

* Need to change `return data` to `callback(data)`. Callback will be given the data, so that function can give back the data without using `return`


Example async function after changes:

```javascript
const fs = require('fs');

const breedDetailsFromFile = function(breed, functionToRunWhenThingsAreDone) {
  console.log('breedDetailsFromFile: Calling readFile...');
  fs.readFile(`./data/${breed}.txt`, 'utf8', (error, data) => {
    // CHANGE: Pass data into callback instead of returning it directly
    console.log("In readFile's Callback: it has the data.");
    if (!error) functionToRunWhenThingsAreDone(data);
  });
};

// CHANGE 1: Moved the console.log into a new function:
const printOutCatBreed = breed => {
  console.log('Return Value: ', breed) // => print out details correctly.
};

// CHANGE 2: we're now passing two arguments into breedDetailsFromFile: breed string and a callback function
breedDetailsFromFile('Bombay', printOutCatBreed);
```
Output:
```bash
> node asyncBreeds.js
breedDetailsFromFile: Calling readFile...
In readFile's Callback: it has the data.
Return Value: The golden eyes and the shiny black coat of the Bombay is absolutely striking. Likely to bond most with one family member, the Bombay will follow you from room to room and will almost always have something to say about what you are doing, loving attention and to be carried around, often on his caregiver's shoulder.
```


## Summary

* Instead of using `return data`, async functions must use **callback functions** to pass that data back