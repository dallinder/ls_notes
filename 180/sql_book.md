<h1>SQL Book Notes</h1>

<h2>Introduction</h2>
<p><b>Relational Database</b> is a database organized according to the relational model of data.</p>
<p><b>Relational Model</b> defines the set of relations(which we can think of as analogous to tables) and describes the relationships, or connections between them in order to determine how the data stored in them can interact.</p>
<p>Using a relational database helps us cut down on duplicated data and provides a much more useful data structure.</p>
<p><b>Relational database management system (RDBMS)</b> is essentially a software application, or system, for managing relational databases.</p>
<p>A RDBMS allows a user, or another application, to interact with a database by issuing commands using sytax that conforms to a certain set of conventions or standards</p>
<p><b>SQL</b><em> - Structured Query Language</em> is the programming Language used to communicate with a relational database.</p>
<p>SQL uses simple English sentences</p>
<p>SQL is a declarative langauge; you describe <em>what</em> needs to be done, but not exactly <em>how</em> to do it.</p>

<h2>Vocab</h2>
<ul>
  <li><b>Relational Database</b> - A structured collection of data that follows the relational model</li>
  <li><b>RDBMS</b> - Relational Database Management System. A software application for managing relational databases</li>
  <li><b>Relation</b> - A set of individual, but related data entries; analogous to a database table</li>
  <li><b>SQL</b> - Structured Query Langauge</li>
  <li><b>SQL Statement</b> - A SQL command used to access/use the database or the data within that database SQL languange.</li>
  <li><b>SQL Query</b> - A subset of a "SQL Statment". A query is a way to search, or lookup, data within a database, as opposed to updating or changing data</li>
</ul>

<h2>Interacting with a database</h2>
<p>One thing all interfaces have in common is the underlying architecture they use to interact with the database: they issue a request, or declaration, and receive a response in return. "Client-Server" architeture.</p>
<p>Commonly used PostgreSQL client applications</P>
<ul>
  <li>createdb</li>
  <li>dropdb</li>
  <li>pg_dump</li>
  <li>pg_restore</li>
  <li>pg_bench</li>
</ul>
  * `psql` console is essentially a REPL; like IRB
<p>You can call client applications from terminal, not the `psql` prompt</p>
<p>Uses the native user account to determine who is connecting to it</p>
<p>Two different types of commands you can issue from the psql console prompt:</p>
<ol>
  <li>You can issue psql console meta-commands</li>
  <li>You can run SQL queries using standard SQL syntax</li>
</ol>
<h3>Meta-Commands</h3>
<p>syntax or a psql console meta-command is `\` followed by the command and any optional arguments. Example: `\conninfo`</p>
<p>Can be used for a number of different things. Connecting to a different database, listing tables, describing the structure of a particular table, setting environment variables, etc...</p>
* `\q` => quits the psql console
<h3>SQL Stataements</h3>
<p>SQL statements are commands issued to the database using SQL syntax.</p>

```sql
postgres=# SELECT name FROM people WHERE id = 1;
```

<p>SQL statements always terminate in a semi-colon.</p>
<p>Another way to write the above example:</p>

```sql
postgres=# SELECT name
FROM people
WHERE id = 1;
```

<p> `SELECT` statement => used to retrieve data from a database</p>
<h3>SQL Sub-languages</h3>
<ul>
  <li>DDL: Data Definition Language. Used to define the structure of a database and the tables and columns within it.</li>
  <li>DML: Data Manipulation Language. Used to retrieve or modify data stored in a database. `SELECT` queries are part of DML</li>
  <li>DCL: Data Control Language. Used to dtermine what various users are allowed to do when interacting with a database.</li>
</ul>

<h1>SQL Basics</h1>

```sql
ls_burger=# SELECT * FROM orders;
```

<h2>Select All</h2>

* `select` = Identifies the type of statement being issued
* `*` = Wild card character that acts as an id for all the columns in a given.
* `FROM` = Another keyword. Used as clause within a `SELECT` statement to id the table which to retrieve the data.
* `orders` = This is the name of the table from which data is retrieved.

<h2>Select Columns</h2>

You can select multiple columns by comma-seperating the column names:

```sql
ls_burger=# SELECT drink, side FROM orders;
```

<h2>Select rows</h2>

Database tables often use a column such as an `id` column as a means if uniquely identifying a particular row of data. You can add where constraint with `id`, to return the data from all the columns for a row.

```sql
ls_burger=# SELECT * FROM orders WHERE id = 1;
```

`=` in SQL - In `WHERE` clause of SQL queries, = is treated as an 'equality' operator in that it compares things.

<h2>Selecting columns and rows</h2>

You can combine syntax for specifying columns and rows.

```sql
ls_burger=# SELECT customer_name FROM orders WHERE side = 'Fries';
```

<h2>Data vs Schema</h2>

Schema is concerned with the structure of the database.
Data is concerned with the contents of the database.

<h1>Create and View Databases</h1>

Steps to create a new database:

1. `$ createdb sql_book` - creates the database
2. `$ psql -d sql_book` - connect to the database via psql console
  * this opens the psql console and connects to the database specificed by the `d` option
3. If you see this, everything is working correctly:

```sql
psql (9.5.3)
Type "help" for help.

