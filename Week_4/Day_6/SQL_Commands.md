## `SELECT` basics

* `WHERE`   -> filter table
* `IN`      -> check if item is in a list
* `BETWEEN` -> range checking (inclusie of boundary values)

Example:
```sql
SELECT population FROM world
  WHERE name = 'Germany'

SELECT name, population FROM world
  WHERE name IN ('Sweden', 'Norway', 'Denmark');

SELECT name, area FROM world
  WHERE area BETWEEN 250000 AND 300000
```
## Pattern Matching Strings

* `LIKE` -> check items in table

* `%`    -> wild-card that can match any characters
  * Eg: `B%`    = starts with B
  * Eg: `%B`    = ends with B
  * Eg: `%B%B%` = has two B's

* `_`   -> single character wildcard
  * Eg: `_n%`   = second character is `n`

* `concat` -> add conditions together
  ```sql
  SELECT name
    FROM world
    WHERE capital LIKE concat(name, ' city')
  ```
  (Example finds the country where the capital is the country plus 'City')

  ```sql
  SELECT capital, name
    FROM world
    WHERE capital LIKE concat(name, '_%')
  ```
  (Example finds the capital and name where the capital is an extension of country's name)

* `REPLACE` -> returns occurances where one value is replaced by another

* `XOR` Operation -> Exclusive OR (either one or the other)
  ```sql
  SELECT name, population, area
  FROM world
  WHERE (area > 3000000 AND population < 250000000) 
  OR ( area < 3000000 AND population > 250000000)
  ```
* `ROUND` function -> round value to selected decimal places
  * positive values = decimals
  * negative values = nearest 10's
    (`ROUND(7253.85, 1)`  -> `7253.9`)
    (`ROUND(7253.85, -3)` -> `7000`)
    
  ```sql
  SELECT name, 
    ROUND(population/1000000, 2), 
    ROUND(gdp/1000000000, 2)
  FROM world
  WHERE continent = 'South America'
  ```
  (Example rounds to two decimal places in millions and billions)

* `LENGTH(s)` or `LEN(s)`- returns the number of characters in string `s`
  ```sql
  LENGTH('Hello') -> 5
  ```

  * Example: Show the name and capital where the name and the capital have the same number of characters.
    ```sql
    SELECT name, capital
    FROM world
    WHERE LEN(name) = LEN(capital)
    ```

* `<>` = **NOT EQUALS** operator

* `LEFT` function - isolate characters from start (specify value to how many letters)
  ```sql
  LEFT(name,1)
  ```
  Shows first character of name

* `NOT IN` - exclude from result (opposite of `IN`, same syntax)

## Useful Functions & Clauses

### Aggregates
Functions that can take many values and deliver just one value back
* `SUM`

* `COUNT`

* `MAX`

* `AVG`

### Distinct
* `DISTINCT` - remove duplicates from results returned by `SELECT` keyword

### Sorting queries
* `ORDER BY` - see result of a `SELECT` in any particular order

  * Ascending order: `ASC`

  * Descending order: `DESC`
  ```sql
  SELECT winner, yr, subject
  FROM nobel
  WHERE winner LIKE 'sir%'
  ORDER BY yr DESC, winner
  ```

* `GROUP BY` - groups rows that have the same values into summary rows

* `WHERE`  - filters rows before aggregates

* `HAVING` - filters rows after aggregates

Example: For each continent show the continent and number of countries with populations of at least 10 million.
```sql
SELECT continent, COUNT(name)
FROM world
WHERE population > 10000000
GROUP BY continent;
```

EXAMPLE: List the continents that **have** a total population of at least 100 million
```sql
SELECT continent
FROM world
GROUP BY continent
HAVING SUM(population) >= 100000000
```

## Joining Tables and Referencing Keys
```sql
-- selcting data from table 1 and joining table2
JOIN table2 ON table2.primary_key = table1.foreign_key
```
* Keywords: `JOIN` and `ON`

* Default to `INNER JOIN`

> If foregin key is `NULL`, the row will not be included in an `INNER JOIN`. In that case, we have to use an `OUTER JOIN`

* Types of `OUTER JOIN`
  1. `LEFT JOIN`  - can omit `OUTER`
  2. `RIGHT JOIN` - can omit `OUTER`
  3. `FULL`

Example
```sql
-- return all students b/c students is to the LEFT of JOIN
1. FROM students LEFT OUTER JOIN cohorts ON cohorts.id = cohort_id;

-- return all cohorts because cohorts is to the RIGHT of JOIN
2. FROM students RIGHT OUTER JOIN cohorts ON cohorts.id = cohort_id;

-- return all rows from both tables, even when there is no match
3. FROM students FULL OUTER JOIN cohorts ON cohorts.id = cohort_id;
```

Rearranging order of table to get the same result
```sql
1. FROM students LEFT JOIN cohorts ON cohorts.id = cohort_id;
2. FROM cohorts RIGHT JOIN students ON cohorts.id = cohort_id;
```

## Quotation Marks

> Rule of thumb:
> * Single quotes for arguments and parameters
> * Double quotes for column renaming

Example:
```sql
SELECT long-url, user_id AS "user identification number"
  FROM urls
  WHERE long_url LIKE 'www.g%.c%'
```

> Escaping single quotes:
> * use two single quotes within a quoted string

Example:
```sql
SELECT yr, subject, winner
FROM nobel
WHERE winner = 'Eugene O''Neill'
```

## Limit query result:
* `LIMIT ... OFFSET ...`