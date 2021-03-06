# OOP Part 1: Class & Instances

* Classes are blueprints (templates) that we use to create *instances* of objects

* A class describes what the object is going to be, and we can create new objects using the class

--

## Class

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



### Customizing the `constructor`

* Every class can have a single constructor method that will get called when an instance of that class is created

* Constructor method is the best place to set up any default property values for an object

* It's a method (function), so ppl can also pass in values (parameters) to the constructor method

* If you want to specify the instance's properties when it is created, set parameters in the class's `constructor` method, then pass values in the parameters as you're declaring the instance (see example).


Establishing a new `class` called `Pizza`:
```javascript
class Pizza {

  constructor(size, crust) {
    this.size = size;
    this.crust = crust;
    this.toppings = ["cheese"];
  }

  addTopping(topping) {
    this.toppings.push(topping);
  }

}
```

Using the class to create a new object, but passing in the size and crust:
```javascript
let pizza3 = new Pizza('large, 'thin);
```

This pizza instance will have properties that look like this:
```javascript
let pizza = {
  size: 'large',
  curst: 'thin',
  toppings: ['cheese']
}
```

--

## Primitives as Objects

* Each primitive in JS (excluding `symbol` which has weird rules) has a corresponding **object constructor** (see example).

```javascript
typeof(true); 
// "boolean" 
typeof(Boolean(true)); 
// => "boolean" 
typeof(new Boolean(true));
// => "object"
```

* An object constructor can be invoked with the keyword `new` => calling object constructors create new, unique *instances* of the objects requested

* Bad practice to use object constructors when creating primitives, because you will run into issues when comparing them (*avoid!!!*)

```javascript
const greeting = "Hello, world!" 
const objGreeting = new String("Hello, world!");

greeting == objGreeting; 
// => true

greeting === objGreeting; 
// => false
```

Despite having same string content, using `===` strict equality will return `false`, but using `==` will coerce one of the variable to the same type and return `true`. These issues can be quite problematic so avoid using these with primitive values if you can.

> TL;DR: Use object constructors when instantiating complex objects to use with your classes, but avoid using them when you're creating primitives.