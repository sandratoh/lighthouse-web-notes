# `setTimeout` Introduction

One of the simplestest and easiest way to learn about asyn programming in JS is `setTimeout`!

## setTimeout
* used to delay the execution of some code to later
* specify the code via a *callback* and the delay in *ms*

To simplify our understanding, think of the function as `setTimeout(callback, delay)`

> Note: the `setTimeout` function can actually take in more parameters, and isn't limited to just two. But this simplified view is acceptable for our purpose of understanding how asyn program works.

Example

```javascript
console.log('first line');
setTimeout(() => {
  console.log('timeout line');
}, 1000);
console.log('last line');
```

Console Output
```bash
first line
last line
timeout line
```

Note how the timeout line will appear last, after approx a one second delay.

## What's It Used For?
Almost all web app (websites) like to schedule something to occur a bit later on their webpages(s) and so they use `setTimeout`

* Showing a notice and hiding it from users after a few sec
* Email clients that try to reconnect after x second of being disconnected
* Disable Adblock prompts on websites after being on them for a few second