sql_book=#
```

* Can use `\list` meta-command to see the current list of databases

* Can create database from psql console using the SQL statement `CREATE DATABASE`

```sql
sql_book=# CREATE DATABASE another_database;
CREATE DATABASE
sql_book=#
```

1. using `CREATE DATABASE` SQL command with `another_database` as the 'name' parameter for the command.
2. The `CREATE DATABASE` (without the prompt) on the second line is the response returned by PostgreSQL to let us know it has executed the statement successfully
3. Line 3, the prompt is back and we can issue another command.

* Convention is to use uppercase for SQL statements and lowercase for tables and databases.
* NOT case sensitive though.
* Name Parameter to `CREATE DATABASE` is mandatory. There are other optional parameters which set things like encoding, collation, connection limit, etc...

<h3>Database Naming</h3>
1. Try to keep database names self-descriptive.
2. Database names should be written in <b>snake_case</b>

<h2>Connecting to a database</h2>
* When in the psql console, you can connect to a different database using `\c` or `\connect` meta-commands (both do the same thing).

```sql
sql_book=# \c another_database
You are now connected to database "another_database" as user "User".
another_database=#
```
1. On the first line we use the meta-command `\c`, passing it to `another database`.
2. Line 2 informs what you are connected to.
3. Is the new prompt with the new database.

* Meta-commands, unlike SQL statements do not have ot be terminated with a semi-colon.

* `\c` and `\connect` meta-commands can take other arguments such as 'username', 'host', 'port', etc... When omitted, the command reuses the values from the previous connection.
* When connecting to a locally installed database, you can generally omit these other arguments.
* This type of connection is generally required whichever interface you are using to connect to a database, particularly when connecting to databases that are hosted remotely.

 <h2>Delete the Database</h2>

 * Use SQL command `DROP DATABASE`

```sql
yet_another_database=# DROP DATABASE another_database;
DROP DATABASE
yet_another_database=#
```

* Use `dropdb`

```sql
$ dropdb yet_another_database
```

* `DROP DATABASE` and `dropdb` are permanent and cannot be reversed.

<h1>Create and View Tables</h1>
<h2>Table Creation Syntax</h2>
`CREATE TABLE` SQL statement to create a table
```sql
CREATE TABLE some_table();
```

* inside the parenthesis is where you put column information
* each column is written on a separate line, separated by comma.

```sql
CREATE TABLE table_name (
  column_1_name column_1_data_type [constraints, ...]
  column_2_name column_2_data_type [constraints, ...]
  .
  .
  .
  constraints
);
```

* Column names and data types are a required part of each column definition. Constraints are optional.
* constraints can be defined either at the column level or the table level.
<h2>Creating a `users` table</h2>
SQL statement to create a table, named users, using `CREATE TABLE` statement.
```sql
sql_book=# CREATE TABLE users (
  id serial UNIQUE NOT NULL,
  username CHAR(25),
  enabled boolean DEFAULT TRUE
  );
