# Intro to Inheritance

## The Duplication Problem
* As you create different types of objects, codes will start to duplicate

* Two classes might share behaviours and state information (may have some identical but not all the same).
  * Behaviours: `constructor` and other methods
  * State info: properties


  ## A Solution with Inheritance
  * Technique in OOP where we can build a new class based on an existing class
  
  * Move everything that is common between the other existing classes into this class

  * Use keyword `extends` for **subclasses** (`Student` and `Mentor`) to inherit behaviour and state info from the **superclass** (`Person`)

  ```javascript
  // This class represents all that is common between Student and Mentor
  class Person {
    // moved here b/c it was identical
    constructor(name, quirkyFact) {
      this.name = name;
      this.quirkyFact = quirkyFact;
  }

  // moved here b/c it was identical
    bio() {
      return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
    }
  }
  ```

  ```javascript
  class Student extends Person {
    // stays in Student class since it's specific to students only
    enroll(cohort) {
      this.cohort = cohort;
    }
  }

  class Mentor extends Person {
    // specific to mentors
    goOnShift() {
      this.onShift = true;
    }

    // specific to mentors
    goOffShift() {
      this.onShift = false;
    }
  }
  ```