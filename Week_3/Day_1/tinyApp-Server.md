## EJS as templating engine
```javascript
const express = require("express");
const app = express();
const PORT = 8080;

// add this line below
app.set("view engine", "ejs");
```

## `res.render()` to pass data to template using `views` directory

* Use `views` directory in project to take advantage of EJS shortcut

* EJS automatically looks inside the `views` directory for any template files that have `.ejs` extension

## EJS Template Files Syntax

* Given `{ greeting: 'Hello World!' } in JS file

* Use `<%= %>` syntax to tell EJS that we want the *result* of this code to show up on page

```html
<!-- This would display the string "Hello World!" -->
<h1><%= greeting %></h1>
```

* If we only want to rude code without it displaying on page use different syntax `<% %>`

```html
<!-- This line will not show up on the page -->
<% if(greeting) {%>
  <!-- This line will only show if greeting is truthy -->
  <h1><%= greeting %></h1>
<% }%>

```

## Partial Files

* Make `partials` directory and include needed componenets in `views` ejs files
* Use syntax  `<%- include('FILE NAME') %>`

Example adding `views/partials/_header.ejs` to `views/urls_show.ejs`
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <%- include('partials/_header') %>
  <meta charset="utf-8">
---
```

## Getting Ready for POST request

* When browser submits a POST request, the data in the request body is sent as a `Buffer` which is not human readable

* Install a piece of middleware `body-parser` to convert to readable data

```bash
npm install body-parser
```

```javascript
// add to server js file before all routes codes
const bodyParser = require("body-parser");
app.use(bodyParser.urlencoded({extended: true}));
```

* `body-parser` library will
  1. convert the request body from a `Buffer` into human-readable string,
  2. Add the data to the `req`(request) object under the key `body`

## Redirection Response

* When the browser receives a redirection response, it does another `GET` request to the `url` in the response

* Use `res.redirect()`

Example:
```javascript
app.get('/u/:shortURL', (req, res) => {
  const longURL = urlDatabase[req.params.shortURL];
  res.redirect(longURL);
});
```

## Purpose of Routing Middleware (e.g Express library)
* It defines application endpoints (URIs)
* Sends respones back to the client
* Matches requested routes using pattern expressions (`'/ab*cd'`)