```
1. `CREATE TABLE`: Firstly, `CREATE TABLE users` is the primary commands
2. `users`: The name of the table that will be created.
3. `()`: The information in the parentheses is related to the columns in the table.
4. `id, username, enabled`: The 3 columns of the table.
5. `serial, CHAR(25), boolean`: These are the data types of the columns.
6. `NOT NULL, DEFAULT TRUE`: These are constraints.
7. Each column definition is comma separated, this is the standard in any SQL database management system.

<h2>Data Types</h2>
* Data Type - classifies particular values that are allowed for that column.

* serial - used to created identifier columns for a PostgreSQL database. These ids are integers, auto-incrementing, and cannot contain a null value.
* char(N) - information stored in a column can contain strings of up to N characters in length. If a string less that than length N is stored, the remaining string length is filled with space characters.
* varchar(n) - information stored in a column can contain strings o up to N characters in length. If a string less than N characters is stored, then the remaining string length isn't used.
* boolean - can only contain two values 'true' or 'false'. In PostgreSQL, booleans are often displayed as t or f.
* integer or INT - a whole number.
* decimal(precision, scale) - takes two arguments. first is the max number digits to hold between 1 and 131072 (precision). second is the number of digits to the right of the decimal point to store.
* timestamp - contains both simple data and time in YYYY-MM-DD HH:MM:SS format.

<h2>Keys and Constraints</h2>
* Keys and constrains are rules that define what data values are allowed in certain columns. Important database concept and are part of a database's schema.
* UNIQUE: Prevents any duplicate values from being entered into that column.
* NOT NULL: when adding data to the table a value MUST be specified for this column, it cannot be left empty.
* DEFAULT: If no value is set when a record is created, then the value of `TRUE` is set in that field.

<h2>View the table</h2>
* `\dt` meta-command shows a list of all the tables, or relations, in a database.
* `\d` meta-command shows more detailed information about a table. `\d users` for example shows information about the `users` table.

`serial` is a special data type in PostgreSQL. It uses `integer` data type along with a `DEFAULT` constraint and a function called `nextval` which keeps track of the current highest value and increments this by one to be used as the next value.

<h2>Schema and DCL</h2>
* Although the information displayed by `\dt` and `\d` meta-commands is in a tabular format, it relates to the schema of the the database and not the data.

* Permissions are determined by DCL(Data Control Language)

<h1>Alter a Table</h1>
* Important to consider how schema changes will affect the data in a table.

<h2>Alter Table Syntax</h2>
* Existing tables can be altered with `ALTER TABLE` statement. `ALTER TABLE` is part of DDL, and is for altering schema only.
* Basic format of `ALTER TABLE` statment is:
* `ALTER TABLE table_to_alter HOW TO CHANGE THE TABLE additional arguments`

<h2>Renaming a table</h2>
* Tables can be renamed using the `RENAME` clause.
```sql
sql_book=# ALTER TABLE users
sql_book-# RENAME TO all_users;
ALTER TABLE
```

<h2>Renaming a column</h2>
* You can use `RENAME` clause to rename a specific column within the table.

```sql
sql_book=# ALTER TABLE all_users
sql_book-# RENAME COLUMN username TO full_name;
ALTER TABLE
```

<h2>Changing a columns datatype</h2>

```sql
sql_book=# ALTER TABLE all_users
sql_book-# ALTER COLUMN full_name TYPE VARCHAR(25);
ALTER TABLE
```

<h2>Adding a Constraint</h2>
* Form for adding a column constraint is:

`ALTER TABLE table_name ALTER COLUMN column_name SET CONSTRAINT CLAUSE`

* Form for adding a table constraint is:

`ALTER TABLE table_name ADD CONSTRAINT constraint_name CONSTRAINT CLAUSE`

<h2>Removing a Constraint</h2>
* Form for removing a column constraint is:

`ALTER TABLE table_name ALTER COLUMN column_name DROP CONSTRIANT`

* Form for removing a table constraint is:

`ALTER TABLE table_name DROP CONSTRAINT constraint_name`

<h2>Adding a column</h2>
* Example of adding a column:

```sql
ALTER TABLE all_users
  ADD COLUMN last_login timestamp NOT NULL DEFAULT NOW();
```

* Adding a new column is the same as the way we define a column when creating a table: Column name, data type, optional constraints.

* NOW() is SQL Function. It provides the current date and time when it is called.

<h2>Removing a column</h2>
* Example of removing a column:

```sql
sql_book=# ALTER TABLE all_users DROP COLUMN enabled;
ALTER TABLE
```

<h2>Dropping Tables</h2>
* Example of deleting a table:

```sql
sql_book=# DROP TABLE all_users;
DROP TABLE
sql_book=# \d all_users
Did not find any relation named "all_users".
```

* `DROP COLUMN` and `DROP TABLE` are not reversible.

<h2>Summary</h2>
Table that has all statements from this chapter: https://launchschool.com/books/sql/read/alter_table#summary

<h1>Inserting Data into a Table</h1>
* DML is a sub-langauge of SQL which incorporates the various key words, clauses, and syntax used to write Data Manipulation Statements.
* Data Manipulation Statements are used for accessing and manipulating data in the database. They can categorized into 4 different types.

1. `INSERT` statements - These add new data into a database table.
2. `SELECT` statements - Also referred to as Queries; retrieve existing data from database tables.
3. `UPDATE` statements - Update existing data in a database table.
4. `DELETE` statements - Delete existing data from a database table.

* The actions performed by these 4 types of statement are sometimes also referred to as CRUD operations.

* `CRUD` - CREATE, READ, UPDATE, and DELETE.

<h2>Insertion Statement Syntax</h2>
* General form of an `Insert` statement

```sql
INSERT INTO table_name (column1_name, column2_name, ...)
  VALUES (data_for_column1, data_for_column2, ...);
