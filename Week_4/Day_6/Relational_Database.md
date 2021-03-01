# Intro to Relational Database

### What is it?
A **relational database** is a type of database that organizes data into tablets, and links them, based on defined relationships.

These relationship enables you to retrieve and combine data from one or more tables with a single query.

## Normalization
* Process of removing reptitions across columns and rows by separating data into different tables, then choosing meaningful primary keys to link the tables together

* Final output: data cleanly organized according to the relational model

### Step 1: First Normal Form (1NF)
* Removing repetitive data across **columns**

* Coined by Edgar F. Codd, computer scientist who layed down the theoretical basis of relational databases

* Eg: Move the repeitive data into a different table

### Step 2: Second Normal Form (2NF)
* Removing repetitive data across **rows**

* After the split, each table has unique rows for users and data

### Step 3: Linking Tables with Keys
* To draw links between tables:
  1. Assign a primary key to a table
  2. Reference that primary key in other table to link it

* Primary key: an unique identifier to each row in a table

* Foreign key: the key that the current table is using to reference another table

#### Question: using a natural key or creating a new primary key for the table?

> What would happen if we use usernames as the primary key, but someone decides to change their username?

Depends on the system, for instance, if users are able to change their user handle, then assigning each user some numerical ID would make sense.


## Relational Database Management Systems (RDBMS)

* Software that allow us to create and use relational databases

* Commercial RDBMS:
  * Oracle Database
  * IBM DB2
  * Microsoft SQL Server

* Free and Open Source RDBMS:
  * MySQL - widely used in Internet companies
  * SQLite - common in embedded systems
  * PostgreSQL - useful for mapping applications

## Structured Query Language (SQL)

* Standard language for workin with RDBMSs

* Very similar to regular English sentences, but there are small variations in SQL between different RDBMS vendors => *SQL dialects*

* Just know: all SQL database systems supports the same fundamental SQL syntax