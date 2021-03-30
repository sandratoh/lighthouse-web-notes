# Active Record (AR)

## Intro
* Active Record (AR) = The ORM (Object Relational Mapper) of choice for Ruby/Rails devs.

* Developed as part of Rails specifically to allow web app to easily work with a SQL db using Classes

* Each AR Class aka Model corresponds to an existing table in the db and provides attirbutes that map to each column/field in the table

* Allows us to CRUD records in that table using that Class and its instances

* Read more on [Rails Guides](https://edgeguides.rubyonrails.org/active_record_basics.html)

## 1. What is Active Record?
* The M in MVC (model, view, controller) - reponsible for representing business data and logic

* **Object Relational Mapping** (ORM) - a technique that connects objects of an app to tables in a relational database management system

* ORM Pros:
  * Write less database access codes
  * More easily store and retrieve object properties and relationships from database

## 2. Convention Over Configuration in AR

### Naming Conventions
* Pluralization menchanisms
  * Eg: `Book` class should have a database table called `books`

* Class names composed of two or more words:
  * Model Class: CamelCase form - singular with first letter of each word capitalized
    * Eg: `BookClub`, `Person`, `Dog`
  * Database Table: snake_case form - plural with underscores separating words
    * Eg: `book_clubs`, `people`, `dogs`

### Schema Conventions
* Convention depends on the purpose of column

* **Foreign keys** - follow the pattern `singularized_table_name_id` (eg: `item_id`, `order_id`)
  * AR will look for these fields when we create associations between our models

* **Primary keys** - By default, AR will use an integer column named `id` as table's primary key
  * Equivalent to `bigint` for PostgreSQL and MySQL, and `integer` for SQLite

* Optional column names with built-in additional features (don't use these keywords if don't need):
  * `created_at` - automatic date and time when created
  * `updated_at` - automatic date and time when created/updated
  * `lock_version` - adds optimistic locking to a model
  * `type` - species that  model uses *Single Table Inheritance* (STI)
  * `(association_name)_type` - store  type for *polymorphic association*
  * `(table_name)_count` - cache the # of belonging objects on association

## 3. Creating Active Record Model
* subclass the `ApplicationRecord` class, and good to go

```rb
class Product < ApplicationRecord
end
```

This will create a `Product` model, mapped to `products` table at the db

## 4. Overriding Naming Conventions
* If need to override for whatever reason, can look into methods in `ActiveRecord::Base` which is where `ApplicationRecord` inherits from

* Eg: Use `ActiveRecord::Base.table_name` when you need to specify the table name that should be used
  ```rb
  class Product < ApplicationRecord
    self.table_name = "my_products"
  end
  ```

* Need to then do use `set_fixture_class` to manually define class name that is hosting the fixture
  ```rb
  class ProductTest < ActiveSupport::TestCase
    set_fixture_class my_products: Product
    fixtures :my_products
    # ...
  end
  ```

* Eg: Override primary key column with `ActiveRecord::Base.primary_key=`
  ```rb
  class Product < ApplicationRecord
    self.primary_key = "product_id"
  end
  ```

## 5. CRUD: Reading and Writing Data

### Create

* `create` will return the object and save it to the database
```rb
user = User.create(name: "David", occupation: "Code Artist")
```

* `new` method will return and instantiate a new object without being saved
```rb
user = User.new
user.name = "David"
user.occupation = "Code Artist"
```
* A call to `user.save` will commit the record to the database

* If a block provided, both `create` and `new` will yield the new object to that block for initialization
```rb
user = User.new do |u|
  u.name = "David"
  u.occupation = "Code Artist"
end
```

### Read
More query methods in the [Active Record Query Interface guide](https://edgeguides.rubyonrails.org/active_record_querying.html)

Examples:
```rb
# return a collection with all users
users = User.all
```

```rb
# return the first user
user = User.first
```

```rb
# return the first user named David
david = User.find_by(name: 'David')
```

```rb
# find all users named David who are Code Artists and sort by created_at in reverse chronological order
users = User.where(name: 'David', occupation: 'Code Artist').order(created_at: :desc)
```

### Update
Approach:
1. Retrieve an AR object
2. Modify attributes
3. Save to database

Example:
```rb
user = User.find_by(name: 'David')
user.name = 'Dave'
user.save
```

Shorthand by hash mapping attribute names to desired value (useful when updating several attributes at once):
```rb
user = User.find_by(name: 'David')
user.update(name: 'Dave')
```

Use `update_all` class method if need to update several records in bulk:
```rb
User.update_all "max_login_attempts = 3, must_change_password = 'true'"
```

### Delete
Approach:
1. Retrieve an AR object
2. Destroy (remove) from database

```rb
user = User.find_by(name: 'David')
user.destroy
```

Use `destroy_by` or `destroy_all` method if deleting several records in bulk
```rb
# find and delete all users named David
User.destroy_by(name: 'David')

# delete all users
User.destroy_all
```

## 6. Validations

* More about validation in the [Active Record Validations guide](https://edgeguides.rubyonrails.org/active_record_validations.html)

* Validate the state of a model before it  gets written into the database (`save` and `update`)

* `save` and `update` will return `false` when validation fails, and operation will NOT run in database

* bang counterpart (`save!` and `update!`) raise exception `ActiveRecord::RecordInvalid` if validation fails

```rb
class User < ApplicationRecord
  validates :name, presence: true
end
```
```bash
irb> user = User.new
irb> user.save
=> false
irb> user.save!
ActiveRecord::RecordInvalid: Validation failed: Name can't be blank
```

## 7. Callbacks

* More about callbacks in [Active Record Callbacks guide](https://edgeguides.rubyonrails.org/active_record_callbacks.html)

## 8. Migrations
* Migrations = Rail's domain-specific language for managing a database schema
* Stored in file and executed against AR-supported database using `rake`

Example:
```rb
class CreatePublications < ActiveRecord::Migration[6.0]
  def change
    create_table :publications do |t|
      t.string :title
      t.text :description
      t.references :publication_type
      t.integer :publisher_id
      t.string :publisher_type
      t.boolean :single_issue

      t.timestamps
    end
    add_index :publications, :publication_type_id
  end
end
```

* Rollback features:
  * To create table: `bin/rails db:migrate`
  * To roll it back: `bin/rails db:rollback`

* More about migrations in [Active Record Migrations guide](https://edgeguides.rubyonrails.org/active_record_migrations.html)