```

* When using an `INSERT`, we have to provide 3 key pieces of info.
1. The table name we wish to store the data in.
2. The names of the columns we're adding data to.
3. The values we wish to store in the columns listed directly after the table name.

* When inserting data into a table, you may specify all the columns from the table, just a few, or none. Generally best to specify which columns you want to insert data into.

* For each column you must specify a value for it in the `VALUES` clause, otherwise you'll get an error back.

<h2>Adding Rows of Data</h2>

<h3>Rows</h3>

* Columns give structure to a table, rows ('tuples') actually contain the data.

* Each row in a table is an individual entity and has a corresponding value for each column in the table.

<h3>Adding a Single Row</h3>

* Specify the columns into our `INSERT` statement.

```sql
sql_book=# INSERT INTO users (full_name, enabled)
sql_book-# VALUES ('John Smith', false);
```

* Order of the columns must match the order of the values to be inserted, but by specifying both columns and values, it is much easier to ensure that the order matches up correctly.

```sql
INSERT 0 1
```

* The first number is the `oid`, the 2nd is `count` of rows that were inserted.

<h3>Adding Multiple Rows</h3>

Example adding mulitple rows:

```sql
sql_book=# INSERT INTO users (full_name)
sql_book-# VALUES ('Jane Smith'), ('Harry Potter');
INSERT 0 2
```

* When we add multiple rows, PostgreSQL adds them in the order that we specified. So 'Jane Smith' id = 2, and 'Harry Potter' id = 3.

<h2>Constraints and Adding Data</h2>

<h3>Default Values</h3>
* Setting a `DEFAULT` value for a column ensure that if a value is not specified for that column in an `INSERT` statement, the nthe default value will be used.

<h3>NOT NULL Constraints</h3>

* Doesn't always makes sense for a column to have a default value. `NOT NULL` constraints can be used to ensure that when a new row is added, a value mus be specified.

<h3>Unique Constraints</h3>

* Sometimes we want to make sure that a value added for that column s unique.

* We can use `UNIQUE`

* `ALTER TABLE table_name ADD UNIQUE (column_name);`

* Having some sort of 'id' column in a database is common, and useful practice. Such a column is generally required to store a unique id for each row.

<h3>CHECK Constraints</h3>

* `CHECK` constraints limit the type of data that can be included in a column based on some condition we set in the constraint.

* `ALTER TABLE table_name ADD CHECK (expression);`

* Each time a new record is in the process of being added to a table, that constraint is first checked to ensure hat data being added conforms to it.

* `<>` is a not equal operator

* A string in PostgreSQL is a sequence of characters bounded by single quotes.

* For `'O'Leary'` to work it would have to be `O''Leary'`

<h1>Select Queries</h1>

* Querying data using `SELECT` forms the Read part of our CRUD operations.

<h2>Select Query Syntax</h2>

```sql
SELECT [*, (column_name1, column_name2, ...)]
FROM table_name WHERE (condition);
```

```sql
sql_book=# SELECT enabled, full_name FROM users
sql_book-# WHERE id < 2;
 enabled | full_name  
---------+------------
 f       | John Smith
(1 row)
```

* The order of the columns in the response is the order that the column names are specified in the query.

* we used the `id` column in the `WHERE` condition so it is used to filter our table, but we didn't specif id in the colmun list so the values in the column are not included in the results.

* We are told `1 row` is returned. This is the number of rows in the table that match the `WHERE` condition.

* `<` is a less than operator.

* It's better to try an avoid naming columns the same as keywords because it will cause an error. If you can't avoid it, use double quotes around the identifier.

<h2>ORDER BY</h2>

* Displays the results of a query in a particular sort order.

```sql
SELECT [*, (column_name1, column_name2, ...)]
FROM table_name WHERE (condition)
ORDER BY column_name;
```

```sql
sql_book=# SELECT full_name, enabled FROM users
sql_book-# ORDER BY enabled;

  full_name   | enabled
--------------+---------
 John Smith   |  f
 Jane Smith   |  t
 Harry Potter |  t
(3 rows)
```

* When ordering by booleans, `false` comes before `true` in ascending order.

* Since two of the rows have the same 'enabled' value, the sort order between those two rows is arbitrary.

* You can specify the sort direction, ascending (ASC) or decending (DESC). If omitted, then the default is `ASC`.

```sql
sql_book=# SELECT full_name, enabled FROM users
sql_book-# ORDER BY enabled DESC;

  full_name   | enabled
--------------+---------
 Jane Smith   |  t
 Harry Potter |  t
 John Smith   |  f
(3 rows)
```

* You can fine tune even further by having comma-seperated expressions in the `ORDER BY` clause.

```sql
sql_book=# SELECT full_name, enabled FROM users
sql_book-# ORDER BY enabled DESC, id DESC;

  full_name   | enabled
--------------+---------
 Harry Potter |  t
 Jane Smith   |  t
 John Smith   |  f
