# DOM Events

## Javascript Event Listening

### Adding Listeners
Use `.addEventListener()` method

```javascript
element.addEventListener(<event-name>, <callback>, <use-capture>);
```
* `event-name` (string): The name or type of event to listen to, can be any standard DOM events (`click`, `mousedown`, `touchstart`, etc.) or custom events

* `callback` (function): The cb func that gets called when the event happens. The `event` object, containing data about the event, is passed as the first argument

* `user-capture` (boolean): Declares whether the callback should be fired in the 'capture' phase

#### Example: adding a click event for a pop-up
```javascript
var element = document.getElementById('element');

function callback() {
  alert('Hello');
}

// Add listener
element.addEventListener('click', callback);
```

### Removing Listeners
Use `.removeEventListener()` method (*Must* have a reference to the original bound cb func, else won't work. This means *named* instead of anonymous functions.)

```javascript
element.removeEventListener(<event-name>, <callback>, <use-capture>);
```

#### Example: removing future click events after button is clicked once
```javascript
var element = document.getElementById('element');

function callback() {
  alert('Hello once');
  element.removeEventListener('click', callback);
}

// Add listener
element.addEventListener('click', callback);
```

### Maintaining Callback Context

Example - context of `user` not passed to the event, called in the context of `element` instead, therefore undefined: 
```javascript
var element = document.getElementById('element');

var user = {
 firstname: 'Wilson',
 greeting: function(){
   alert('My name is ' + this.firstname);
 }
};

// Attach user.greeting as a callback
element.addEventListener('click', user.greeting);

// alert => 'My name is undefined'
```

#### Solution 1: Anonymous Function
```javascript
element.addEventListener('click', function() {
  user.greeting();
  // alert => 'My name is Wilson'
});
```

* Can fix by using an anonymous function inside the right context

* But remember anonymous function can't be used with `.removeEventListener()`

#### Solutino 2: `.bind()` Method
```javascript
// Overwrite the original function with
// one bound to the context of 'user'
user.greeting = user.greeting.bind(user);

// Attach the bound user.greeting as a callback
button.addEventListener('click', user.greeting);
```
* Generate a new function (`bound`) that will always run in the given context, then pass it as a callback to `.addEventListener()`

* This also gives a reference to the callback, which we can use to unbind the listener if needed

```javascript
button.removeEventListener('click', user.greeting);
```

---

## The Event Object

* `event` object is created when the event first happens and it travels with the evenet through the DOM

### Event Info from `event` Object:

#### Event Meta
* `type` (string) - name of the event
* `target` (node) - DOM node where the event originated
* `currentTarget` (node) - DOM node the event cb is currently firing on
* `eventPhase` (number) - current phase event is in:
  * `0` = none
  * `1` = capture
  * `2` = target
  * `3` = bubbling
* `timestamp` (number) - date on which the event occurred
* `isTrusted` (boolean) - an event is 'trusted' when it originates from the device itself, and not synthesized from within JS

#### Bubbling & Capturing
* `bubbles` (boolean) - whether this is a 'bubbling' event
* `stopPropagation` (function) - prevents callbacks from being fired on any nodes further along the event chain (does NOT prevent addtional cb of same event from running on the current node though)
* `stopImmediatePropagation` (function) - prevents any cb from being fired on any nodes further  along  the event chain, *including* additional cb of same event on the current node

#### Default Behaviour
* `preventDefault` (function) - prevents default event behaviour from occuring (e.g when we don't want window to refresh when we click a link)
  ```javascript
  anchor.addEventListener('click', function(event) {
    event.preventDefault();
    // Do our own thing
  });
  ```
* `concelable` (boolean) - whether the default behaviour of the event can be prevented by calling the `event.preventDefault` method
* `defaultPrevented` (boolean) - whether the `preventDefault` method has been called on the event object

---

## Event Phases

### Capture Phase
* set third argument of `addEventListener` to `true` to listen to capture phase

* rarely used, but can potentially prevent any clicks from firing in ertain element if the event is handled in the capture phase

```javascript
let form = document.querySelector('form');

form.addEventListener('click', function(event) {
  event.stopPropagation();
}, true); // Note: 'true'
```
### Target Phase
* when an event reaches the target

* event fires on the target node, before reversing and retracing its steps, propagating back to the outermost doc lvl

* Eg: if listening for a `click` event on a `<div>` element, and user actually clicks on a `<p>` element in the `<div>`:
  * `<p>` = event target
  * `<div>` - can listen for clicks still because the event will bubble

### Bubbling Phase
* after event has fired on target, it bubbles up through the DOM until it reaches the doc's root (`window`)

* Useful by removing the need to listen for an event on the *exact* element it came from - we can listen on an element further up on the DOM tree, and let the event reach us instead

## Custom DOM Events

It's possible to create our own custom events and dispatch them on any element in the document like a regular DOM events.

```javascript
var myEvent = new CustomEvent("myevent", {
  detail: {
    name: "Wilson"
  },
  bubbles: true,
  cancelable: false
});

// Listen for 'myevent' on an element
myElement.addEventListener('myevent', function(event) {
  alert('Hello ' + event.detail.name);
});

// Trigger the 'myevent'
myElement.dispatchEvent(myEvent);
```

## Event Delegation with jQuery
* Listen for events using parent element and then identifying the children element after

Example: listening on parent `<ul>` for event in `<li>`
```javascript
// Not using event delegation
$('li').on('click', function(){});

// Using event delegation
$('ul').on('click', 'li', function(){});
```

## Exercises
*Notice how `event` object is passed as parameter to anonynous cb*

### Capturing event coordinates
```javascript
document.addEventListener("dblclick", (event) => {
    let x = event.clientX;
    let y = event.clientY;
    let coords = `X coords: ${x} and Y coords: ${y}`;
    console.log(coords);
})
```