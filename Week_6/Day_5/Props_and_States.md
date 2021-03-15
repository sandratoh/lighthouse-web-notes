# React Concepts: Props & States

### Definitions
**Props**: data passed from a parent componenet to a child component
  * Like passing args to a function except you can't change the *props* passed to a componet
  * Props only change when the parent passes new one

**State**: private data managed internally by the componenet
  * State is owned locally - only exists at the level it was created at
  * State is mutable - updated by the component that owns it
  * Triggers a `render()` when changed

### How to differentiate?
1. Is it passed in from a parent via *props*?

2. Does it remain unchanged over time?

3. Can you compute it based on any other *state* or *props* in your componenent.

If any of them are true, it probably isn't *state*.

### Components
* React is component-based, which makes it possible to split a complex applicatin into smaller cpomponents

* Good compononents are:
  * composable
  * encapsulated
  * resusable
  * testable
  * only have single responsibility (ideally)