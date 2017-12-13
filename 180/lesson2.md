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

<html>
<tbody>
<tr>
<td><code>varchar(length)</code></td>
<td>character</td>
<td>up to <code>length</code> characters of text</td>
<td><code>canoe</code></td>
</tr>
<tr>
<td><code>text</code></td>
<td>character</td>
<td>unlimited length of text</td>
<td><code>a long string of text</code></td>
</tr>
<tr>
<td><code>integer</code></td>
<td>numeric</td>
<td>whole numbers</td>
<td>
<code>42</code>, <code>-1423290</code>
</td>
</tr>
<tr>
<td><code>real</code></td>
<td>numeric</td>
<td>floating-point numbers</td>
<td>
<code>24.563</code>, <code>-14924.3515</code>
</td>
</tr>
<tr>
<td><code>decimal(precision, scale)</code></td>
<td>numeric</td>
<td>arbitrary precision numbers</td>
<td>
<code>123.45</code>, <code>-567.89</code>
</td>
</tr>
<tr>
<td><code>timestamp</code></td>
<td>date/time</td>
<td>date and time</td>
<td><code>1999-01-08 04:05:06</code></td>
</tr>
<tr>
<td><code>date</code></td>
<td>date/time</td>
<td>only a date</td>
<td><code>1999-01-08</code></td>
</tr>
<tr>
<td><code>boolean</code></td>
<td>boolean</td>
<td>true or false</td>
<td>
<code>true</code>, <code>false</code>
</td>
</tr>
</tbody>
</html>
