# Getters and Setters

* **Getters** and **setters** are special methods that are used to *get* the value of a property or *set* the value of a proprty

* Reasons for using getters and setters:
  1. *Validating* data before assigning it to a property
  2. *Computing* a value on the fly instead of simply pulling it out of a property

### Validating Data

* We can include data validation in the object's **setter method** so the object can validate the value before it gets set.

* Eg: if pizza can only have three sizes (`s`, `m`, `l`), but someone set the size to something invalid like an emoji or x-large, setter method will reject/ignore that value before the invalid value gets set

### Computed Value

* Using a property to keep track of changes means we have to keep track of all the changes and constantly update it, even if we don't need it at the moment.

* Using a **getter method** allows us to compute values when it is needed

---

### A better way with `get` and `set`

* The need for getters and setters is very common in OOP

* JS classes have special `get` and `set` keywords to implement getters and setters more easily

* Behind the scenes: `get` and `set` binds an object's property to a function that will be called when that value is looked up
  * Method will appear as a value

* Makes object's interface more simple

Previously:
```javascript
setSize(size) {
    if (size === 's' || size === 'm' || size === 'l') {
      this.size = size;
    }
  }

getPrice() {
    const basePrice = 10;
    const toppingPrice = 2;
    return basePrice + (this.toppings * toppingPrice);
  }
```

With `set` keyword:
```javascript
set size(size) {
  if (size === 's' || size === 'm' || size === 'l') {
      this.size = size;
    }
}

get price() {
    const basePrice = 10;
    const toppingPrice = 2;
    return basePrice + (this.toppings * toppingPrice);
  }
```

What it changes: (accessing parameter as *value properties* instead of *method properties*):
```javascript:
let pizza = new Pizza();

pizza.price;      // instead of getPrice()
pizza.size = 's'; // instead of setSize(size)
```