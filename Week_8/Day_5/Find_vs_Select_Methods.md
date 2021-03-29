# `.find` vs `.select` Method in Ruby

## Enumerable
* An object is an *enumerable* when it describes a set of items and a method to loop over each of them

## The .find method

* Alias `.detect` - same output as `.find`

* Iterates through an array and gives the **first match** for which the expression within a block returns true

* If value is not found, iterator will return `nil`

Example:
```ruby
>> [1,2,3,4,5,6,7].find { |x| x.between?(3,4) }
=> 3
>> [1,2,3,4,5,6,7].find { |x| x.between?(3,6) }
=> 3
>> [1,2,3,4,5,6,7].detect { |x| x.between?(3,7) }
=> 3
>> [1,2,3,4,5,6,7].detect { |x| x.between?(2,7) }
=> 2
```

## The .select method

* Iterates on an array or hash, and returns an array or hash of **all values that evalute as true** given a block of code

Example:
```ruby
[1,2,3,4,5].select { |num|  num.even?  }   #=> [2, 4]
```

### .select vs .find_all
* `.find_all` can be an alias for `.select` when working with arrays, BUT they work differently when working with hashes

Example:
```ruby
array = [1, 2, 3, 4, 5, 6]
hash = {a: 1, b: 2, c: 3, d: 4, e: 5, f: 6}

array.select{|x| x.even?}       # => [2, 4, 6]
array.find_all{|x| x.even?}     # => [2, 4, 6]

hash.select{|k,v| v.even?}     # => {:b=>2, :d=>4, :f=>6}
hash.find_all{|k,v| v.even?}   # => [[:b, 2], [:d, 4], [:f, 6]]
```
What is happening?
* `.find_all` gives an **array** regardless of if you're iterating over an array or hash
* `.select` returns an **array or hash** depending on your input

Read more [here](https://medium.com/@ingridf/understanding-the-differences-between-select-and-find-methods-in-ruby-16f4632c24b8)