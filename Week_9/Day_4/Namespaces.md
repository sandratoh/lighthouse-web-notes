# Namespaces

## Intro

* Funadamental concept of OOP

* Libraries (or gems, node pkg, etc.) can have functions that are named the same thing - program will throw an error if unsure which one to call

* Use **namingspacing** to organize functionality into named categories

## Namespacing in Ruby

### Modules as Namespaces

* Use modules as a tool for bundling logicaly related objects together

* Modules can store class, functions, or constants

* Use constant lookup (`::`) operator to scope things inside module

Eg: Having two version of the Array class (one is from us, one is Ruby built-in)

```rb
module Perimeter
  class Array
    def initialize
      @size = 400
    end
  end
end

our_array = Perimeter::Array.new
ruby_array = Array.new

p our_array.class     # custom module class
p ruby_array.class    # built-in class in Ruby
```

Eg: Nested constant lookups

```rb
module Dojo
  A = 4
  module Kata
  	B = 8
    module Roulette
      class ScopeIn
        def push
          15
        end
      end
    end
  end
end

A = 16
B = 23
C = 42

puts "A - #{A}"
puts "Dojo::A - #{Dojo::A}"

puts

puts "B - #{B}"
puts "Dojo::Kata::B - #{Dojo::Kata::B}"

puts

puts "C - #{C}"
puts "Dojo::Kata::Roulette::ScopeIn.new.push - #{Dojo::Kata::Roulette::ScopeIn.new.push}"
```

## Controller Namespaces and Routing

* Can organize groups of contrllers under a namespace

* Eg: Group a number of administrative controllers under an `Admin::` namespace, and place them under `app/controllers/admin` directory

* Use `namespace` block to create routes for each of the controllers (routes would have `/admin` prefix):
  ```rb
  namespace :admin do
    resources :articles, :comments
  end
  ```
* Use `scope` block and specify the `module: ` if you don't want the prefix (`/admin`), and just want it to route to the resources (`/articles`, and `/comments`)
  ```rb
  scope module: 'admin' do
    resources :articles, :comments
  end
  ```
* Use `resources` directly for single route, named route helpers won't have `admin_` before it like using `scope`, but path would still have the `/admin` prefix
  ```rb
  resources :articles, path: '/admin/articles'
  ```

Read more [here](https://guides.rubyonrails.org/routing.html#controller-namespaces-and-routing)