(3 rows)
```

* The above first sorts by enabled, then by id's.

<h2>Operators</h2>
<h3>Comparison Operators</h3>

| Operator     | Description              |
| :------------| :----------------------- |
| `<`          | less than                |
| `>`          | greater than             |
| '<='         | less than or equal to    |
| '>='         | greater than or equal to |
| '='          | equal                    |
| '<>' or `!=` | not equal                |

* Comparison predicates behave much like operators but have a special syntax.

* Examples: `BETWEEN`, `NOT BETWEEN`, `IS DISTINCT FROM`, `IS NOT DISTINCT FROM`, `IS NULL`, `IS NOT NULL`

* `NULL` is a special value in SQL that represents an unknown value.
* When identifying `NULL` values we must instead use the `IS NULL` comparison predicate.

```sql
SELECT * FROM my_table WHERE my_column IS NULL;
```

<h3>Logical Operators</h3>
* There are 3 logical operators:
1. `AND`
2. `OR`
3. `NOT`

* `NOT` is less commonly used. `AND` and `OR` operators allow you to combine multiple conditions in a single expression.

```sql
sql_book=# SELECT * FROM users WHERE full_name = 'Harry Potter' OR enabled = 'false';
 id |  full_name   | enabled |         last_login         
----+--------------+---------+----------------------------
  1 | John Smith   | f       | 2017-12-09 12:58:57.50925
  3 | Harry Potter | t       | 2017-12-09 13:02:49.055887
(2 rows)
```

<h3>String matching Operators</h3>
* String or pattern matching allows you to add flexibility to your conditional expressions in another way, by searching for a sub-set of data within a column.

* most often carried out with a `LIKE` operator

```sql
sql_book=# SELECT * FROM users WHERE full_name LIKE '%Smith';
```

* `%` - wildcard for any number of characters.
* `_` - wildcard for only a single character.

* An alternative for `LIKE` is `SIMILAR TO`, which uses Regex.

<h1>More on Select</h1>

* When working with large datasets, it is common to display only one portion of the data at at time.

* Displaying portions of data as separate 'pages' is a user interface pattern used in many web apps, generally referred to as 'pagination.'

* `LIMIT` and `OFFSET` clauses of `SELECT` are the base on which pagination is built.

* Below shows 1 row at a time.

```sql
sql_book=# SELECT * FROM users LIMIT 1;
```

* Below skips a row and then shows 1 row.

```sql
sql_book=# SELECT * FROM users LIMIT 1 OFFSET 1;
```

* You can use `LIMIT` to get a preview or taste of what data is available or would be returned rather than returning the entire dataset. Useful during development when forming your queries and getting an understanding of the dataset and data quality.


<h2>DISTINCT</h2>

* `DISTINCT` can be used as part of a `SELECT` query to return only distinct, or unique, values.

```sql
sql_book=# SELECT full_name FROM users;
 full_name   
--------------
 John Smith
 Jane Smith
 Harry Potter
 Harry Potter
 Jane Smith
(5 rows)
```

```sql
sql_book=# SELECT DISTINCT full_name FROM users;
 full_name
--------------
 John Smith
 Jane Smith
 Harry Potter
(3 rows)
```

* `DISTINCT` can be useful when used in conjunction with SQL functions.

```sql
sql_book=# SELECT count(full_name) FROM users;
 count
-------
     5
(1 row)
```

```sql
sql_book=# SELECT count(DISTINCT full_name) FROM users;
 count
-------
     3
(1 row)
```

<h2>Functions</h2>

* Functions can be grouped into the 3 most commonly used types:
1. String
2. Data/time
3. Aggregate

<h3>String Functions</h3>

* Perform some operation on values whose data type is a string.

* `length` - `SELECT length(full_name) FROM users;` - This returns the legnth of every users name. You could also use `length` in a `WHERE` clause to filter data based on name length

* `trim` - `SELECT trim(leading ' ' from full_name) FROM users;` - If any of the data in our `full_name` column had sopace in front of the name, using the `trim` function like this would remove the leading space.

<h3>Data/Time Functions</h3>

* `data_part` - `SELECT full_name, date_part('year', last_login) FROM users;` - allows us to view a table that only contains part of a user's timestamp.

* `age` - `SELECT full_name, age(last_login) FROM users` - `age` function, when passed a single `timestamp` as an argument, calculates the time elapsed between that timestamp and the current time.

<h3>Aggregrate Functions</h3>

* Aggregrate functions compute a single result from a set of input values.

`count` - Returns the number of values in the column passed in as an argument

`sum` - Not to be confused with count. Sums numeric type values for all rows being selected to return total.

`min` - This returns the lowest value in a column for all selected rows.

`max` - This returns the highest value in a column for all selected rows.

`avg` - This returns the average(arithmetic mean) of numeric type values for all the rows being selected.

* Aggregate functions really start to be useful when grouping table rows together.

<h3>GROUP BY</h3>

```sql
sql_book=# SELECT enabled, count(id) FROM users GROUP BY enabled;
 enabled | count
---------+-------
 f       |     1
 t       |     4
