```js
const { Pool } = require("pg");
const pool = new Pool({
  user: "vagrant",
  password: "123",
  host: "localhost",
  database: "lightbulb",
});

const sql = "SELECT id, name FROM users LIMIT 5";
const promise = pool.query(sql);

const promise = pool.query(sql); // returns Promise { <pending> } because the command only put the promise into the event loop that will execute after the main thread is complete.
                                 // This promise begins executing asynchronously as soon as it is invoked here
                                 
promise.then(result = {     //this will log the result of the pool.query(sql) In this case the promise was already executed/resolved, and the .then() command works with the result
    console.log(result.rows);
})

const getUsers = function(){
  const sql = "SELECT id, name FROM users LIMIT 5";
  const promise = pool.query(sql);
  return promise;
};

const result = getUsers()
  .then(res => console.log(res));
console.log(result);

const getUsers = function(){
  const sql = "SELECT id, name FROM users LIMIT 5";
  const promise = pool.query(sql)
      .then(result => {
        console.log(result.rows);
      }
  return promise; // this will return undefined because there is no return from the .then(), only console.log in there
                  // the .then() will need to return a promise that will be used by the next .then()
};

const getUsers = function(){
  const sql = "SELECT id, name FROM users LIMIT 5";
  return promise = pool.query(sql);
    .then(result => console.log(result));
    .then(res => console.log(res)); // this will be undefined because the previous .then did not return
};

const getUsers = function(){
  const sql = "SELECT id, name FROM users LIMIT 5";
  return promise = pool.query(sql);
    .then(result => {
      console.log(result)
      return result;
    });
    .then(res => console.log(res)); // this will log result because it is returned from the .then() previous
    .catch(err => {
      console.log("catch:", err.message); //logs the error message, err itself is an object error information.
    })
};
```

```js

const axios = require('axios'); // like ajax to jQuery

const url = "http://api.kanye.rest";

axios.get(url)
  .then(res => {
    console.log(res.data);
  });
  .catch(err => {
    console.log(err.message);
  });
  .finally(()=>{ // will run regardless
  });

console.log("End of user thread!");

promise.all([promise1, promise2, promise3]); //takes an array of promises
  .then(res => {
  })
```
