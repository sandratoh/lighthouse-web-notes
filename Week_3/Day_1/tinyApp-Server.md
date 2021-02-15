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
