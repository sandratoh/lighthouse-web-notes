# Data Definition Language (DDL)

## What is it?
* SQL commands used to define the database schema

* Common DDL statements:
  * `CREATE` => create
  * `ALTER`  => modify
  * `DROP`   => remove

## Postgresql Tutorials/Cheatsheets
* Data types:
  * https://www.postgresql.org/docs/9.3/datatype.html
  * https://www.postgresqltutorial.com/postgresql-data-types/

* Alter table: 
  * https://www.postgresqltutorial.com/postgresql-alter-table/ 

## Creating Tables
* Must set primary key

* Number data types:
  * `SMALL INT`
  * `INTEGER`
  * `BIG INT`
  * `DECIMAL`
  * `NUMERIC`
  * `REAL`
  * `DOUBLE`
  * `SMALLSERIAL`
  * `SERIAL`
  * `BIGSERIAL`

### Auto Incrementing / Serial
* For anything that needs to be *one more than the previous entry* (e.g `id`), instead of manually managing it, can get database to do it

* Each DBMS has own way of doing it

* In postgresql : set `id` to be `SERIAL`
  * SERIAL: *pseudo-type* that sets column to be a `NOT NULL INTEGER`and **automatically increments**
  * *Note*: `SERIAL` is not a real type, just a convenience/shorthand, so can NOT add it to column after table is created, need to be set from the start

### Foreign Key
* `REFERENCES` primary key from other table

* If other table's primary key was set using `SERIAL` - same as `INTEGER NOT NULL` for foreign key

* `ON DELETE CASCADE` - Delete data every time foreign key gets deleted

## Altering Table
* Basic syntax

```sql
ALTER TABLE table_name action;
```

* Avaialble actions include:
  * Add a column
  * Drop a column
  * Change data type of a column
  * Rename a column
  * Set/Drop default value for column
  * Add constraint to a column (e.g: `NOT NULL`, `ADD CHECK`)
  * Rename a table

## Dropping Table
* If we have multiple tables in database, `CASCADE` will make sure all records from other tables that depend on this table will also be deleted.

* Good practice to make sure table exists before dropping it - avoids sql error

```sql
DROP TABLE IF EXISTS table_name CASCADE;
```