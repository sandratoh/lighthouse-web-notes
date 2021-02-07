# Automated Testing

## Unit Testing

* Practice of testing small pices of code alone and isolated (e.g individual functions)
* Essentially gives the function t hat's tested some inputs, then check the function output is correct
* Can use unit tests to help design codes and keep it as a safety net when doing changes
* Same methods used in unit testing are also applicable to other types of testing (they just get more complex and less precise in other tests)
* Prevents **regressions** - bugs that  occur repeatedly (better than integration/function tests in this area because unit tests are more *specific*)

#### Q: When should you use unit testing?
#### A: Ideally, at all times

## Integration Testing

* Test how parts of the system work together - the integration of the parts
* Similar to Unit Testing except... *integration tests are NOT isolated from other componenets*
* Useful for when unit testing is not enough, eg. when verifying two separate systems are working together corectly
* Slower than unit tests because of the added complexity
* Might need some set up or configuration
  * Makes writing and maintetance harder, so focus on unit tests unless you absolutely need an integration test
* Can usually be written with the same tools as unit testing

## Functional Testing

* AKA **E2E Testing** or **Browser Testing** (all the same thing)
* Testing of complete functionality of some application
  * Eg. in web apps, it means using some tool to automate a browser, which is then used to click around on the pages to test the application
* Difficult to write because of high complexity
* Runs very slowly because stimulates relal user interaction on a web page
* Should used for testing common user interactions, like an user flow
* Validate test results as if you were an user instead of through the code results alone
* Use if have some repeated tests you do manually in the browser
* Be careful not to make them too fine-grained
* Common tools for functional testing:
  * Selemnium
  * PhantomJS
  * CasperJS