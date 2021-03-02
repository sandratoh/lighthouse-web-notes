# `SELECT` within `SELECT

## Nested `SELECT` statements

AKA *sub-query*

> The inner `SELECT` statement must be
> * returning **one column of value** only
> * not be null

## Using `ALL` with Nested `SELECT`

* Can use keyword `ALL`  to allow >=, >, <, or <= to act over a list

* Need condition>0 in sub-query if some data may be `null` for value

Example: Find countries that have a GDP greater than every country in Europe, some countries may have `null` GDP values
```sql
SELECT name
FROM world
WHERE gdp >= ALL (
                  SELECT gdp
                    FROM world
                   WHERE continent = 'Europe'
                        AND gdp>0
                                    )
AND continent != 'Europe'
```

## Correlated or Synchronized Sub-Query

Works like a nested loop:
* subquery only has access to rows related to a single record at a time in the outer query
* Relies on table aliases (`x` and `y`) to identify two different uses of the *same table*
  * One in the outer query
  * One in the inner query

SQLZoo 4/7: Find the largest country (by area) in each continent. Show continent, name, and area
```sql
SELECT continent, name, area
   FROM world x
 WHERE area >= ALL (
                    SELECT area
                      FROM world y
                    -- Where the correlated values are the same
                     WHERE y.continent = x.continent
                       AND area>0
                    );
```

SQLZoo 4/8: List each continent and name of the country that comes first alphabetically
```sql
SELECT x.continent, x.name
  FROM world x
 WHERE x.name <= ALL (SELECT y.name
                       FROM world y
                      /* Compare the country name of an instance from x with the country name of an instance from y if they share the same continent */
                      WHERE x.continent = y.continent
)
ORDER BY name;
```

SQLZoo 4/9: Find countries that belong to continents where all countries have a population <= 2500000. Show name, continent, and population
```sql
SELECT name, continent, population
FROM world x
WHERE 25000000 > ALL (
                      SELECT y.population
                      FROM world y
                      WHERE x.continent = y.continent
                      )
```

SQLZoo 4/10: Find countries that have populations more than three times that of any of their neighbours (in the same continent). Show countries and continents
```sql
SELECT name, continent
FROM world x
-- Where country's population >= 3* All other population
WHERE population/3 >= ALL (
                          SELECT y.population
                          FROM world y
                          WHERE x.continent = y.continent
                          -- exclude self country from the neighbours
                          AND x.name != y.name
)


```