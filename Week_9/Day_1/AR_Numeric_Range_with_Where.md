# Using Numeric Conditions with Where

Read more [here](https://stackoverflow.com/questions/11317662/rails-using-greater-than-less-than-with-a-where-statement)

## Greater Than or Equal to

**Syntax**: `key: <lower_range>..Float::INFINITY`

```rb
User.where(id: 201..Float::INFINITY)
```
This is the same as

```sql
SELECT users.* FROM users  WHERE (users.id >= 201)
```

## Less Than or Equal to

**Syntax**: `key: -Float::INFINITY..<higher_range>`

```rb
Store.where(annual_revenue: -Float::INFINITY..1000000)
```

This is the same as

```sql
SELECT stores.* FROM stores WHERE (annual_revenue <= 1000000)
```

## >= vs >

### For discrete numbers
Use previous methods but +1 or -1 to get > instead of >=

Example: Looking for revenue less than 1 million (~ less than or equal to 999999)
```rb
Store.where(annual_revenue: -Float::INFINITY..1000000 - 1)
```

```sql
SELECT stores.* FROM stores WHERE (annual_revenue <= 999999)
```

### Inverted Logic
Utilizing logic: `x > y == !(x <= y)` and `where.not` chain

```rb
User.where.not(id: -Float::INFINITY..200)
```

same as

```sql
SELECT users.* FROM users WHERE (NOT (users.id <= 200))
```

### Arel Table
Creates an instance for the model/table

```rb
User.where(User.arel_table[:id].gt(200))
```

generate SQL

```sql
SELECT users.* FROM users WHERE (users.id > 200)
```

Specifics that's happening:
```rb
User.arel_table              #=> an Arel::Table instance for the User model / users table
User.arel_table[:id]         #=> an Arel::Attributes::Attribute for the id column
User.arel_table[:id].gt(200) #=> an Arel::Nodes::GreaterThan which can be passed to `where`
```