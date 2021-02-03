# Objects - Basic Concepts

## Objects Overview
* Contain **key-value pairs**; each key maps to a value
* Contain keys which are *always strings* (or symbols, but it's less common and not important right now)
* Have unique keys; the same key cannot appear twice in an object
* Have their keys point to values which can be of any type

--

## Object Literals
### Syntax:
* Use curly braces `{}`
* Use colon `:` to assign value to variable
* Use comma `,` to separate each key-value pairing
```javascript
//empty object
const emptyObject = {};

//object literal with a single key-value pair
const tinyObject = { size: "Tiny" };

//object literal with three key-value pair
const myObject = { shape: 'Round', colour: 'Teal', isMine: true };
```

#### *Notes: **Literals** = notation for representing a fixed value in source code. ('Literally' writing some codes this way lead to a certainly typed variable exclusively)*

--

## Object Values
* Can be of any type
  ```javascript
  // Example
  const myObject = {
    a: 6,     // Number
    b: "abc", // String
    c: true,  // Boolean
    d: null,  // Null
  };
  ```
* Can be a pre-defined variable 
  ```javascript
  const spam = "spam";
  person["dislikes"] = { food: spam, "e-mail": "spam" };
  ```

## Accessing Object Values
* Square-bracket notation (`[]`)
  * **Must use quotation mark around key (as a string).** Otherwise, it would be considered a variable name instead of a string literal.
    * Will return `ReferenceError` if variable was not defined previously
* Dot notation (`.`)

```javascript
const person = { firstName: "Khurram" };

// Square-bracket notation
person["firstName"]

// Dot notation
person.firstName
```

## Assigning a New Value to a Key
* Access object using either square bracket or dot notations, then assign values to new/exisiting keys using `=` operator

## Objects as values
* Can nest objects within objects (but don't go overboard b/c it can get too complicated)
* Basically, a key-value pair in an object can have a value that is another object

  ```javascript
  const person = {
    name: "Paul",
    address: {
      street: "310 W 95th",
      city: "New York",
      zipCode: 10027
    }
  };
  ```
* To access the nested object
  ```javascript
  person["address"]["city"]; // => "New York"

  person.address.city // => "New York"
  ```

## Object.keys
* To inspect an object's keys, use method `Object.keys(...)` and it will return an array of keys

```javascript
Object.keys(person) // Output: [ 'name', 'address', 'phoneNumber' ]
```