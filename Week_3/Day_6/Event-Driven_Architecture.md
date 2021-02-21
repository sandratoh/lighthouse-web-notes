# Event-Driven Architecture (EDA)


### Intro
> When `X` happens, then do `Y`

* `X` is the event
* `Y` is the event handler

* Think asynchronous programming

### Client-Side Events
* DOM Events: `onClick`, `onFocus`, `onLoad`
* jQuery

## Server-Side Events
* Node.js: incoming request is an event, callback function handles the event (and could render a response)
* Core API in Node.js: `EventEmitter` class