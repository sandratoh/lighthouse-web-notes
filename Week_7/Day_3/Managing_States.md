# Managing and Combining States

## Combine various states to better manage app

Previous states
```jsx
const [day, setDay] = useState('Monday');
const [days, setDays] = useState([]);
```

Combined state
```jsx
const [state, setState] = useState({
    day: 'Monday',
    days: []
  });
```

## What happens to `setDay` and `setDays`?

Even after combining different states into a single object, we can still have separate actions to update certain parts of the state

```jsx
const setDay  = day  => setState({ ...state, day });
const setDays = days => setState({ ...state, days });
```

Can also use `Object.assign` technique to merge objects
```jsx
const state = { day: "Monday", days: [] };
setState(Object.assign({}, state, { day: "Tuesday" });

```
> MUST INCLUDE EMPTY OBJECT AS FIRST ARGUMENT IN `assign`, otherwise this would mutate the `state`!!!

## `useEffect` and New Dependencies

* If any of previous unmerged state was used as a dependency in an `useEffect` operation, using the new state/state functions may cause an error because our dependency changed

* We need to update the dependency in relation to the new combined state

* In scheduler app, to remove the dependency, we pass a function to `setState`

```jsx
const setDays = days => setState(prev => ({ ...prev, days }));
```