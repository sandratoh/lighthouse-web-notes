# Intro to jQuery

## What is jQuery?
* jQuery core library created in 2006 by John Resig, and it is widely used across the Internet

* Provides conveniences when working with DOM, events, and many more

### Why does it exist? 
* Reason 1: Fixes browser compatibility issues
* Reason 2: Cleaner API

## Event Listening using jQuery

* As of jQuery 1.7, all events are bound via the `on` method, even if you call `bind` or `click`, they will act as alias of `on` and are mapped to the `on` method internally

> Use `on` method for faster and more consistent code.

```javascript
// The many ways to bind events with jQuery
// Attach an event handler directly to the button using jQuery's
// shorthand `click` method.
$( "#helloBtn" ).click(function( event ) {
    alert( "Hello." );
});
 
// Attach an event handler directly to the button using jQuery's
// `bind` method, passing it an event string of `click`
$( "#helloBtn" ).bind( "click", function( event ) {
    alert( "Hello." );
});
 
// As of jQuery 1.7, attach an event handler directly to the button
// using jQuery's `on` method.
$( "#helloBtn" ).on( "click", function( event ) {
    alert( "Hello." );
});
 
// As of jQuery 1.7, attach an event handler to the `body` element that
// is listening for clicks, and will respond whenever *any* button is
// clicked on the page.
$( "body" ).on({
    click: function( event ) {
        alert( "Hello." );
    }
}, "button" );
 
// An alternative to the previous example, using slightly different syntax.
$( "body" ).on( "click", "button", function( event ) {
    alert( "Hello." );
});
```

* Final two examples are examples of **event delegation** - an element higher in the DOM tree listens for events occuring on its children (works b/c of *event bubbling*!)

## Event Delegation

* Pros of event delegation over binding directly to element(s)
    * better performance and memory management
    * event bubbling

* (E.g) Binding events to 1 table over 1000 table cells, the latter will be a nightmare...

## The `event` object

```javascript
// Binding a named function
function sayHello( event ) {
    alert( "Hello." );
}
 
$( "#helloBtn" ).on( "click", sayHello );
```

* We can also bind named functions to our `on` method to help keep our codes DRY

* `event` argument in the `sayHello` function contains info about the event
    * when and where the event occurred
    * what type of event
    * which element the event occurred on
    * etc.

* Use event object's `.preventDefault()` method to cancel an element's default action (e.g clicking on a button to submit a form)

* Use event object's `.stopPropagation()` method to stop bubbling, so parent elements aren't notified of event occurrence

* When using both `.preventDefault()` and `.stopPropagation()` at the same time, can also refactor and use `return false`, but do it only if both are actually necessary

```javascript
// Preventing a default action from occurring and stopping the event bubbling
$( "form" ).on( "submit", function( event ) {
 
    // Prevent the form's default submission.
    event.preventDefault();
 
    // Prevent event from bubbling up DOM tree, prohibiting delegation
    event.stopPropagation();
 
    // Make an AJAX request to submit the form data
});
```

* `event.originalEvent` - the event object the broser created, useful for touch events on mobile devices and tablets

* Can `console.log` the event (including `originalEvent`) to browser's console which helps when debugging

```javascript
// Logging an event's information
$( "form" ).on( "submit", function( event ) {
 
    // Prevent the form's default submission.
    event.preventDefault();
 
    // Log the event object for inspectin'
    console.log( event );
 
    // Make an AJAX request to submit the form data
});
```