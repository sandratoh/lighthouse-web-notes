# Entity Relationship Diagram (ERD / ER Diagram)

### What is it?
A diagram that separates information you need from each table, and shows how each table relate to each other.

## Major Parts of ERD

1. Entity
2. Attribute
3. Primary Key
4. Relationship
5. Cardinality

### Entity
* A person, place or thing that you want to track in a database
* Becomes a **table** in the database
* Each occurence of entity becomes an entity instances (row of a table)

### Attribute
* Describe various characteristics about an individual entity
* Becomes the **columns** in the table
* Can be unique to student or not

### Primary Key / Identitifier
* An attriute or group of attributes that uniquely identifies an instance of the entity
* Like a special attribute that *has* to be unique to each entity instances
* Sometimes need a composite primary key instead of primary keys
  * Use a combination of data for an instance to create an unique identifier

### Relationship
* Describes how one or more entities interact with each other
* Usually a **verb**

### Cardinality
* The count of instances that are allowed or necessary b/w entity relationships

* Think of it this way:
  * Entities are tables
  * Instances of entites are rows of the table
  * Cardinality tells us how many rows we need from one table to link it to another table

* Minimum vs Maximum Cardinality
  * **Minimum**: minimum # of instances required
  * **Maximum**: maximum # of instances allowed

* Crow's Foot Notation
  * Way to represent cardinality in an ERD
  * Minimum: `one` vs. `many`
  * Maximum: `mandatory` vs `optional`
  * 4 ways to represent:
    * One - Mandatory  => must have at least one and only one instance
    * Many - Mandatory => must have at least one, but can have several instances
    * One - Optional   => don't have to have one, but if you do, can only have one
    * Many - Optional  => don't need to have one, but if you do, there's no limit