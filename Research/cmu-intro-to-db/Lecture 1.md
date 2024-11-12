---
title: Relational Model and Algebra
tags:
  - rdbms
  - databases
  - cmudb
---
### Database Systems Background:
- what is a db ? clickhouse, imdb, dictionary
- clichkouse is a DB management systems, rest are database 
- Database -> organized collection of inter-related data that models some aspect of the real-world.
- Databases are the core component of most computer applications.
- Eg: create a db that models a digital music store to keep track of artists and albums 
- Info we ned to keep track of in our store:
	- Info about Artists 
	- The Albums those Artists released.


### Relational Model:

- The relational model defines a database abstraction based on relations to avoid maintenance overhead.
- Key tenets:
	- Store database in simple data structures(relations).
	- Physical Storage left up to the DBMS implementation.
	- Access data through high-level language, DBMS figures out the
	- best execution strategy.
- abstracted away the thing by the data and the query planner and abstracted away some more.
	- *Structure*: Definition of the database's relations and their contents independent of their physical representations.
	- *Integrity* -> Ensure the database's contents satisfy the constraints.
	- *Manipulation* -> Programming interface for accessing and modifying a database's contents. (relational algebra basically)
- Data Independence : Isolate the user/application from low-level data repr.
	 - The user only worries about high-level application logic.
	 - DBMS optimizes the layout according to opereating environment, database contents and workload.
	 - DBMS can then re-optimize the database if/when these factors changes.
	 - External schema (views) => virtual tables on top of actual tables.
	 - Logical Schema -> Schema/ Constraint (SQL)
	 - Physical Schema -> Pages,Files,extents etc.
- CODASYL couldnt do the physical data independence , which is obvious for every RDBMS now.
- Relational Model:
	- *relation* -> unordered set that contain the relationship of attributes that represent entities.
	- *tuple* -> set of atttributed values (aka its domain) in the relation.
		- values are (normally) atomic/scalar
		- special value NULL is a member of every domain (if allowed)
	- n-ary relation = Table with n columns 
- *Primary Keys*: A relation's primary key uniquely identifies a single tuple. 
- Some DBMS's automatically create an internal primary key if a table does not define one.
- DBMS can auto-generate unique primary keys via an identity column:
	- IDENTITY (SQL STANDARD)
	- SEQEUNCE (PostgreSQL/Oracle)
	- AUTO_INCREMENT (MySQL)
- Foreign Key: specifies that an attribute from one relation maps to a tuple in another relation.
	- Eg: mixed tables having multiple artists and want to track them 
	- maintain a seperate table that maps the artist_id to a album_id.
	- so the artist_id and album_id would the foreign keys from the respective tables.
- Constraints: User defined conditions that must hold for instance of the database.
	- can validate data within a single tuple or across entire relation(s)
	- DBMS prevents modifications that violate any constriant.
- Unique key and referentia(key) constraints which are the most common.
- SQL:92 standard supports global asserts, but these are rarely used(too slow).
	- Eg:
	```sql 
	create table artist (name varchar not null, year int, country char(60), check (year > 1900));
```

#### DML (Data Manipulation Languages):
- API that a DBMS exposes to application to store and retrieve information from a database.
- There are 2 types of DML:
	- Procedural(Relational Algebra)
		- Query specifies the high-level strategy to find the desired result based on sets/bags.
	- Non-Procedural (Declarative) (Relational Calculus)
		- Query specifies only what data is wanted and not how to find it.

### Relational Algebra 
- Relational algebra defines fundamental operations to retrieve and manipulate tuples in a relation.
	- Based on set algebra(unordered lists with no duplicates)

- Each operator takes one or more relations as its inputs and outputs a new relation.
	- we can "claim" operators together to create more complex operations.

- Operators:
	- 

### Alternative Data Models 