(2 rows)
```

* If you include columns in the column list alongside the function then those columns must also be include in a `GROUP BY` clause.  

<h1>Update data in a table</h1>

<h2>Updating Data</h2>

* `UPDATE` statement can be written with the following syntax:

```sql
UPDATE table_name SET [column_name1 = value1, ...]
WHERE (expression);
```

* `WHERE` clause in the example is optional. If omitted PostgreSQL will update every row in the target table.

* You can test your `WHERE` clause in a `SELECT` statement to check you which rows are being targeted, before using it in an `UPDATE` statement.

<h3>Update all rows</h3>

```sql
sql_book=# UPDATE users SET enabled = false;
UPDATE 5
```

* Ave sets all users to false in the enabled column

* `UPDATE 5` means we have updated 5 rows. This includes the row where `enabled` already had a value of false.

<h3>Update specific rows</h3>

* Using a `WHERE` clause lets us update only the specific rows that meet the condition(s) set in the clause.

```sql
sql_book=# UPDATE users SET enabled = true
sql_book-# WHERE full_name = 'Harry Potter' OR full_name = 'Jane Smith';
UPDATE 4
```

<h2>Deleting data</h2>

* `DELETE` statement is used to remove entire rows from a database table.

```sql
DELETE FROM table_name WHERE (expression);
```

<h3>Delete specific rows</h3>

```sql
sql_book=# DELETE FROM users
sql_book-# WHERE full_name='Harry Potter' AND id > 3;
DELETE 1
```

* `DELETE 1` tells us how many rows were deleted.

<h3>Delete all rows</h3>

* It's rare to do this. To do it, don't include a `WHERE` clause.

```sql
DELETE FROM users;
```

<h2>Update vs Delete</h2>

* `UPDATE` can update one or more columns within one or more rows by using `SET` clause

* `DELETE` can only delete one or more entire rows, and not particular pieces of data from within those rows.

* You can use `NULL` to approximate deleting specific values. `NULL` = unknown value.

```sql
UPDATE table_name SET column_name1 = NULL
WHERE (expression);
```

* A column with a `NOT NULL` constraint will throw an error.

<h1>Table Relationships</h1>

<h2>Normalization</h2>

* The process of splitting up data across different tables and creating relationships between them to remove duplication and improve data integrity is known as normalization.

* Two important things to remember about normalization for now:

1. The reason for normalization is to reduce data redundancy and improve data integrity.

2. The mechanism for carrying out normalization is arranging data in multiple tables and defining relationships between them.

<h2>Database design</h2>

* Database design involves defining entities to represent different sorts of data and designing relationships between those entities.

<h3>Entities</h3>

* An entity represents a real world object, or set of data that we want to model within our data base. We often identify major nouns of the system we're modeling.

<h3>Relationships</h3>

* Entity Relationship Diagram (ERD) - graphical representation of entities and their relationships to each other.

<h3>Keys</h3>

* Keys are special type of constraint used to establish relationships and uniqueness.

* They can be used to identify a specific row in the current table or refer to a specific row in another table.

<h4>Primary Keys</h4>

* Unique identifier for a row of data.

* To act as a unique identifier, a column must contain some data and that data should be unique to each row.

* Making a column a `PRIMARY KEY` is essentially equivalent to adding `NOT NULL` or `UNIQUE` constraints to that column.

```sql
ALTER TABLE users ADD PRIMARY KEY (id);
```

* Although any column in a table can have `UNIQUE` and `NOT NULL` constraints applied to them, each table can only have one Primary Key.

* Popular convention to use `id` column as a primary key.

<h4>Foreign Keys</h4>

* Allows us to associate a row in one table to a row in another table. This is done by setting a column in one table as a Foreign Key and having that column reference another table's Primary Key column.

* `REFERENCES` keyword.

```sql
FOREIGN KEY (fk_col_name) REFERENCES target_table_name (pk_col_name)
```

* A reference creating a connection between rows in different tables.

* Referential integrity is the assurance that a column value within a record must reference an existing value; if it doesn't then an error is thrown.

<h2>One to One</h2>

* A one-to-one relationship between two entities exists when a particular entity instance exists in one table, and it can only have one associated entity instance in another table.

* Example: A user can only have one address, and an address belongs to only one user.

* the `id` that is the `PRIMARY KEY` of the `users` table is used as both the `FOREIGN KEY` and `PRIMARY KEY` of the `addresses` table.

```sql
/*
one to one: User has one address
*/

CREATE TABLE addresses (
  user_id int, -- Both a primary and foreign key
  street varchar(30) NOT NULL,
  city varchar(30) NOT NULL,
  state varchar(30) NOT NULL,
  PRIMARY KEY (user_id),
  FOREIGN KEY (user_id) REFERENCES users (id) ON DELETE CASCADE
);
```

* The above SQL statement creates a new `addresses` table, and creates a relationship between it and the `users` table.

```sql
INSERT INTO addresses (user_id, street, city, state) VALUES
  (1, '1 Market Street', 'San Fransisco', 'CA'),
  (2, '2 Elm Street', 'San Fransisco', 'CA'),
  (3, '3 Main Street', 'Boston', 'MA');
