# Imperative vs. Declarative Programming 

> “Imperative programming is like **how** you do something, and declarative programming is more like **what** you do.”

## Real-Life Metaphors

Metaphor 1: Going to a restaurant for dinner, appraoch the front desk and say...

* **Imperative approach (HOW)**: 'I see that table located next to xyz is empty. We are going to walk over there and sit down.'

* **Declarative approach (WHAT)**: 'Table for two, please.'

Metaphor 2: Telling someone how to get to your house from Wal-Mart...

* **Imperative response**: 'Go out of the north exit of the parking lot and take a left. Get on I-15 North until you get to the 12th street exit. Take a right off the exit like you’re going to Ikea. Go straight and take a right at the first light. Continue through the next light then take your next left. My house is #298.'

* **Declareative response**: 'My address is 298 West Immutable Allery, Eden, Utah 84310'

> Many (if not all) declarative approaches have some sort of underlying imperative abstraction.

* Assumption that the declarative approaches know all the imperative steps

## JavaScript

1. Write a function called `double` which takes in an array of numbers and returns a new array after doubling every item in that array.` double([1,2,3]) // [2,4,6]`

```javascript
// imperative approach
const double = arr => {
  let results = []
  for (let i = 0; i < arr.length; i++){
    results.push(arr[i] * 2)
  }
  return results
}

// declarative approach
const double = arr => {
  return arr.map(elem => elem * 2);
}
```

2. Write a function called `add` which takes in an array and returns the result of adding up every item in the array. `add([1,2,3]) // 6`

```javascript
// imperative appraoch
const add = arr => {
  let result = 0
  for (let i = 0; i < arr.length; i++){
    result += arr[i]
  }
  return result
}

// declarative appraoch
const add = arr => {
  return arr.reduce((sum, acc) => sum + acc, 0)
}
```

3. Using jQuery (or vanilla JavaScript), add a click event handler to the element which has an `id` of `btn`. When clicked, toggle (add or remove) the `highlight` class as well as change the text to `Add Highlight` or `Remove Highlight` depending on the current state of the element.

```javascript
// imperative approach
$('#btn').click(function(event) {
  event.preventDefault;

  $(this).toggleClass('highlight');
  $(this).text() === 'Add Highlight'
    ? $(this).text('Remove Highlight')
    : $(this).text('Add Highlight')
})

// declarative approach
<Btn
  onToggleHighlight={this.handleToggleHighlight}
  highlight={this.state.highlight}>
    {this.state.buttonText}
</Btn>
```

## Other Definitions

> Declarative languages contrast with imperative languages which **specify explicit manipulation of the computer’s internal state**; or procedural languages which specify an explicit sequence of steps to follow.

> In computer science, declarative programming is a programming paradigm that expresses the logic of a computation without describing its control flow.

## React & Declarative Programming
> React is declarative which makes the code easy to read and write