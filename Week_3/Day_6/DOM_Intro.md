# The DOM

What it stands for: **Document Object Model**

## What is it?
* A representation of the HTML and CSS document of a website created by the browser

* The **model** allows JS to access the text content and elements of the website **documents** as **objects**

## The Document Object
* The `document` object is a built-in object that has many **properties** and **methods** that we can use to access and modify websites

* Typing `document` in console of DOM and see output of the object

## Difference between DOM and HTML Source Code
Two instances when browser-generated DOM will be different than HTML source code:
    1. The DOM is modified by client-side JavaScript
    2. The browser automatically fixes errors in the source code

### Modifying DOM by Client-side JavaScript
* When modifying CSS property in DOM, have to type out hyphenated CSS property as camelCase in JavaScript

* Won't change the source code, new code we added in the console will disappear when we refresh the page

### DOM Fixing Errors
* DOM automatically fixes some mistakes that devs might leave in their HTML

* Example: forgetting to include `table` tag, or forgetting to close tags 