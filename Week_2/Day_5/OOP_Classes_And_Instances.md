# OOP Part 1: Class & Instances

* Classes are blueprints (templates) that we use to create *instances* of objects

* A class describes what the object is going to be, and we can create new objects using the class

### Class

* To declare a class: use the `class` keyword with the name of the class
  *  Name of class: a noun with first letter capitalized

```javascript
class Pizza {

}
```

* To create a new object from a class: use the `new` keyword

```javascript
let pizza1 = new Pizza();
let pizza2 = new Pizza();
```

* When you create an object using class, it is an **instance** of that class

* However, though instances are created from the same class, **they are completely separate objects**

> `pizza1` and `pizza2` are both *instances* of the `Pizza` class, but they are SEPARATE objects.

```javascript
pizza1 === pizza2; // false
```

### Methods and Properties

* Can add a method to a class with the following syntax

```javascript
class SomeClass {
  methodName(parameters) { // this is a method
    this.hello = 'hi'; // created a property called helo
  }
}
```
* Any pizza objects (*instances*) created from this `Pizza` class will have its own version of these properties and methods

> We can call the `addTopping()` method on `pizza1` without it affecting `pizza2`

* Methods will exist on instances created from the class, but not on the class itself

> Because a class is a blueprint for creating objects, methods will NOT work on them. (Even though you are creating them inside the class declaration code block, they can't be called. See example.)

```javascript
// This will **NOT** work.
// That's because addTopping is a method only available to actual instances of Pizza
// Give it a try!
Pizza.addTopping();
```

--

## Introduction to `constructor`

* `constructor` is a special kind of method (remember it's a function) that gets executed when an object instance is created from a class => sets up default values for any new object's properties

* Example: everything inside the `constructor` method will get run for the new instance of the class when we call new `Pizza()`

```javascript
class Pizza {
  constructor() {
    this.toppings = ["cheese"];
  }
}
```

--

## Customizing the `constructor`

* Every class can have a single constructor method that will get called when an instance of that class is created

* Constructor method is the best place to set  up any default property values for an object

* It's a method (function), so ppl can also pass in values (parameters) to the constructor method