# Data Fetching with Axios

## Intro

What is it?
* A modern library for data fetching - limited to making HTTP requests
* Allows us to use Promises to handle async requests
* Can use it with any of the popular view libraries available - Angular, Vue, React


## Usage

Install using:
```bash
npm install axios
```
Four most common methods:
  * `axios.get(url[, config])`
  * `axios.post(url[, config])`
  * `axios.put(url[, config])`
  * `axios.delete(url[, config])`

## `GET` request
* Provide string url as argument in `GET` request

* `axios` lib returns a `response` object when Promise resolves

```javascript
axios.get("/api/appointments").then((response) => {
  console.log(response);
});
```

## `POST` / `PUT` request
* Provide string url and *second argument* in request when sending data to server

* Example provides object containing data to update as second argument

```javascript
axios
  .put(`/api/appointments/2`, {
    id: 2,
    time: "1pm",
    interview: {
      student: "Archie Cohen",
      interviewer: 9,
    },
  })
  .then((response) => {
    console.log(response);
  });
```

## Errors
* Use Promise `catch` method to handle errors sent by API server.

* `error` argument in `catch` methods include the `status` code

* Pattern allows us to handle HTTP requests

```javascript
axios
  .get("/api/appointments")
  .then((response) => {
    console.log(response);
  })
  .catch((error) => {
    console.log(error.response.status);
    console.log(error.response.headers);
    console.log(error.response.data);
  });
```

## Other Advanced Features
* Cancel an in-progress request

* Set timeout for a response

* Supports [CSRF](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.md) protection