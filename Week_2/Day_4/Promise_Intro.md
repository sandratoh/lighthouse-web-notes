# Promises Intro

## Official Technical Definition

> * A promise represents the eventual result of an asynchronous operation. 
>  * Primarily uses `then` method to interact with a promise
> * Then use callbacks to receive either a promise's eventual value (the result if promise is fulfilled) or the reason why the promise cannot be fulfilled (the error if promise is rejected)

**TL;DR**: avoid callback hell by wrapping callbacks into a promise.

* A promise is an object
* They don't rely on anything other than basic JS
* As of ES6, promises are built into the language (via `Promise`)


## Benefits of Promises
* We can chain promises, which turn nested callbacks from doing async tasks into manageable/readable control flow

* Error handling becomes much simpler

* Easier to unit test async codes

* `Promise.all` can be used to run multiple async operations in parallel and have a single calback to see all the result together