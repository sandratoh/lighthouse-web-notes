# Custom Hooks in React

## Rules for Custom Hooks
1. A custom Hook is a function that **must start with the word 'use'**
2. Don't call Hooks inside loops, conditions, or nested functions (general Hook rule)
3. Only call Hooks from inside React component (general Hook rule)

## Usage
What problems Hooks can solve in React:
* It's hard to reuse stateful logic between components
* Complex components grow in size
* Classes confuse people and machines

> Custom Hooks can reduce repetition in components and help manage complex classes and components

* Store custom Hooks in `src/hooks` folder, with each file containing a single Hook

* Example: `useDebounce` hook
  ```jsx
  import { useEffect } from "react";

  export default function useDebounce(operation, ms) {
    useEffect(() => {
      const handle = setTimeout(operation, ms);
      return () => clearTimeout(handle);
    }, [operation, ms]);
  }
  ```