```

* `user_id` column uses values that exist in the `id` column of the `users` table in order to connect the tables through the foreign key constraint.

<h3>ON DELETE clause</h3>
* Adding `ON DELETE` and setting it to `CASCADE` means that if the row being referenced is deleted, the row referencing it is also deleted.

<h2>On to Many</h2>

* Example: A book has many reviews. A review only belongs to one book.

```sql
CREATE TABLE books (
  id serial,
  title varchar(100) NOT NULL,
  author varchar(100) NOT NULL,
  published_date timestamp NOT NULL,
  isbn char(12),
  PRIMARY KEY (id),
  UNIQUE (isbn)
);

/*
 one to many: Book has many reviews
*/

CREATE TABLE reviews (
  id serial,
  book_id integer NOT NULL,
  reviewer_name varchar(255),
  content varchar(255),
  rating integer,
  published_date timestamp DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (id),
  FOREIGN KEY (book_id) REFERENCES books(id) ON DELETE CASCADE
);
```

* Key difference on the `reviews` table:

* Unlike the `addresses` table, the `PRIMARY KEY` and `FOREIGN KEY` reference different columns, `id` and `book_id`. This means that the `FORIEGN KEY` column, `book_id` is not bound by the `UNIQUE` constraint of our `PRIMARY KEY` and so the same value from `id` column of the books table can appear in this column more than once. In other words, a book can have many reviews.

<h2>Many to Many</h2>

* Example: A user can check out many books. A book can be checked out by many users (over time).

* Use two foreign keys and one primary key.

```sql
CREATE TABLE checkouts (
  id serial,
  user_id int NOT NULL,
  book_id int NOT NULL,
  checkout_date timestamp,
  return_date timestamp,
  PRIMARY KEY (id),
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE,
  FOREIGN KEY (book_id) REFERENCES books(id) ON DELETE CASCADE
);
```

<h1>SQL Joins</h1>

* JOINs are clauses in SQL statements that link two tables together, usually based on keys that defined the relationship between those two tables.

* Several types of JOINs: INNER, LEFT OUTER, RIGHT OUTER, FULL OUTER, and CROSS.

<h2>Join Syntax</h2>

```sql
SELECT [table_name.column_name1, table_name.column_name2,..] FROM table_name1
join_type JOIN table_name2 ON (join_condition);
```

* To join one table to another, PostgreSQL needs to know several pieces of information:

1. The name of the first table to join.
2. The type of join to use.
3. The name of the second table to join.
4. The join condition.

* The pieces are combined together using the `JOIN` and `ON` keywords.

* The part that comes after the `ON` keyword is the join condition.

* In most cases the join condition is created using the primary key of one table and the foreign key of the table we want to join it with.

* Creates a virtual table known as a join table.

<h2>Types of Joins</h2>

<h3>INNER JOIN</h3>

* Returns a result set that contains the common elements of the tables, i.e. the intersection where they match on the joined condition.

* Most commonly used JOIN type. PostgreSQL assumes INNER JOIN if you use the `JOIN` keyword.

```sql
SELECT users.*, addresses.*
FROM users
INNER JOIN addresses
ON (users.id = addresses.user_id);
```

<h3>LEFT JOIN</h3>

* Takes all the rows from one table, defined as the `LEFT` table, and joins it with a second table. The `JOIN` is based on the conditions supplied in the parentheses. A `LEFT JOIN` will always include the rows from the `LEFT` table, even if there are no matching rows in the table it is JOINed with.

```sql
sql_book=# SELECT users.*, addresses.*
sql_book-# FROM users
sql_book-# LEFT JOIN addresses
sql_book-# ON (users.id = addresses.user_id);
 id |  full_name   | enabled |         last_login         | user_id |     street      |     city      | state
----+--------------+---------+----------------------------+---------+-----------------+---------------+-------
  1 | John Smith   | f       | 2017-12-09 12:58:57.50925  |       1 | 1 Market Street | San Francisco | CA
  2 | Alice Walker | t       | 2017-12-09 13:02:49.055887 |       2 | 2 Elm Street    | Santa Fe      | NM
  3 | Harry Potter | t       | 2017-12-09 13:02:49.055887 |       3 | 3 Main Street   | Boston        | MA
  5 | Jane Smith   | t       | 2017-12-10 06:58:11.035029 |         |                 |               |
(4 rows)

```

<h3>RIGHT JOIN</h3>

* `RIGHT JOIN` is similar to a `LEFT JOIN`, execpt the roles are reversed.

```sql
SELECT reviews.book_id, reviews.content,
       reviews.rating, reviews.published_date,
       books.id, books.title, books.author
