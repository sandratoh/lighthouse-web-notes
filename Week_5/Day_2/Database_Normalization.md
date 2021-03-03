# Database Normalization

## Intro
* Database normalization definition: process of making the data in a database available in the most organized way possible

* Concept of *normal forms*: describe how organized the info is in the database. It enables the most straightforward approches for searching across info.

## Why should we normalize data?
* reduce duplicate data

* **Denormalized** database - store same information in several places

* To normalized database - split data into related tables

> It is *normal* to create more tables when normalizing a database.

## Normalization Process

Things to consider when normalizing a database:
1. Are there any internal redundancies in the database?
2. Are the dependencies across the different tables in the database logically organized?

### First Normal Form

* No repeated information across multiple columns

* Table organized into rows

* Each row has an unique primary key

* May have redundant info across multiple rows, but each rows will be unique

### Second Normal Form

* Split out redundant info into an independent table

* Match data up using foreign keys

* No repeated information across rows

### Third Normal Form

* Make sure non-key elements in each table provides info about the key in the row

* Create unambiguous unique primary key for each table

### Fourth Normal Form

* Table should not have any **Multivalued Dependencies**

* Should be in **Boyce-Codd Normal Form** (3NF)