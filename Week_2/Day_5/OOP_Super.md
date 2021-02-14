# Method Overriding and Super

### The Problem
Sometimes you want a subclass to have similar but slightly different behaviour to its superclass

### Solution Part 1: **Method Override**
Subclass implements a method that already exists in the superclass: completely re-define the method inherited from superclass and gives its own version of the method when called.

```javascript
// Superclass
class Person {
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

// Subclass
class Mentor extends Person {
  // Completely re-define the bio method since it has more to say
  bio() {
    return `I'm a mentor at Lighthouse Labs. My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

// DRIVER CODE

const bob = new Mentor('Bob Ross', 'I like mountains way too much');
console.log(bob.bio());
```

### Solution Part 2: Use `super`!
Subclass's re-defined method can also call on and reference its parent class/superclass's method by using the key word `super`

> Using `super` allows us to access the superclass.

```javascript
class Mentor extends Person {
  // Mentor bios need to include a bit more info
  bio() {
    return `I'm a mentor at Lighthouse Labs. ${super.bio()}`;
  }
}
```

--

### Conclusion
* Overriding methods in subclasses to change their behaviours. If you end up repeating some things in the overring methods...

* Use `super` in the overriding methos to avoid repeating code that's already present in the superclass.