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

### Primary and Foreign Keys
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
birth_date DATE // not gonna include age column because can calculate from birth_date
department_id INTEGER // ('IT','SALES','EXECUTIVE OFFICE', etc.) would be better to pull these values out and reference to them with user_id please see below

departments
----------------
id   SERIAL
name TEXT

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

### Naming Conventions
* Table and field names are written in snake_case
* Table names are always pluralized
* The primary key for each table will simply be called id
* A foreign key's name is the singular of the primary key's table appended with id(eg.user_id is the foreign key pointing to the id field in the users table)

### Data Types
* Each field in a table must have a data type defined for it
* The data type tells the database how much room to set aside to store the value and allows the database to perform type validation on data before insertion (to protect the data integrity of the table)
* Choosing the perfect data type is less of a concern nowadays because disk space is now comparably cheap
  * Postgre column types
    - Different data type have different preset constraints, storage sizes, etc.

### Relationship Types
* One-to-One: One record in the first table is related to one (and only one) record in the second table
* One-to-Many: One record in the first table is related to one or more records in the second table
* Many-to-Many: One or more records in the first table are related to one or more records in the second table

It could be argued that there is really only one relationship type: One-to-Many as One-to-One's extremely rare

### Design concepts - good practices, designs, for data base ease of use and easy maintenance, integrity
* Make fields required(add * after type or NOT NULL) if they represent the bare minimum for a row, eg in users example above, id,email,password would be required, maintains data integrity
* Intelligent default values can be set for fields (such as the current timestamp for a created_on field)
* Don't use calculated fields (a field that can be derived from one or more other fields, such as full_name is a combination is a combination of first_name and last_name)
* Pull repeated values out to their own table and make reference to them with a foreign key
* Try not to delete anything (use a boolean flag instead to mark a record as active or inactive)
* Consider using a type field instead of using two (or more) tables to store very similar data
(eg. create an orders table with an order_type field instead of a purchase_orders and a sales_orders table)
type CHAR('user','admin') // this defines the type to be 'user' or 'admin;'

### ERD diagram use app.diagrams.net

# W5D3 - SQL from our apps

- [ ] Connect a database
- [ ] Perform `BREAD` actions on database via command line app
- [ ] Demonstrate an SQL injection attack
- [ ] Server database content to the browser
- [ ] Protecting secrets with Environment Variables

### node-postgres

We are going to use node-postgres (`pg`) node package to interact with our database
In order to connect with our database, we pass configuration options to the `pg` client:

```js
const pg = require('pg)
```

## Connecting to a database
- npm init // to get a package.json file
- npm install pg 
- node index.js // return 'please enter a recognized verb'
- 
```index.js
require('dotenv').config(); //use .env file to hide config information
const pg = require('pg');

const Client = pg.Client;

//const configObj = {
//  user: 'postgres', //username is visible
//  host: 'localhost',
//  database: 'spot',
//  password: 'postgres', //password is visible
//  port: 5433 //database port that it is listening on
//};

const configObj = {
//  user: process.env.DB_USER,
//  host: process.env.DB_HOST,
//  database: process.env.DB_NAME,
//  password: process.env.DB_PASS, //password is hidden with dotenv
//  port: process.env.DB_PORT //password is hidden with dotenv
//};

// console.log('db connection info:', configObj);

const client = new Client(configObj);

client.connect()
.then(()=>{
  console.log('db connected');
})
.catch((err) => {
  console.log('db connection error:', err.stack); // if password incorrect, will return failed password authentication.
})

const verb = process.argv[2]

switch (verb) {
  case 'browse':
    client.query('SELECT id,question FROM objectives ORDER BY id;')//return a promise
    .then((response)=>{ //response is a Result (class from pg) object, rows is an array of objects containing the data
      console.log(browse query response rows: ', response.rows);
      client.end(); // ends the program
    })
    .catch((err) => {
      console.log('db browse query error:', err.stack);
      client.end(); 
    })
    break;
  case 'read':
    const id = process.argv[3];
    // client.query(`SELECT id,day_id,question,answer,type,sort FROM objectives WHERE id = ${id};`)// avoid using *, type out column names to be precise
    // if input is '50;DROP TABLE objectives', will return id 50 and delete the table
    client.query(`SELECT id,day_id,question,answer,type,sort FROM objectives WHERE id = $1;`,[id])//pg inherently have method to avoid SQL injection attack, query takes in 2 parameters, in the string, $1 refer to the first element in the array in the second parameter
    .then((response)=>{ 
      console.log(browse query response rows: ', response.rows);
      client.end(); 
    })
    .catch((err) => {
      console.log('db browse query error:', err.stack); 
      client.end(); 
    })
    break;
  default:
    console.log('please enter a recognized verb.');
    client.end(); // ends the program
    break;
}
```
## Setup Express server to work with sql database

```index-web.js
const express = require('express');
const app  = express();
app.set('view engine','ejs');

const dbFns = require('./db/queries');

app.get('/',(req,res)=>{
  dbFns.getAllObjectives((rows)=>{
    const templateVars = {rows: rows};
    res.render('home', templateVars);
  });
});

const PORT = process.env.PORT || 7878;
app.listen(PORT, ()=>{
  console.log(`Server is listening on port=${PORT}`);
})
```
```db/queries.js
const client = new Client(configObj);

client.connect()
.then(()=>{
  console.log('db connected');
})
.catch((err) => {
  console.log('db connection error:', err.stack); // if password incorrect, will return failed password authentication.
})

//
// DB Queries
//

const getAllObjectives = (cb)=>{
  client.query(`SELECT * FROM objectives;`)
  .then((response) => {
    cb(response.rows);
  })
  .catch((err)=>console.log('db getAllObjectives error:',err));
};

module.exports = {
  getAllObjectives
}
```
```home.ejs
<body>
<table>
  <%
  rows.forEach((item)=>{
  %>
  <tr>
    <td>
      <%= item.question%>
    </td>
    <td>
      <%= item.answer%>
    </td>
  </tr>
  <%
  })
  %>
</table>
<body>  
```
## Protecting secrets with Environment Variables
dotenv package
.env //file need to be in root directory where the express file is.
DB_USER=
DB_HOST=
DB_NAME=
DB_PASS=
DB_PORT=
