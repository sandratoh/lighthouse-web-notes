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
  // stays in Student class since it's specific tostudents only
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

* When constructing instances of the **subclasses**, you can use parameters set by the `constructor` method in the **superclass**. You can use it when creating the instance, or after it is created as a method.

* When declaring the instance, if you want to skip a parameter, put `undefined` as parameter value

```javascript
let mentorOne = new Mentor('Lupin', 'Werewolf');
mentorOne.goOnShift();
console.log(mentorOne);
// output: Mentor { name: 'Lupin', quirkyFact:'Werewolf', onShift: true }

let studentOne = new Student;
studentOne.enroll('Feb 2021');
studentOne.name = 'Hermione Granger';
studentOne.quirkyFact = 'Knows magic';
console.log(studentOne);
// output: Student { name: 'Hermione Granger', quirkyFact: 'Knows magic, cohort: 'Feb 2021' }
console.log(studentOne.bio());
// output: My name is Hermione Granger and here's my quirky fact: Knows magic
```