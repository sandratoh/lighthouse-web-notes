# Transforming Data with Selectors

## Intro

* Sometimes, we have to transform data retrieved from an API so we can use it with our component (e.g formatting issue)

* To compute new data from an existing state, we can use **selectors** - a function that accepts state as an argument and returns data that is derived from that state

## Selectors

### Simple Example
```javascript
function selectUserByName(state, name) {
  const filteredNames = state.users.filter(user => user.name === name);
  return filteredNames;
}
```

### Reasons to use selectors
* We can transform data into a format that is compatible with what our components expect as props

* We can compute new data from existing data

### Unit Tests
* Since these functions only depend on the argument passed to them, they are easy to test with unit tests