# Introduction to Object Oriented Programming

## What is Object Orientation?
* *Object Orientation* ("OO") is a software development paradigm

* *Object Orientation Programming* ("OOP") - the practice of using objects to keep codes modular and reduce repetition

* Many modern languages have been designed mainly for OOP or are *predominantly* OO:
  * C++
  * C#
  * Java
  * Python
  * Ruby
  * PHP
  * Swift
  * Objective-C

* Some other languages chose *Functional Programming* (FP)
  * Erlang
  * Common Lisp
  * Elixir
  * Haskell
  * Clojure

## JavaScript and OO:
* JS has multiple paradigms: initially popularized FP, but was also object-oriented.

* ES6 brought in more OOP features and enhanced the language

* Having multiple paradigms make a language more flexible and powerful, but also tends to cause confusion among community.

### Terminology

* An object is a collection of key-value pairs known as `properties`

* An object is a little bundle of info, AKA `states`

* Each property that an object has can represent the state of that object
  * Eg: In example, the object's `sound` is `'woof'` and its `breed` is '`'shih tzu'` => that is the dog's state!

* When a property's value is a function, it's called a `method`

* An object's `behaviours` are things they can do. They take the form of `methods` - some methods might modify the object, some might ask the object for info, etc.
  * Eg: In example, the dog has a method called `speak()` that logs info to console => that is the dog's behaviour!

```javascript
const dog = {
  sound: "woof", // Property
  breed: "shih tzu", // Property
  speak: function() { // Method
    console.log(`${this.dogBreed} says ${this.dogSound}`);
  }
};
```

### `this`
* `this` is a keyword, like `for` for `function`, so like any other keyword, it has its own special functionality

* context matters for `this`: value of `this` is determined at the time of the call and depends on *how* and *where* it was called

> In JavaScipt: when you use `this` inside a method, `this` refers to the object that the method was called on

* JavaScript OO: when used inside a method, `this` refers to the object that the method was called on 

Example: `this` and `dog` are the same in this case
```javascript
const dog = {
  sound: "woof",
  speak: function() {
    console.log(this.sound);
  },
  teachMeSomething: function() {
    if (dog === this) {
      console.log('dog === this');
    }
    this.speak();
  }
};

dog.teachMeSomething();
```

> Whenever your method is accessing a property or another method on the same object, use `this`.

## Conclusion

OO bundles (groups) together related state and logic into an object that can be passed around as a single entity.