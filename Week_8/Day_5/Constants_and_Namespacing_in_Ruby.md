# Constants and Namespacing in Ruby

## Constants

In Ruby, any keyword with a capitalized first letter is considered a constant.

Exaple: Both `Math` and `PI` are constants that refer to a Module
```ruby
Math.class # => Module
Math::PI.class # => Float
```
## Namespacing

Question: What is `::` in `Math::PI`???

Answer:It's how the Math library define the constant `PI` *within* the `Math` space

Both Module and Class constants create a namespace within which other constants can be placed.

### Why is namespacing imporant?

Important and used heavily because it:
  * Limits the exposure of constants defined in the global namespace
  * Avoids name collision between multiple identifiers that share the same name

When you `require` a library in Ruby:
  * No variable reference pointing to the contents of the library
  * Required files have the ability to and are expected to define constants in the global namespace

**JavaScript Example**
```js
const express = require('express');

// Now the things that the express module exports are only available via the express variable.
```

**Ruby Example**
```rb
require 'some_library'

# No variable to refer back to the library
```

### Creating constnats and namespaces
```rb
module Apple
  FOUNDED_BY = "L. Ron Hubbard"
end
```

## Summary

In Ruby:
  * Capitalized words can be used to define a constant
  * A constant can refer to a Module, Class, or simple data like Floats and Strings
  * Namespacing is used heavily to limit the exposure of constants defined in the global namespace
  * The `::` Syntax is used to access constants (Modules, Classes, etc)
  * It is convention to only capitalize the first letter when defining Class and Module constants like `Apple`
  * It is convention to capitalize and underscore the entire name when defining value constants like `FOUNDED_BY`