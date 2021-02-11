# JSON Fundamentals

## What is it?

* **JavaScript Object Notation** - a subset of the JavaScript language, therefore, will follow valid JS syntax

* Built on two universal data structures:
  1. A collection of name/value pairs
  2. An ordered list of values

* Keys are always double-quoted 'strings' (no trailing commas allowed), and values can be numbers (no leading zeros, NaN or Infinity), strings, or objects (see JSON example)

```json
{
  "name": "New York City",
  "boroughs": [
    "Manhattan",
    "Queens",
    "Brooklyn",
    "The Bronx",
    "Staten Island"],
  "population": 8491079,
  "area_codes": [212, 347, 646, 718, 917, 929],
  "position": { "lat": 40.7127, "lng": -74.0059 }
}
```

--

## Serialization

* **Serialization**: converts `objects`(or data structures) => `strings` of text (usually)
  * so it can be stored or transmitted between computers

* **Deserialization**: opposite of serialization, goes from `string` => `object`

* JSON object is JavaScript's method to serialize and deserialize. [Read more on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON#Methods)

---

## Static Methods 

### `JSON.parse(string[, reviver])`
* Parse a string as JSON, optionally transform the produced value and its properties, and return the value.

* Optional `reviver` parameter: for interpreting what the `replacer` has used to stand in for other datatypes

### `JSON.stringify(value[, replacers[, splace]]`)
* Return a JSON string corresponding to the specificed value, optionally including only certain properties or replacing property values in a user-defined manner

* By default, all instances of `undefined` are replaced with `null`, and other unsupported native data types are censored

* Optional `replacer` parameter: for specifying other behaviour

> Basically opposite of each other, `JSON.parse` goes from `string` => `object`, while `JSON.stringify` goes from `object` => `string`

--

## JSON Media Type
* Media Type for JSON data is different depending on medium used
  * HTTP request/responses: `application/json`
    * set via the `Content-Type` HTTP response header
  * HTML: `text/html`

> To check Content-Type in HTML response header, run this code in terminal `curl -i ipinfo.io`

* Example: `Content-Type: application/json; charset=utf-8`
  * indicates the media t ype and character encoding of the response body

## JSON for Configuration Like `package.json`
* JSON is great for configuration/setting files
* Text read from the file is a string
* NPM needs that info so it reads the file (`package.json`), then parses the info into an object using the JSON object

## JSON > XML
* Before JSON, XML was the standard
* Problem with XML: has query, sends it server,which gets to database, and gets sent back an XML thing, which you need to send another query to get the data inside
  * Why don't you just give it to me before? => JSON!

## JSON is Language Independent
* Can be used not *just* in Node / JS Projects, but in other programming languguages / ecosystems:
  * Python
  * Ruby
  * C#
  * Golang
  * Rust
  * and many more!