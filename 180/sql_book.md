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

```bash
postgres=# SELECT name FROM people WHERE id = 1;
```

<p>SQL statements always terminate in a semi-colon.</p>
<p>Another way to write the above example:</p>

```bash
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

```bash
ls_burger=# SELECT * FROM orders;
```

<h2>Select All</h2>

* `select` = Identifies the type of statement being issued
* `*` = Wild card character that acts as an id for all the columns in a given.
* `FROM` = Another keyword. Used as clause within a `SELECT` statement to id the table which to retrieve the data.
* `orders` = This is the name of the table from which data is retrieved.

<h2>Select Columns</h2>

You can select multiple columns by comma-seperating the column names:

```bash
ls_burger=# SELECT drink, side FROM orders;
```

<h2>Select rows</h2>

Database tables often use a column such as an `id` column as a means if uniquely identifying a particular row of data. You can add where constraint with `id`, to return the data from all the columns for a row.

```bash
ls_burger=# SELECT * FROM orders WHERE id = 1;
```

`=` in SQL - In `WHERE` clause of SQL queries, = is treated as an 'equality' operator in that it compares things.

<h2>Selecting columns and rows</h2>

You can combine syntax for specifying columns and rows.

```bash
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

```bash
psql (9.5.3)
Type "help" for help.

sql_book=#
```

* Can use `\list` meta-command to see the current list of databases

* Can create database from psql console using the SQL statement `CREATE DATABASE`

```bash
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

```bash
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
 
```bash
yet_another_database=# DROP DATABASE another_database;
DROP DATABASE
yet_another_database=#
```
