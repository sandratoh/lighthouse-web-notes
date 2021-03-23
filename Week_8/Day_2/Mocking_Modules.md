# Mocking Modules

* Use mocking to replace functionality of entire modules

* Can wait for asynchronous changes in the interface and chain promises to create tests that resemble normal software usage

## Fixtures

* Definition: reusable static data that is imported or embedded into a test file

* Make sure you have accurate data that matches the schema from the server

* Ensure tdata is complete but not excessive

## Replacing `axios.get`

* Only need to include mock fns for the parts of the API that we are using

* Eg. If we are mocking the `axios.get()` function, we will use `jest.fn()` to create the mock
```javascript
export default {
  get: jest.fn(url => {
    if (url === "/api/days") {
      return Promise.resolve({
        status: 200,
        statusText: "OK",
        data: fixtures.days
      });
    }

    if (url === "/api/appointments") {
      /* Resolve appointments data */
    }

    if (url === "/api/interviewers") {
      /* Resolve interviewers data */
    }
  })
}
```

* In the case of error `TypeError: Cannot set property 'baseURL' of undefined`:
  * Means we're using previous configuration: `axios.defaults.baseURL = "http://localhost:8001";`
  * To solve: we have to set a default base url for `axios` to mock the configuration object

```javascript
export default {
  defaults: { baseURL: "" }, // add this line
  get: jest.fn(url => {
    if (url === "/api/days") {
      return Promise.resolve({
        status: 200,
        statusText: "OK",
        data: fixtures.days
      });
    }
```

## `waitForElement` Function

* Useful for making test asynchronous by returning a Promise

* The `waitForElement` function returns a promise that
  * resolves when the callback returns a truthy value, and
  * rejects after a time out when it cannot find the specified text

* When we return a Promise from the test function, the Jest framework knows that the test isn't complete until the promise chain has resolved or rejected

* Chaining Promise returned from `waitForElement`

```javascript
it("defaults to Monday and changes the schedule when a new day is selected", () => {
  const { getByText } = render(<Application />);

  return waitForElement(() => getByText("Monday")).then(() => {
    fireEvent.click(getByText("Tuesday"));
    expect(getByText("Leopold Silvers")).toBeInTheDocument();
  });
});
```