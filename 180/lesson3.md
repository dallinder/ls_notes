<h1>What is relational data?</h1>

* They are called relational because they persist data in a set of relations
  * Relation - table, which is a set of columns and rows.
  * If you can use something in the `FROM` clause of a `SELECT` statement it is probably a relation.

* Relationship is a connection between entities(rows of data), usually resulting from what those entities represent and how they are related to one another.

* Relation - usually another way to say 'table'
* Relationship - an association between the data stored in those relations.

<h1>Database Diagrams: Levels of Schema</h1>

* Three different levels of schema (abstraction):
  1. Conceptual
  2. Logical
  3. Physical

* Conceptual - high-level design focused on identifying entities and their relationships.

* Physical - Low-level database-specific design focused on implementation.

* Logical - Combination of conceptual and physical

* Entity-relationship model - this is talking about a conceptual schema.

* P - primary key
* N - Not NULL
* F - Foreign key

* One to Many
  * One side will have a primary key, and the many side will have foreign key that connects to it.

* Many to Many
  * When you have many to many relationship, there will be an extra table that represents that relationship
  * These tables are usually called join tables.
  * The number of tables in a Conceptual schema will not always match the number of tables in a physical schema

<h1>Cardinality and Modality</h1>

* Cardinality - number of objects on each side of the relationship
* Modality - if the relationship is required (1) or optional (0)

* Many times a one to one relationship will be actually be stored in the same table when the database is implemented.

* Notation styles:
  * Crows foot (one in the videos)
  * Chen's

<h1>A review of JOINs</h1>

* `INNER JOIN` - It needs to find a matching row in both tables in order to display it.
* `LEFT OUTER JOIN` - Want data from all the rows in the left table, only get values from right table if it matches the left table.
* `RIGHT OUTER JOIN` - Same as left, but with right tables.
  * More common to use `LEFT OUTER JOIN`
* Best to use most explicit name for the JOINs
* `CROSS JOIN` - Returns the Cartesian product. Every possible combination of 2 different tables.
  * Uncommon in production applications.

* `SELECT * FROM comments, users;` = CROSS JOIN
* `SELECT * FROM comments, users WHERE comments.user_id = users.id;` = `SELECT * FROM comments INNER JOIN users ON comments.user_id = users.id;`
  * The second is more explicit and specify how the tables are going to be joined.
  * Best to use the second way.

<h1>Using foregin keys</h1>

* Foreign Key can refer to two different, but related things:
  1. A column that represents a relationship between two rows by pointing to a specific row in another table using its primary key. A complete  name for these columns is foreign key column.
  2. A constraint that enforces certain rules about what values are permitted in these foreign key relationships. A complete name for this type of constraint is a foreign key constraint.

* To create a foreign key column, just create a column of the same type as the primary key column it will point to. `integer` to `interger`
, `text` to `text`.

* To create a foreign key constraint, there are two syntaxes that can be used. The first is to add a `REFERENCES` clause to the description of a column in a `CREATE TABLE` statement.

```sql
CREATE TABLE orders (
  id serial PRIMARY KEY,
  product_id integer REFERENCES products (id),
  quantity integer NOT NULL
);
```

* The second way is to add the foreign key constraint separately, just as you would any other constraint.

```sql
ALTER TABLE orders ADD CONSTRAINT orders_product_id_fkey FOREIGN KEY (product_id) REFERENCES products(id);
```

* One of the main benefits of using the foreign key constraints provided by a relational database is to preserve the referential integrity of the data in the database. The database does this by ensuring that every value in a foreign key column exists in the primary key column of the referenced table. Attempts to insert rows that violate the table's constraints will be rejected.

<h1>One to Many realtionships</h1>

* Normalization - the process of designing schema that minimize or eliminate the possible occurance of update, insertion, and deletion anomalies.
* The procedure of normalization involves extracting data into additonal tables and using foreing keys to tie it backto its associated data.
