# Event Propagation in DOM

## Bubbling and Capturing

*Concept*: Since DOM elements are nested within other elements (tree-like structure), events that affects a child element *bubble up* through its parents.

Can use `stopPropagation()` to prevent an event from contining its propagation.

## Bubbling

> Bubbling: when an event happens on an element, it first runs the handlers (function that specifies browser's action when an event occurs) on it, then on its parent, then all the way up on other ancestors.

Example
```html
<style>
  body * {
    margin: 10px;
    border: 1px solid blue;
  }
</style>

<form onclick="alert('form')">FORM
  <div onclick="alert('div')">DIV
    <p onclick="alert('p')">P</p>
  </div>
</form>
```

A click on the inner `<p>` will bubble upward and run the command until the `document` object: `p` --> `div` --> `form`

> *Almost* all events bubble. Some event does not bubble (i.e `focus`).

## event.target
* *target element* = the mostly deeply nested element that caused the event
    * can access it as `event.target`

* event bubbles up from `event.target` to the root, calling handlers assigned using `on<event>` HTML attributes and `addEventListener` with or without the 3rd argument (`false/{ capture:false }`)

#### Difference between `this` and `event.target`
* `event.target` - the 'target' element that initiated the event, it does NOT change through the bubbling process

* `this` - the 'current' element, the one that has a currently running handler on it (`event.currentTarget`)

* Eg: have a single handler `form.onclick`, it can 'catch' all clicks inside the form
    * `this` is the `<form>` element, b/c the handler runs on it
    * `event.target` is the actual element inside the form tha was clicked
    * it is possible that `event.target` = `this` when the click is made directly on the `<form>` element

## Stopping Bubbling
* Bubbling events goes from target element --> `<html>` --> `document` object --> `window` (some events)

* `event.stopPropagation()` - stops the move upwards, but on the current element, all other handlers will run

* `event.stopImmediatePropagation()` - stop bubbling and prevent handlers on current element from running --> stops every handlers from executing

* Don't stop bubbling without a need, could create problems

## Capturing
* Rarely used in real coding situation, but could be useful at times

* Standard 3 Phases of Event Propagation in DOM Events :
    1. Capturing phase - the event goes down to the element
    2. Target phase    - the event reached the target element
    3. Bubbling phase  - the event bubbles up from the element

* Usually invisible to us

* To catch an event on the capturing phase, need to set the handler `capture` option to `true`

* `capture` option:
    * `false`  => set on bubbling phase (default)
    * `true`   => set on capturing phase

* target phase triggers both capture and bubbling phase when event reaches the targetted element

* Example
```javascript
elem.addEventListener(..., {capture: true})
// or, just "true" is an alias to {capture: true}
elem.addEventListener(..., true)
```

* `event.eventPhase` - tells the number of the phase the event was caught on (rarely used, because we usually know it in the handler)
    * capturing = 1
    * target    = 2
    * bubbling  = 3

* To removes handler, need the same phase to correctly remove the handler (e.g `removeEventListener(..., true)` for previous example)

* Listener on same element and same phase run in the same order as they are created

```javascript
elem.addEventListener("click", e => alert(1)); // guaranteed to trigger first
elem.addEventListener("click", e => alert(2));
```