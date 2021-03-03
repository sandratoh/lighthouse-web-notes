# Data Manipulation Language (DML)

## What is it?
* SQL commands that let us interact with data

* Common DML:
  * `SELECT` => get data from tables
  * `INSERT` => add rows to a table
  * `UPDATE` => update rows w/i a table
  * `DELETE` => delete rows from table

## `INSERT` Query

Useful link: https://www.tutorialspoint.com/sql/sql-insert-query.htm

### Basic Syntax

Syntax 1: With column names
```sql
INSERT INTO TABLE_NAME (column1, column2, column3,...columnN)  
VALUES (value1, value2, value3,...valueN);
```

Syntax 2: Omit column names
```sql
INSERT INTO TABLE_NAME VALUES (value1,value2,value3,...valueN);
```

* May not need to specify the column(s) name if adding values for all columns of the table, but then need to make sure order of values is in the **same order** as columns in the table

* `SERIAL` and default values will still work if detail is omitted while doing `INSERT INTO` statements (must use syntax 1 and specify column names)

* `SERIAL` can only go UP, so if previous id is deleted, it won't replace that id, but give a new one with a higher value instead

### `SERIAL` Experimentations

**Experiment 1** - delete an id, and see the next auto insert id:
* Delete `id 1`
* Insert new data, not specifying `id`
* Output: table automatically gave `id 2` instead

**Experiment 2** - insert an id not in sequence with current database id
* Current table id goes up to `id 3`
* Insert new data jumping number by 1 with `id 5`
* Output: table gives `id 5` as input requested
* Insert new data not specifying `id`
* Output: table automatically give `id 4`, following original computation
* Insert: new data not specifying `id`
* Output: table error - conflicting primary key value (set to be unique)
* Insert again with same line not specifying `id`
* Output: table moves on and gives `id 6`

> **Experiment Summary:**
> * `SERIAL` will increase everytime table receives data
> * `SERIAL` will NOT replace deleted values
> * `SERIAL` will give error if computed value conflicts with existing value
> * `SERIAL` will move on and increase to the next value even if previous `SERIAL` operation fails

## `DELETE` Query

https://www.tutorialspoint.com/sql/sql-delete-query.htm

Basic Syntax
```sql
DELETE FROM table_name
WHERE [condition];
```
* Can combine N number of conditions using `AND` or `OR` operators

* Always include a `WHERE` clause when deleting, otherwise, will delete all records of table...

> Omiting `WHERE`clause when using `DELETE` will delete all records in table

## `UPDATE` Query

https://www.tutorialspoint.com/sql/sql-update-query.htm

Basic Syntax
```sql
UPDATE table_name
SET column1 = value1, column2 = value2...., columnN = valueN
WHERE [condition];
```
* Can combine N number of conditions using `AND` or `OR` operators

* Removing `WHERE` clause will update all records