FROM reviews RIGHT JOIN books ON (reviews.book_id = books.id);

book_id |     content      | rating |       published_date       | id |       title        |   author    
---------+------------------+--------+----------------------------+----+--------------------+-------------
      1 | My first review  |      4 | 2017-12-10 05:50:11.127281 |  1 | My First SQL Book  | Mary Parker
      2 | Another review   |      1 | 2017-10-22 23:47:10.407569 |  2 | My Second SQL Book | John Mayer
      2 | My second review |      5 | 2017-10-13 15:05:12.673382 |  2 | My Second SQL Book | John Mayer
        |                  |        |                            |  3 | My Third SQL Book  | Cary Flint
(4 rows)

```

<h3>FULL JOIN</h3>

* Essentially a combination of `LEFT JOIN` and `RIGHT JOIN`

* Contains all the rows from both of the tables.

<h3>CROSS JOIN</h3>

* Returns all rows from one table crossed with every row from the second table.

* Since it returns all combinations, a `CROSS JOIN` does not need to match rows using a join condition, therefore it does not have an `ON` clause.

```sql
sql_book=# SELECT * FROM users CROSS JOIN addresses;
 id |  full_name   | enabled |         last_login         | user_id |     street      |     city      | state
----+--------------+---------+----------------------------+---------+-----------------+---------------+-------
  1 | John Smith   | f       | 2017-12-09 12:58:57.50925  |       1 | 1 Market Street | San Francisco | CA
  3 | Harry Potter | t       | 2017-12-09 13:02:49.055887 |       1 | 1 Market Street | San Francisco | CA
  5 | Jane Smith   | t       | 2017-12-10 06:58:11.035029 |       1 | 1 Market Street | San Francisco | CA
  2 | Alice Walker | t       | 2017-12-09 13:02:49.055887 |       1 | 1 Market Street | San Francisco | CA
  1 | John Smith   | f       | 2017-12-09 12:58:57.50925  |       2 | 2 Elm Street    | Santa Fe      | NM
  3 | Harry Potter | t       | 2017-12-09 13:02:49.055887 |       2 | 2 Elm Street    | Santa Fe      | NM
  5 | Jane Smith   | t       | 2017-12-10 06:58:11.035029 |       2 | 2 Elm Street    | Santa Fe      | NM
  2 | Alice Walker | t       | 2017-12-09 13:02:49.055887 |       2 | 2 Elm Street    | Santa Fe      | NM
  1 | John Smith   | f       | 2017-12-09 12:58:57.50925  |       3 | 3 Main Street   | Boston        | MA
  3 | Harry Potter | t       | 2017-12-09 13:02:49.055887 |       3 | 3 Main Street   | Boston        | MA
  5 | Jane Smith   | t       | 2017-12-10 06:58:11.035029 |       3 | 3 Main Street   | Boston        | MA
  2 | Alice Walker | t       | 2017-12-09 13:02:49.055887 |       3 | 3 Main Street   | Boston        | MA
(12 rows)
```

* Unlikely that you would use a `CROSS JOIN`.

<h3>Multiple Joins</h3>

* It is possible and common to join more than just 2 tables together. This is done by adding additional `JOIN` clauses to your `SELECT` statement.

* Example joining `users`, `checkouts`, and `books` tables.

```sql
SELECT users.full_name, books.title, checkouts.checkout_date
FROM users
INNER JOIN checkouts ON (users.id = checkouts.user_id)
INNER JOIN books AS b ON (books.id = checkouts.book_id);
```

<h2>Aliasing</h2>

* Sometimes queries get too long and you can use aliasing to shorten them.

```sql
SELECT u.full_name, b.title, c.checkout_date
FROM users AS u
INNER JOIN checkouts AS c ON (u.id = c.user_id)
INNER JOIN books AS b ON (b.id = c.book_id);
```

* You can shorten even more by leaving out `AS` keyword. `FROM users u`

<h3>Column Aliasing</h3>

* Can also use aliasing to display more meaningful information in our result table.

```sql
sql_book=# SELECT count(id) AS "Number of Books Checked Out"
sql_book-# FROM checkouts;
Number of Books Checked Out
-----------------------------
                          4
(1 row)
```

vs

```sql
sql_book=# SELECT count(id) FROM checkouts;
 count
-------
     4
(1 row
```

<h2>Subqueries</h2>

* Example: executing a `SELECT` query, and the using the results that query as a condition in another `SELECT` query.

```sql
sql_book=# SELECT u.full_name FROM users u
          WHERE u.id NOT IN (SELECT c.user_id FROM checkouts c);
  full_name
-------------
 Harry Potter
(1 row)
```

* `NOT IN` compares the current user id to all the rows in the result of the the subquery.

<h2>Subqueries vs Joins</h2>

* A differentiator between them may be their performance. As a general rule, JOINs are faster to run than subqueries.
