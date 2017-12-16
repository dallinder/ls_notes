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
