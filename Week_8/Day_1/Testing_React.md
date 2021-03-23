# Testing React

## Unit Test Structures
1. **Setup**:  Initialize the component we want to test
2. **Change**: Trigger the change that executes the unit
3. **Verify**: Verify that unit produced the expected result

### Most Basic Test - render without crash: 

```javascript
it("renders without crashing", () => {
  render(<Button />);
});
```
* `it` function - from Jest
* `render` function - from `react-testing-library` to render our component (`Button` in this case)

## Testing Helpers

```javascript
it("renders its `children` prop as text", () => {
  const { getByText } = render(<Button>Default</Button>);
  expect(getByText("Default")).toBeInTheDocument();
});
```
* `render` fn - from `react-testing-library`
* `expect` fn - injected into global scope from Jest
* `getByText` **query** fn - returned by the `render` fn but is a part of the `dom-testing-library`
* `toBeInTHeDocument` fn - [**matcher**](https://jestjs.io/docs/expect) provided through JEst by `jest-dom` library
  * matchers: allow us to validate different things with `expect`

### Libraries

* [Jest](https://jestjs.io/docs/en/expect)

* [jest-dom](https://github.com/testing-library/jest-dom)

* [react-testing-library](https://testing-library.com/docs/react-testing-library/intro)
  * builds on top of `dom-testing-library` to specifically work with React components
  * inherit access to queries provided by `dom-testing-library`

* [dom-testing-library](https://testing-library.com):
  * read more about queries [here](https://testing-library.com/docs/queries/about/)

  * Single Elements
    * `queryBy...` - sync, returns `null` if unable to find, throws error if more than one match is found
    * `getBy...`   - sync, throws error if unable to find
    * `findBy...`  - async, throws error if unable to find, returns a Promise

  * Multiple Elements
    * `queryAllBy...`
    * `getAllBy...`  
    * `findAllBy...` 