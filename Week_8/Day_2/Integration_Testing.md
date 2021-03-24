# Integration Testing

## Scoping to Containers

Recall the two ways to work with `dom-testing-library` queries: imported or returned
```javascript
import { getByText } from "@testing-library/react"; // Method 1. Imported from lib
const { getyByText } = render(<Application />);     // Method 2. Returned in a test
```

* Queries in Method 2 are automatically scoped to the `document.body` - will search the document from top to bottom every time

* Scoping is a technique used to search subtrees of DOM - need to import directly from library

## prettyDOM

* Helpful function from `@testing-library/react` that outputs a useful representation of the DOM tree

```javascript
import { prettyDOM } from "@testing-library/react";
```

## Adding test id

* Eg: adding a `data-testid="appointment"` prop to an `<article>` element

* Any attribute on an HTML element prefixed with `data-` is accessible through the browser API using `document.querySelector("[data-testid=appointment]")`. It is the same API that the dom-testing-library uses to perform the query internally.

