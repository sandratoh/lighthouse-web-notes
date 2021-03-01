# SQL Intro Commands

## Making the table

#### Create a table
```sql
CREATE TABLE groceries (
  id INTEGER PRIMARY KEY
  , name TEXT
  , quantity INTEGER
  , aisle INTEGER
);
```

#### Insert data into table
```sql
INSERT INTO groceries VALUES (
  1
  , "Bananas"
  , 4
  , 7
);
```

## Querying the table

#### Get *all* the data from the table (`*`)
```sql
SELECT * FROM groceries;
```

#### Get specific data from the table, enter column name (eg: `name` column)
```sql
SELECT name FROM groceries;
```

#### Get data in specific order (`ORDER BY`):
```sql
SELECT * FROM groceries ORDER BY aisle;
```
#### Filtering out results (`WHERE`)
```sql
SELECT * FROM groceries WHERE aisle > 5 ORDER BY aisle;
```

## Aggregating data
**Aggregate function**: useful for things like getting the maximum, minmum, sum, or avg or data

#### Summing data (`SUM`)
```sql
SELECT SUM(quantity) FROM groceries
```

#### Summing by column
```sql
SELECT aisle, SUM(quantity) FROM groceries GROUP BY aisle;
```
1. Groups rows together by column name (`GROUP BY aisle`)
2. Sum up quantity in each of those group (`SUM(quantity)`)
3. Selected the first column value for all the groups (`SELECT aisle`)

**Best practice**: query the same variable as what you are grouping by