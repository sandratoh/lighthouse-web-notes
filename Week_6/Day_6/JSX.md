# JSX

* JSX - language used with React to create elements and declare how an interface looks

* Not required to use with React, but has lots of benefits

* Looks a lot like HTML, but it is NOT HTML

* Some properties do not map directly to HTML attributes (read through warnings)
  * Eg: JSX uses `className` instead of HTML/CSS's `class`

## React.createElement

* Define the type of element and any properties we want to pass to element

* JSX codes run through a tool that knows how to turn JSX into JavaScript. The tool produces a JS expression that creates a React element

**JSX:**
```jsx
const element = <h2 className="name">Name</h2>
```
-- *JSX codes run through tool and converted to JS expression* --

**JavaScript:**
```javascript
const element = React.createElement("h2", {
  className: "name"
}, "Name")
```

* `React.createElement(type, [props], [...children])` function allows us to create a hierarchy of DOM nodes

> Have to `import React from 'react` (add to top of file) even when we don't see a reference to `React` anywhere in the file. When the JSX is converted to JavaScript the dependency on React is revealed.

**JSX:**
```jsx
import React from "react";

function Tweet() {
  return (
    <article className="tweet">
      <header className="tweet__header">
        <img
          className="tweet__header-avatar"
          src="https://api.adorable.io/avatars/64/react@adorable.png"
          alt="Avatar"
        />
        <h2 className="tweet__header-name">React</h2>
      </header>
      <main className="tweet__content">
        <p>A JavaScript library for building user interfaces</p>
      </main>
      <footer className="tweet__footer">May 29th, 2013</footer>
    </article>
  );
}
```

**JavaScript:**
```javascript
import React from "react";

function Tweet() {
  return React.createElement(
    "article",
    {
      className: "tweet"
    },
    React.createElement(
      "header",
      {
        className: "tweet__header"
      },
      React.createElement("img", {
        className: "tweet__header-avatar",
        src: "https://api.adorable.io/avatars/64/react@adorable.png",
        alt: "Avatar"
      }),
      React.createElement(
        "h2",
        {
          className: "tweet__header-name"
        },
        "React"
      )
    ),
    React.createElement(
      "main",
      {
        className: "tweet__content"
      },
      React.createElement(
        "p",
        null,
        "A JavaScript library for building user interfaces"
      )
    ),
    React.createElement(
      "footer",
      {
        className: "tweet__footer"
      },
      "May 29th, 2013"
    )
  );
}
```

* In React, must start componenet names with a capital letter - when JSX is converted, it uses the case of the tag name to determine if it's a componenet (first letter uppercase) or an HTML element (all lowercase)
  * Eg: create a Tweet componenet with `const tweet = <Tweet />`

> Always start component names with a capital letter

## ReactDOM.render

* Elements can be 'rendered' into any DOM node using the `react-dom` library

  ```jsx
  import ReactDOM from 'react-dom';
  ```

* Most apps call `ReactDOM.render(element, container)` once to render the app

```jsx
import React from "react";
import ReactDOM from "react-dom";

function Tweet(props) {
  return (
    <article className="tweet">
      <header className="tweet__header">
        <img className="tweet__header-avatar" src={ props.avatar } />
        <h2 className="tweet__header-name">{ props.name }</h2>
      </header>
      <main className="tweet__content">
        <p>{ props.content }</p>
      </main>
      <footer className="tweet__footer">{ props.date }</footer>
    </article>
  );
}

ReactDOM.render(
  <Tweet
    name="React"
    avatar="https://api.adorable.io/avatars/64/react@adorable.png"
    content="A JavaScript library for building user interfaces"
    date="May 29th, 2013"
  />,
  document.getElementById("root") // render <Tweet /> into 'root' DOM node
)
```

## JSX Expressions

* JSX feels very similar to EJS and looks like a template language, but it is purely JavaScript

* Can include expressions and functions within JSX

## JSX Rules

### **Rule #1**
All tags must be closed (2 methods)
  1. Open and close tag
  2. Self-closing tag

```jsx
<div>
  <img> 
  <Album />
</div>

/* will give error beause not closed, should be <img /> */
```

### **Rule #2**
A child tag must close before its parents - creating a tree struture, so last one to open is the next one to close

```jsx
<div>
  <ul>
    <li>
    </ul> {/* gives error because closed before </li> */}
  </li>
</div>
```

### **Rule #3**
All JSX expressions must result in one root level element.

* A function can only `return` one value (can NOT return multiple values)

* componenet is defined using a JS Func, so same rules apply

**Bad:**
```jsx
return (
  <div>
  </div>
  <input />
)

/* becomes? */

return (
  React.createElement("div", null)
  React.createElement("input", null)
)

/* Nope. Functions can't return multiple values like that. */

/* Gives error: adjacent JSX elements must be wrapped in an enclosing tag */
```

**Good:**
```jsx
return (
  <div>
    <input />
  </div>
)

/* becomes */

return React.createElement("div", null, React.createElement("input", null))
```

### **Rule #5**
No HTML comments
```jsx
return (
  <div>
    <!--- Not allowed --->
    {/* Allowed */}
  </div>
)
```