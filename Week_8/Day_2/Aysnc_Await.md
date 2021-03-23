# Async/Await

## Intro

* Doesn't replace Promise, but make them easier to use

* Updated syntax from ECMAScript 2017

* Can change any raw Promise syntax to the newer async/await syntax

**Example**: `Application.test.js` from scheduler app

Using Promise:
```javascript
it("changes the schedule when a new day is selected", () => {
  const { getByText } = render(<Application />);

  return waitForElement(() => getByText("Monday")).then(() => {
    fireEvent.click(getByText("Tuesday"));

    expect(getByText("Leopold Silvers")).toBeInTheDocument();
  });
});
```

Using async/await:
```javascript
it("changes the schedule when a new day is selected", async () => {
  const { getByText } = render(<Application />);

  await waitForElement(() => getByText("Monday"));

  fireEvent.click(getByText("Tuesday"));

  expect(getByText("Leopold Silvers")).toBeInTheDocument();
});
```

Primary changes:
  1. Asynchronous function defined as one using the `async` keyword
  2. Promise chain hidden using the `await` keyword

---

## Anatomy of Async Await

```javascript
function setTimeoutPromise(error) {
  /* Wrapping a function that takes a callback with a Promise */
  return new Promise((resolve, reject) => {
    if (error) {
      /* When an error occurs we reject the Promise */
      reject("Error");
    } else {
      /* This Promise will resolve in 1000ms */
      setTimeout(() => resolve("Data"), 1000);
    }
  });
}

setTimeoutPromise(true /* or false */)
  .then(data => {
    /* Success case */
    console.log(`Promise Resolved with ${data}`);
  })
  .catch(error => {
    /* Failure case */
    console.log(`Promise Rejected with ${error}`);
  });
```

* First thing to do: create an `async` fn, then invoke it like any other fn

```javascript
/* Can only use await inside of an async function */
async function run() {}

/* We can invoke the async function like any other */
run();
```
> `await` keyword can only be used within an `async` function. Trying to use it outside will result in a `SyntaxError`

```javascript
async function run() {
  /* We want to halt execution of this function until this Promise is resolved */
  const data = await setTimeoutPromise();

  /* The resolved behaves like a return value when we use await */
  console.log(`Promise Resolved with ${data}`);
}

run();
```

* Use `try/catch` instead of `then/catch` syntax when we use `await`

* An `async` function returns a Promise that can be further chained

```javascript
async function run() {
  console.log("1. The calm before async");

  try {
    const data = await setTimeoutPromise();

    console.log(`3. Promise Resolved with ${data}`);
  } catch (error) {
    console.log(`3. Promise Rejected with ${error}`);
  }
}

/* We can invoke the async function like any other */
run().then(() => {
  console.log("4. Use Pomises at the top level");
});

/* This prints immediately after run() is called */
console.log("2. Careful, this prints before the timeout is complete");

/*
1. The calm before async
2. Careful, this prints before completing the timeout
3. Promise Resolved with Resolved Data
4. Use Promises at the top level
*/
```