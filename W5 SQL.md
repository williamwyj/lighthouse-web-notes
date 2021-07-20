# W5D1 SQL

[ ]Why Databases
[ ]DBMS - Data Base Management System
[ ]Relational Databases
[ ]SQL

## Why Databases
  * Three Tiers of the Web Developement Architecture 
    - Client Tier
    - Logic Tier - web framework - workflow system
    - Data Tier - SQL - search engine - noSQL -....
## DBMS - Data Base Management System
  * A server that the logic backend server access as a client
## Relational Databases
  * Multiple tables that contain information and relate to each other.
## SQL (Structured Query Language)
  * Declarative Language (vs imperative)
    - We state only only we need
    - abstract how to get it
    - Grouped into DDL(data definition language) and DML(data manipulation language)
  * All Key words are CAPITALIZED, a guideline only depending on the DBMS, strongly recommanded to follow as best practice
  *  ; at end of query is very important since queries can be and usually are multiline.

### psql
: psql -U postgres -p 5433 spot // postgres is username, 5433 is port, spot is database name, /q to exit, /dt to show all tables

### SELECT statement
  SELECT column list, function(), function(), ...
  FROM table1
  INNER JOIN table2 // a way of connecting one table to another table
  ...
  ON table1.col1 = table2.col2
  ...
  WHERE criteria for row selection
  [AND criteria for row selection]
  [OR criteria for row selection]
  GROUP BY column list
  HAVING criteria  
### JOINS
  - There are many types of joins, best practice is be as specific as possible.
    * INNER JOIN, [LEFT||RIGHT] OUTER JOIN
    * The difference, if there is an empty column, should it be included?
  - INNER JOIN, A.key = B.key if A.key or B.key is blank, dont include that tables of row in the combination
    EG. SELECT day_description, question, answer FROM days INNER JOIN objectives ON day.id=day_id LIMIT 10;
    - when specify columns in a table, use table_name.column_name 
### ERD - Entity Relationship Diagram

# W5D2 - DATABASE

## Primary and Foreign Keys
* Primary Key : field values that uniquely identify a particular record within a table
* A PK must be unique (within the table) and can never be null
* A PK's data type is usually auto-incrementing integer (INTEGER or BIGINT)
* A Foreign Key is formed from field values that match a Primary Key stored in another table
* The Primary Key and Foreign Key MUST be the same data type

```sql
users
----------------
id        SERIAL //this means auto incrementing integer, will auto fill the next integer for every new row inserted
name      TEXT
email     TEXT
password  TEXT
logged_in DATE

blogs
----------------
id        SERIAL
title     TEXT
body      TEXT
user_id   INTEGER // foreign key

users
1. mickey, heMouse@disney.com, foryoureyesonly!, 2021-07-01
1. minnie, sheMouse@disney.com, foryoureyesonly!, 2021-07-01

blogs
1, How I Rose to Fame, "Lorem Ipsum etc.", 2
```

## Naming Conventions
* Table and field names are written in snake_case
* Table names are always pluralized
* The primary key for each table will simply be called id
* A foreign key's name is the singular of the primary key's table appended with id(eg.user_id is the foreign key pointing to the id field in the users table)
