# SQL Injection

### What is it?
* A common web hacking techniques which inject malicious codes into database via SQL statements

* When passing parameters to queries, **avoid string concatenating parameters into the query text directly**. This can and often leads to SQL injection vulnerabilites.

## Parameterized Query

* Separate SQL statement into two different parts
  1. The part that we write and we have control over
  2. The part that comes from somewhere else and might be malicious

* Send both parts as parameters to query

The part that we write - `$` placeholders:
```sql
const queryString = `
  SELECT students.id as student_id, students.name as name, cohorts.name as cohort
  FROM students
  JOIN cohorts ON cohorts.id = cohort_id
  WHERE cohorts.name LIKE $1
  LIMIT $2;
  `;
```

The values that come from somewhere else - place in array:
```sql
const cohortName = process.argv[2];
const limit = process.argv[3] || 5;
// Store all potentially malicious values in an array. 
const values = [`%${cohortName}%`, limit];
```

When query is ready to run, send both of these parts to the database:
```sql
pool.query(queryString, values);
```

> Always use parameterized queries when we have data that comes from an untrusted source, which is pretty much every source.