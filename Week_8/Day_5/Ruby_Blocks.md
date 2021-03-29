# Ruby Blocks

## Intro
* In Ruby, a block is basically a chunk of code that can be passed to and excuted by any method.

* Blocks are always used with methods, which usually feed data or behaviours to them (as arguments).

* Any method can receive a block as an implicit argument. 

* Widely used in Ruby gems (including Rails) and in well-written Ruby code.

* Blocks are not objects, hence cannot be assigned to variables

## Basic Syntax

> A block is a piece of code enclosed by `{}` or `do...end`.

By convention:
* Single-line blocks: `{}` curly brace syntax
* Multi-line blocks: `do...end` syntax

## Execution

> A block is execute by the `yield` statement within a method.

```ruby
def meditate
  print "Today we will practice zazen"
  yield # This indicates the method is expecting a block
end 

# We are passing a block as an argument to the meditate method
meditate { print " for 40 minutes." }

Output:
Today we will practice zazen for 40 minutes.
```

What is happening:
  * When `yield` statement is reached, the method *yields control* to the block and runs code within it
  * Once block is excuted, control is *returned* back to the method, which resumes executing the codes immediately after the `yield` statement

## Exception and Optional Block

* If a block is not provided when expected in a method, an exception will be throw when program reaches the yield statement

> If a block is optional, avoid an exception from being raise by adding `if block_given?` inside `yield` statement

```ruby
def meditate
  puts "Today we will practice zazen."
  yield if block_given? 
end meditate

Output:
Today we will practice zazen. 
```

* It is not possible to pass multiple blocks to a method. Each method can receive only one block.

Read more in this [StackOverflow question](http://stackoverflow.com/questions/3066703/blocks-and-yields-in-ruby)

## Example 1: `yield`ing invisible Block
* Passing blocks as a sort of 'invisible argument'

```ruby
def print_result
  result_from_block = yield
  puts result_from_block
end

# This will print out the number 9 to the console
print_result { 3 * 3 }
```

* Writing blocks with `do...end` syntax
```ruby
# Blocks can also be written using the do...end format
print_result do
  creature = "walrus"
  "I am the #{creature}!"
end
```

## Example 2: Alternative Syntax
* Accept block as argument to a function by being more explicit when defining the argument list

```ruby
def print_result(&block)
  result_from_block = block.call
  puts result_from_block
end
```

## Blocks === Callbacks?
* Passing a *block* in Ruby is very similar to passing a *callback function* into a JavaScript function.

* Ruby also has Procs and Lambdas which are even more like callbacks than blocks are.
  * More powerful
  * Less commonly used/needed