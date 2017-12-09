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
<p> `psql` console is essentially a REPL; like IRB</p>
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
<p> `\q` => quits the psql console</p>
<h3>SQL Stataements</h3>
<p>SQL statements are commands issued to the database using SQL syntax.</p>

```ruby
postgres=# SELECT name FROM people WHERE id = 1;
```

<p>SQL statements always terminate in a semi-colon.</p>
<p>Another way to write the above example:</p>

```ruby
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
