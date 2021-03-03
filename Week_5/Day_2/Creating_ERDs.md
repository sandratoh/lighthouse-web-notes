# Tips to Creating ERDs

## Whiteboarding / Online ERD Software
* [draw.io](https://app.diagrams.net)
* Always design a database using an ERD before writing any codes

## Naming Conventions
* Use `snake_case` for table and column names

* Pluralize tables names
  * E.g. `students`, `assignment_submissions`

* Singluarize column names
  * E.g. `name`, `start_date`

* Call primary key `id`

* For *most* foreign keys use `<table>_id`
  * E.g `student_id`, `cohort_id`