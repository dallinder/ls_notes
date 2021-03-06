<h1>The SQL Language</h1>

* SQL is a special purpose language. Only used for a very specific purpose: interacting with relational databases.

* SQL is a declarative language. Describes what needs to be done, but does not detail how to accomplish this objective.

* For the most part a SQL database engine selects the most efficient way to execute a query.

* SQL is really 3 langs in 1.
1. DDL (Data Definition Language) - relation structure and rules.
  * SQL Constructs - `CREATE`, `DROP`, `ALTER`
2. DML (Data Manipulation Language) - values stored within relations.
  * SQL Constructs - `SELECT`, `INSERT`, `UPDATE`, `DELETE`
3. DCL (Data Control Language) - who can do what.
  * SQL Constructs - `GRANT`

<h2>DDL: Data Definition Language</h2>

* What allows a user to create and modify the schema stored within a datatbase.

* Includes CREATE TABLE, ALTER TABLE, ADD COLUMN.

<h2>DML: Data Manipulation Language</h2>

* What allows a user to retrieve or modify the data stored within a database.

* Includes SELECT, INSERT, UPDATE, and DELETE.

<h2>DCL: Data Control Language</h2>

* Controlling the rights and access roles of the users interacting with a database or table.

<h2>Syntax</h2>

* SQL code is made up of statements.

* Statements are terminated by semicolon.

* Expressions in SQL can make use of operators and functions.

* `||` used to concatente strings.

* `lower(string)` makes a string lowercase.
  * `lower(SOMETHING)`

<h1>PostgreSQL Data Types</h1>

* `varchar(length)`
 * Type: character
 * Value: up to `length` number of characters
 * Example: `canoe`

* `text`
  * Type: character
  * Value: unlimited length of text
  * Example: `A long string of text`

* `integer`
  * Type: numeric
  * Value: whole numbers
  * Example: `42`, `-1423290`

* `real`
  * Type: numeric
  * Value: floating point numbers
  * Example: `24.563`, `-14924.3515`

* `decimal(precision, scale)`
  * Type: numeric
  * Value: arbitrary precision numbers
  * Example: `123.45`, `-567.89`

* `timestamp`
  * Type: date/time
  * Value: data and time
  * Example: `1999-01-08 04:05:06`

* `date`
  * Type: data/time
  * Value: only a date
  * Example: `1999-01-08`

* `boolean`
  * Type: boolean
  * Value: true or false
  * `true`, `false`

* `text` is specific to PostgresSQL and not part of SQL standard
* Using `text` is in many cases preferable to using `character(n)` or `varchar(n)`
* No performance difference with `varchar(n)`, improvement over `character(n)`

* `integer` can only store values between -2147483648 and +2147483647

<h2>NULL</h2>

* NULL represents nothing, absence of any other value.
* In SQL `NULL` will return `NULL` instead of true or false when used on either side of comparison operators.

* When dealing with `NULL` always use `IS NULL` or `IS NOT NULL` constructs.

<h1>Loading Database Dumps</h2>

* Files will contain a list SQL statements just as if they had been typed out manually.

* Two ways to load SQL files into a PostgresSQL database.

<h2>psql</h2>

```bash
$ psql -d my_database < file_to_import.sql
```

* This will execute the SQL statements with `file_to_import.sql` within `my_database`

* If you're already running a `psql` session, you can import a SQL file using the `\i` meta command.

```sql
my_database+# \i ~/some/files/file_to_import.sql
```

* To dump a database:

```bash
$ pg_dump -d database_name -t table_name --inserts > new_file.sql
```

* Three ways to use schema to restrict what values can be stored in a column

1. Data type (which can include a length limitation)
2. NOT NULL constraint
3. Check constraint


* A key uniquely identifies a single row in a database table.

* A natural key is an existing value in a dataset that can be used to uniquely identify each row in that dataset.

* Some values that seem like solutions: phone number, email addresss, social security, product number.

* Surrogate key is a value that is created soley for the purpose of identifying a row of data in a database table.

* The most common surrogate key is the auto-incrementing integer.

* Common to call a surrogate key created for a table `id`

```sql
-- This statement:
CREATE TABLE colors (id serial, name text);

-- is actually interpreted as if it were this one:
CREATE SEQUENCE colors_id_seq;
CREATE TABLE colors (
    id integer NOT NULL DEFAULT nextval('colors_id_seq'),
    name text
);
```

* Sequence is a special kind of relation that generates a series of numbers. A sequence will remember the last number it generated, so it will generate numbers in a predetermined sequence automatically.

* You can use `nexval` in a `SELECT` statement

* Once a number is returned by `nextval` for a standard sequence, it will not be returned again, regardless of whether the value was stored in a row or not.

```sql
CREATE TABLE more_colors (id serial PRIMARY KEY, name text);
```

* By specifying `PRIMARY KEY`, PostgreSQL will create an index on that column that enforces it holding unique values in addition to preventing the column from holding NULL values.

1. All tables should have a primary key column called `id`
2. The `id` column should automatically be set to a unique value as new rows are inserted into the table.
3. the `id` column will often be an integer, but there are other data types (like UUIDs) that can provide specific benefits.

* Do not have to declare a column `PRIMARY KEY`, but it's a good idea to do so.

* UUIDs - very large number that are used to identify individual objects or, when working with a database, rows in a database.

* Often represented with hexadecimal strings with dashes.

* SQL statement to make a new sequence: `CREATE SEQUENCE sequence_name`

<h1>How PostgreSQL Executes Queries</h1>

* Basic process for a `SELECT` query.


1. Rows are collected into a virtual derived table.
  * new temp table from all tables listed in `FROM` clause
2. Rows are filtered using `WHERE` conditions.
  * All conditionals are evaluated for each row, Those that don't meet the requirement are removed.
3. Rows are divided into groups.
  * If query include `GROUP BY` clause, remaining rows are divided into appropriate groups.
4. Groups are filtered using `HAVING` conditions.
  * `HAVING` conditions are very similar to `WHERE` conditions except that they are applied to values that are used to create groups and not individual rows.
  * A column that is mentioned in a `HAVING` clause should almost always appear in a `GROUP BY` clause and/or an aggregate function in the same query.
  * `HAVING` clause is used to filter aggregated/grouped data.
5. Compute values to return using select list.
  * Each element in the select list is evaluated, including any functions, and the resulting values are associated with the name of the column they are from, name of the last function evaluated, unless a different name is specified in the the query with `AS`
6. Limit results
  * If `LIMIT` or `OFFSET` clauses are included in the query, these are used to adjust which rows in the result set are returned.

<h1>Table and Column Aliases</h1>

* Joining multiple tables is a time when might need to using aliasing. Might have multiple columns named the same thing.

* Change name of table within a SQL query. Useful in longer, move involved queries.

* Use `AS` to make an alias.

* Don't want to alias table names unless you have to.
