# [William Wang]'s Notes
## Summary
This repository contains all of the notes take by [William Wang](https://github.com/williamwyj/) for the lighthouse labs Wed Development Bootcamp.

## Table of Contents
* [Week 1](/Week_1)
  * [Day 1](/Week_1/Day_1)
### Day 1
* How to add emoji in javascript: 
  * add emoji in quotes like string.
  * Control + command + space opens an emoji menu
* Process.argv: an array where [0] is a directory of the executable, [1] is the executed file name, [2 and onward] are pass in values
  * syntax [runtime] [file name] [argument1] [argument2] etc....
    eg. let variable = process.argv
        use input: node program.js argument1 argument2 //separated by spaces
* Template Literals
  * String concatenantion, syntax: use back ticks `, surround variable with ${variable}, eg:
  * ```javascript
    const name = 'Alice';
    console.log(`Hello, ${name}!`);
    ```javascript

### Day 2
* Francis, Vasiliy, Dom east coast instructor
* Andy, Christian west coast instructor

* Incremental Development
  * Code in steps, test each step

*git commands
  * git remote -v shows repo 
  * git branch -M main : rename current branch to main
  * git branch : shows current branch name
  * git remote add origin gitlink : link repo to local repo
  * git push -u origin main : push to origin repo, main branch, the -u enable future push not to list origin and main anymore
  * git checkout -b newbranchname : create and switch to new branch
  * git checkout main : switch back to main branch
  * git push origin newbranchname : push to github in new branch
  - merge branch to main
    * switch to the main branch by : git checkout main
    * git merge newbranchname

* Incremental Development
  1. Write sudo code or comments of logic first
  2. write code under each comment logic for what the comment requires
  3. use console.log frequently to check, eg. console.log('What this console log is for', variable/argument);
     * Console log description is to help identify what it is for, required to keep track of console log.
NaN is a number type, use isNan() function to check NaN

* function
  - function declaration : function functionName(parameter){}, this is hoisted 
  - function expression : const functionName = function(parameter){}, this is Not hoisted
  - function expression is prefered as will be using arrow functions later
  - best practice is only call funciton after it is declared.

```javascript
const someFct = numbers => {
}
```

  - if only one parameter get rid of parenthesis, if only one line of code get rid of curley brackets, get rid of return status and arrow directly.

* Refactor - use functions to make code blocks for reusability
           - separate code blocks to be less specific functions such that function should only have a single goal
### Day 3
## Outline
1. Primitive Data Types
2. Object Fundamentals
3. Functions and Objects
  * pass-by-value
  * Object methods

## Primitive Data Types
1.number (have upper and lower limit, bigger or smaller than this limit is bigint)
2.string
3.boolean
4.null 
5.undefined (default value for anything)
6.symbol (unique, dont auto convert strings)
7.bigint 

> Is there a difference between string and String?

in JS all primitives and Object have an Object wrapper. String.prototype.length

```javascript
var str = "test"
str.length

"test".length
```

Primitives are immutable.
Primitive data cannot be changed, but variables can be reassigned.
```
var x = "this is a string"
x.toUpperCase();
returns "THIS IS A STRING"
x = "this is a string"
x = x.toUpperCase();
x = "THIS IS A STRING"
```
## Object Fundamentals
> So what is an object?

Is an array an object? YES
is a function an object? YES

>An object is a value in memory which is referenced by an identifier. In JS objects can be thought of as a collection of properties.

### Examples of objects
1. "normal" objects (collections of key value pairs)
2. Functions (objects that are "callable")
3. Arrays (indexed collections)
4. null is an object? not technically true, a peculiarity in JS due to having to work with Java

```
const arr  = [1,2,3]
arr.test = "test"
console.log(arr)
[1,2,3, test: 'test]
```

> What are key value pairs?


eg. obj.key
> the . syntax is a shorthand, had limitation, it is literal, will take what comes after the . and convert it into a string.
  eg 
```
const obj = {
  "key" : "value"
  "another key" : "another value"
}

var variable = "key"
console.log(obj.variable]
```
will return undefined
```
console.log(obj[variable])
```
will return "value"
     
> if key name have a space in it, . syntax will not work becasue a space means something else.
  eg "another key" : "another value" cannot be called by obj.another key

> Object references
  - An object is a value in memory which is referenced by a an identifier
  - the name of an object is an identifier or reference that points to the actual object in memory.
  - when object name is passed into a function, a copy of the identifier is passed into the function and the copy identifier is manipulated in the function
  - But when refering to an property of the object, the actual object in the memory is accessed because the copy identifier points to the same object
  - when a primitive data type is passed into a function, the function creates a copy of the data itself, not an identifier.
```
const replace = function(ref) {
  ref = {} //this changes which object ref is pointing to
}

const update = function(ref) {
  ref.key = "newvalue" // this updates the key value in the object
}

let obj = {key : "value"}
update(obj) // obj still has its original value (unchanged)
replace(obj) // obj contents has changed
```
>Object methods

```

function setAge(age) {
  this.age = age
}

const person = {
  firstName: "Zola",
  
  lastName: "McAdie",
  
  getFullName : function() {
    return this.firstName + " " + this.lastName
  }
  
  setAge
}

console.log(person.getFullName())

console.log(person.age)

person.setAge(29)

console.log(person.age)
```
  - variables defined outside of the object can be defined as keys inside the object.
  - the "this." refers to the object the function will be called in, and create a new property for what is written after this.
  
>Iterating in Objects
  - because objects are not indexed like array, can not use for counter loop, can use for...of loop eg:
  - ```
    for (var planet in planetMoons) {
  // additional filter for object properties:
    if (planetMoons.hasOwnProperty(planet)) {
      //  ...
      }
    }
    ```
   - above used .hasOwnProperty to filter out properties or methods inherited from protoype chains.

### Day 4 - Callbacks!

## To Do
- [ ] Functions as values
- [ ] Function calling vs function passing
- [ ] Callbacks and higher order functions
- [ ] Anonymous functions
- [ ] Arrow functions
- [ ] Make our own higher order function

* [ ] Functions as Values
> key value pair, assignment of a value to a variable
> Functions
```javascript
//function declaration
  - function sayHello(name) {
      console.log(`hello there ${name}`);
    }
//function expression
  - const sayHello = function(name) {
      console.log(`hello there ${name}`):
    };
 ```
> function declaration does NOT get hoisted, and is prefered.
> In function declaration, functions are Values or Objects.
  -in this case, another variable can be assigned to the function value.

> Functions are objects, eg, add a key value pair to function.
> Functions can be stored into an array as an element. Or in objects as key value pairs.

* [ ] Function calling vs function passing
> Functions are first class, they are treated as Objects and can be used as such. 
> Functions can be an argument and passed into another function, this is call a callback, eg below.
```javascript
const runMyFunction = function(yourFunction) {
  console.log(yourFunction.toString());
  yourFunction('Elise');
};

const sayHellow = function(name) {
  console.log(`hello there ${name}`);
};

runMyFunction(sayHello);
```
> when a value or function does not have a variable assigned to it, it is called anonymous, call anonymous function inline, eg.
```javascript
myFunction(function(name) {
  console.log(name);
});
```
> as soon as a function finishes working, its content is garbage collected
> scope: conditional, loops are their own small scopes so variable declared inside are not available outside of them

* [ ] Arrow Functions
> shorter syntax
> 1. no need for the 'function' key word
> 2. if there is only a single argument passed in, can omit parens
> 3. if only one line of code, can omit curly braces
> 4. arrow functions without curly braces automatically return whatever is to the right of the arrow
> GOTCHA: if youre using the word 'this', you have to use a function keyword function.
```javascript
const sayHello = name => `hello there ${name}`;
  //content
//anonymous function as arrow function
name => `hello there ${name}`; 
  
```
* [ ] Make our own higher order function
```javascript
cont animalNoises = ['Oink', 'Moo', 'Meow', 'Bark, 'Oof', Nehhhh', 'Boww', 'Haaay', 'Quack'];

const whatTheAnimalDoes = (animalNoise) => {
  console.log(`the animal says "${animalNoise}");
};

const loopOverArray = (arr, behaviour) => {
  for (const element of arr) {
    behaviour(element);
}

loopOverArray(animalNoises, whatTheAnimalDoes);
```
* map, go thru an array, perform an action on each element, return an array of result for each element
* map => transformation on an array
* filter => removes elements from an array
* forEach => perform an operation on each element of an array
* reduce => takes an array and reduces it to a single value
```
const outMap = (arr, callback) => {
  const output = [];
  
  // iterate over the provided arr
  for (const element of arr) {
    // call the call back for each element of the array
    const returnVal = callback(element);
    //push the return value from the callback into output
    output.push(returnVal);
    }
  return output;
};

cont animalNoises = ['Oink', 'Moo', 'Meow', 'Bark, 'Oof', Nehhhh', 'Boww', 'Haaay', 'Quack'];

const mapped Array = ourMap(animalNoises, (animalNoise) => {
  return `only good animals say ${animalNoise}`;

//use js predeteremined methods
const builtInMap = animalNoises.map((animalNoise) => `the animal says ${animalNoise}`);
console.log(builtInMap);
});
console.log(mappedArray);

```
* filter

* Breakout - callbacks!

* To Do

*** Week 2

*** Day 1 - TDD with mocha and chai

* TDD => test driven development
 - Process that create test cases before developing the actual code, an iterative approach.
   1. Create an expected value and test against it, test fails
   2. write code so test passes
   3. refactor/clean code
 - Benefits
   1. help recognize what the results should be, help clarify what requirements are, help ask the questions
   2. help figure out different possibilities/edge cases, various pathways that our code may take.
   3. help make sure code works after modification, and identify new bugs introduced in the process of debugging.
   4. automate test, do not need to manually test after every modification. 
   5. save time, help remember all required test cases.
   6. help coordinator between team members, over the long time of developement.

* Error Handling
  - try catch block
```javascript
try{
//Do the job with potential risk
console.log(aaaaaa);
}
catch(error)
{
console.log(error.message);
console.log(error.name);
//Do whatever you want with the error
}

console.log('bb')
```
   -above code will result
     aaaaaa is not defined
     Reference error
     bb
   -code will stop execution as it arrive at an error, eg if a variable is defined
   -try catch block will continue to execute code despite the error.

* Require
  -Access other files, makes our code more modular
```
//operations.js
const add = (num1, num2) => {
}
const sub =....
const mul =....
module.exports = {add, sub, mul}; //<= this is called object destructuring
//calculator.js
const {add,sub,mul} = require(operations)
console.log(add(10,20))
console.log(sub(10,20))
```
  -eg numberOfVowels.js
```javascript
const numberOfVowels = (str) => {

}

numberOfVowels('pizza')
  
```
  - eg numberOfVowels_test.js
```javascript
const numberOfVowels = require('./numberOfVowels.js');
const assert = require('assert').strict //this make sure the assert is strict eg === and not ==, also all methods in the assert object.

console.log(numberOfVowels("pizza"));
```
```
console.log(assert.equal(1,2, 'Check equality of 2 numbers'));
```
  - assertion error is encountered when assertion fail (when actual !== expected)
  - above will print the assertion error, and the error message

** try and catch block
```javascript
const numberOfVowels = (str) => {
const vowels = 'aeiou';
let counter = 0;
for (const letter of str) {
  if(vowerls.includes(letter)) {
    counter++;
  }
}
return counter;
}

module.exports = numberOfVowels;
```
```javascript
const assert = require('assert').strict // use assert library in node
try{
  console.log(assert.equal(numberofVowels('pizza'),1,'check pizza has 2 vowels'))
//code here to test
}
catch(error)
}
  console.log(error.name, error.message) 
  console.log('Actual is ',error.actual, 'while exptect is: '.error.expected);
//code to manipulate the error, eg print out the error message
{

try{
  console.log(assert.equal(numberofVowels('sashimi'),3,'check sashimi has 3 vowels'))
//code here to test
}
catch(error)
}
  console.log(error.name, error.message, error.actual);
//code to manipulate the error, eg print out the error message
{
```

** mocha and chai
- mocha is the test frame work, while chai is the assertion library that can be used with mocha.
```javascript
npm install --save-dev mocha //install into the project folder, not the test folder
npm install mocha
mkdir test
//make a test.js file in the test folder
//change scripts 'test':'mocha' //'test' is the name of the test
npm run test //test is the name of the test, can be any string
npx mocha//npx execute npm packages, this is another way to run the test
```
* mocha
```javascript
const assert = require('assert').strict;
const numberOfVowels = require('../numberOfVowels')

//describe a feature(or function) in multiple different scenarios

describe('numberOfVowels', () => {
  it('there is 2 vowels in pizza', () => {
    assert.equal(numberOfVowels('pizza'), 2)
  })
  it('there is 3 vowels in sashimi', () => {
    assert.equal(numberOfVowels('sashimi'), 3)
  })
});
```

  - check array equal
```assert.deepEqual([1,2,3],[1,2,3]);```

* chai
```
npm install chai //in the project folder not test folder, chai is only for test, so no need for --save-dev, in the json file it is listed as dependencies, and not dev dependencies

const {expect} = require('chai');
const numberOfVowels = require('../numberOfVowels')

describe('numberOfVowels', () => {
  it('there is 2 vowels in pizza', () => {
    expect(numberOfVowels('pizza')).to.equal(2);
  })
  it('there is 3 vowels in sashimi', () => {
    expect(numberOfVowels('sashimi')).to.equal(3);
  })
});
```

*** W2D2 - Asynchronous coding

sample-robot.js
```javascript

const start = Date.now();
//Analogy: need this robot to be able to monitor its status while it is doing other actions, eg if it gets knocked over as it get up or walk so it can update itself and not carry on the predetermined activity while knocked down

function sleepFor(sleepDuration) {
  const nowObject = new Date ();
  //  console.log('nowObject:',JSON.stringify(nowObject));
  const now = nowObject.getTime();
  while(new Date().getTime() < now + sleepDuration) {
   /* do nothing */
  }
}

function doAction(name, duration,next = null/*set next to null if no parameter passed in/*) {
  const now = new Date();
  console.log(`${now.getTime() - start}: Starting ${name}`);
  setTimeout ( () => {
    console.log(`${then.getTime() - start}: Ending ${name}`);
    next();
  }, duration);
  //sleepFor(duration); <= a blocking action that absorbs time
}

//
// Look
//
const look = () => {
  doAction('Look',500,look);
};
//
// Get Up
//
const getUp = () => {
  doAction('Get Up',5000,walk);
};
//
// Walk
//
const walk = () => {
  doAction('Walk',8000,openTheDoor);
};
//
// openTheDoor
//
const openTheDoor = () => {
  doAction('Open The Door',3000,walkThroughTheDoor);
};
//
// walkThroughTheDoor
//
const walkThroughTheDoor = () => {

  doAction('Walk Through The Door',4000);
};

look();

getUp();


```
-function setTimeout(), schedule a function to run at a later time.

```javascript

function sleepFor(sleepDuration) {
  const nowObject = new Date ();
  //  console.log('nowObject:',JSON.stringify(nowObject));
  const now = nowObject.getTime();
  while(new Date().getTime() < now + sleepDuration) {
   /* do nothing */
  }
}

console.log('start');

const nameOfFunction = () => {
  console.log('monkey fuzz!');
};

setTimeout( nameOfFunction, 4444 ); // first parameter a function, second parameter time in millisecond of delay to call the function.

console.log('presleep');
sleepFor(10000); // will block the setTimeout code from running at its schedule
console.log('postsleep');

console.log('end');
```
>The setTimeout will execute after everything but without additional delay
>The event loop, it is only when the main thread finish, then scheduled tasks execute
>function definition only declare function and allocate memory but does not execute
>schedule program to run in the event loop, the data will only return to the call back that is called in the event loop, not the main thread.

*** W2D3 - internet

* Internet is a network of networks, its a protocal that allows your network of computers to connect to a back end system that can route individual computers on your network to individual computers on other networks. Open protocal that allows computers to connect through various different hardware
  - original made be DARPA, US military
* Web is set of software that is used on the internet
  - TCP - Transport Control Protocol
   - large messages are separated into small packets labeled with a sort order, each packet is sent to the internet, hops from place to place to the destination.
   - packets arrive at the destination to be sorted by the TCPIP layer software, put them back in order. happens at a software level in the OS.
   - packets does not need to take the same route
     - made this way to be optimally robust to nuclear attacks, redundency of travel path.
* DNS => Domain Name System
  - convert URL to IP address
  - 192.168.x.x means its guranteed packets would not be routed to the internet
  - 127.0.0.1 is the IP for the local machine or localhost
* Port
  - Port is also required to connect to server
  - a server machine typical host multiple server software. IP address is for a single machine. A port number is used to distinguish request to different servers on the same machine
** Chat server example
* server.js
```javascript
const net = require('net');
const port = 8088; /*port number 1024 can be used without admin, port 80 is typical non-encrypted web traffic*/

const connectedClients = [];

const broadcast = (message) => {
  //loop over all connect clients and write the message to each.
  for (let cClient of connectedClients) {
    cClient.write(message);
    console.log('sending!');
  }
};

const server = net.createServer();

server.on('connection', function(client){
  console.log(`Client has connected.`);
  connectedClients.push(client);
  client.write(`Welcome to my awesome server`!);
  
  client.on('data', function(message){
    console.log(`Message received from client: ${message}`);
    broadcast(message);
  }
  
  client.on('end', function(){
    console.log(`Somebody disconnected`);
  } // need to confirm original quote, syntax not correct.
});
//reaction function, on event 'connection' invoke call back function. This is scheduling the callback on the eventloop, in reaction to other things, 
//server.on or server.log order does not matter because they are asynchronous.
//there can be multiple clients connect to a server, for every client that connect, this code will execute

server.listen(port, function(){
  console.log(`Server is listening on port ${port}`);
});
```
* client.js

```javascript
const net = require('net');
const port = 8088;

const client = net.createConnection(
  {
    port : port,
    host : 'localhost'
  }
);

client.on('connect', function(){
  console.log(`Client is connected to the server.`);
});

client.on('data', function(message){
  console.log(`Server sent: ${message}`);
});

process.stdin.on('data', function(message){
  client.write(message);
})

client.on('end',function(){
  console.log(`client disconnected from server`); // this would be invoked if server is stopped, terminating the connection
})
```
* type anything in the terminal while a program is running is called 'standard input'
**URL
             
https:// www.google.com:80/search?q=bootcamp#montreal

'https://' = Protocal
'www' = sub-domain
'google.com' = domain name
'com' = top-level domain
':80' = port
'search' = path
'?' = query
'q=bootcamp' = parameters
'#montreal' = fragment

* http cat status code => a photo graph of a cat for each status code

***W2D4 Promise

- Per the profile generator assignment from Tuesday, using readline and call backs to display a series of questions and ask for reply each time will end writing a  'callback hell', where each additional rl.question is the call back of the previous rl.question function. This makes sure the sequance of the questions asked where only the next question is asked once the question was the answer for the previous question was received.
**Promise 
- Promise is a javascript Object that behaves in a certain wayy
  - Puts events on the event loop, either resolves or rejected. 
  - promist object can use `.then` key function
    - .then function takes in a function call back, where the single parameter is the return value of the promise that was completed and called the then.
    - the .then recognize its input function is not a promise and make it into a promise, where its own return value can be chain with the next .then call.
    - the .then only runs when its previous promise was successfully resolved, it is scheduled in the event loop regardless but wether it runs depend on the successful resolution of the previous promise
  - catch function in promise chain
    - .catch() will execute when a promise is rejected. 
    - .catch() is able to return a promise to continue the chain, however all .then and .catch are written and execute in sequance
 **Promise.all
```
const functions = require('./promise-generator');

const returnPromise = functions.returnPromise;
const returnRejectedPromise = functions.returnRejectedPromise;

const promiseOne = returnPromise(`one`,1500);
const promiseTwo = returnPromise(`Two`,5000);
const promiseThree = returnPromise(`Three`,3000);
const promiseFour = returnPromise(`Four`,4000);

 Promise.all(promises) //where promises is an array of promise objects
   .then((data) => {
   console.log('success:', data);
   })
   .catch((err) => {
   console.log('something was rejected!:',err);
   })
```
- ahove code returns a array of response for each resolved promises only after all promises resolved.
- above code will only resolve with .then after all promises in the array resolves as they were first  created
- above code will return error and not execute any .then
**Promise.race
- will run the .then for the first promise that resolves in the array of promises and does NOT get to the others.
- error catching, only will catch if the fastest promise resolve error
**Create my own promise
- A new promise can be created using the 'Promise' class
- The 'Promise' constructor takes a callback that accepts two functions as arguments:
  -'resolve': this call back is called when the operation has finished successfully
  -'reject': this call back is called if the operation failed (usually with the error)
```js
const myPromise = new Promise((resolve,reject) => {
//do something and resolve when finished or reject with an error
}
const returnRandomPromise = (value,delay = 1000) => {
  const num = Math.floor(Math.random()*2);
  if(num < 1) {
    return new Promise(resolve,reject)=>{
      setTimeout(()=>resolve(`yay! resolved!: ${value}`),delay);
  })
 }
 return new Promise(resolve,reject)=>{
  setTimeout(()=>reject(`doh! rejected: ${value}`),delay);
 })
}
```
*Class => class is a object template, syntax:
```js
new ObjectClass // this creates a new object from a predefined object class eg a Promise
```
***W2D5

**Class => class is an object template, it however CANNOT be used as an object itself

*new => this keyword for class will create a new Instance of the class, different instances are separate objects

*constructor => this key word set the default values of the class, arguments passed into the class when make a new instance are passed in here

```
class Pizza {

  constructor(size, crust) {
    this.size = size;
    this.crust = crust;
    this.toppings = ["cheese"];
  }

  addTopping(topping) {
    this.toppings.push(topping);
  }

}

let pizza1 = new Pizza('large','thin');
console.log(pizza1.toppings); // ["cheese"]
console.log(pizza1.size); // 'large'
pizza1.addTopping("mushrooms");
console.log(pizza1.toppings); // ["cheese", "mushrooms"]

```

*inheritance => build a new class based on an existing class, 
  - key word 'extends'
```js

// new class Student will inherit Person class, and add its own state or method.

class Student extends Person {
  // stays in Student class since it's specific to students only
  enroll(cohort) {
    this.cohort = cohort;
  }
}
```

*Super => invoke a method or property from the super-class(class that was inherited from) and insert into subclass
```js
class Person {
  constructor(name, quirkyFact) {
    this.name = name;
    this.quirkyFact = quirkyFact;
  }

  bio() {
    return `My name is ${this.name} and here's my quirky fact: ${this.quirkyFact}`;
  }
}

class Mentor extends Person {
  // Mentor bios need to include a bit more info
  bio() {
    return `I'm a mentor at Lighthouse Labs. ${super.bio()}`;
  }
}

const bob = new Student('Bob Ross', 'I like mountains way too much');
console.log(bob.bio());
```
>above code will result "I'm a mentor at Lighthouse Labs. My name is Bob Ross and here's my quirky fact: I like mountains way too much"

*getter and setter
 - getting, key word get, computes a value and set it to a property key.
  - defines a function where the return value of the function will equal to the value with property key = name of the function
 - setting, key word set, checks the value and sets a value to a property key
  - defines a function where a parameter is passed into the function, the parameter is checked and if conditionals passes, the parameter is set to a property key.

*** W2WE

** charactor encoding
  - UTF-8 is the most common encoding using on the web today, includes all reasonable languages humans use.

** DNS server
  - server chain:
    Root server > TLD(Top Leverl) > Authoritative > Resolving

*** W3D1

*** Web Servers 101

* TinyApp, URL shortener.
  - register an account
  - log in
  - input and url and return a shortened URL
  - list of generated url, edit and delete the list
** Web Servers
  - Application running on a computer that speaks HTTP
  - Serve up files/data, HTML, CSS, Javascript, JSON, XML
  - clients make requests, server responds (if possible)
** HTTP - Hyper Text Transfer Protocol
  - Built on top of the persistent TCP connection
  - request => response protocol, the server does nothing until a request comes in. (unlike the snek TCP assignment, where request like up, down, right, does not result in a response.
  * Find the computer
    - We need to know where the other computer is? < IP address, or url like google.com, localhost.
    - what port is it listening on? A machine can host multiply different servers, there are 65535 ports for every internet connection.
      - reservered ports , 443(reserved for secured HTTPS), 80 or 8080 is standard HTTP (unsecured)
  * Make a request
    - Request is made up of a verb and a path
    - Verb
      - Tells us what we want to do
        - GET => retrieve information
        - POST => create/update/delete something on the server.
    - Path
      - Tells us what we want to do it to
        - Follows the domain/host in the url (eg /users, /maps, /blogposts)
        - eg. www.amazon.ca <= the host, /products <= path
  * Receive a response
    - Response code
      - Indicate success/failure of the request
      - eg. 404 (not found), 200 (all good), 420(enhance your comm), 418(I am a teapot), 500(internal server error)
    - Response body (optional)
  * Node is made from the Chrome v8 engine, which is an interpreter for javascript.
    - nodejs.org
      - http.createServer([option][requestListener]) //<= square brackets means optional
  * Example web server
```js
const http = require('http');

const server = http.createServer((request, response) => {
  response.write('hello there');
});

server.listen(12345);

const server = http.createServer((request, response) => {
  console.log('request')
  const url = request.url;
  const method = request.method;
  
  // GET /home, POST /users
  const reqStr = `${method} ${url}`;
  console.log(reqStr);
  
  if (reqStr === 'Get /home') {
    response.write('you have visited the home page');
  } else if {reqStr === 'Get /about') {
    response.write('welcome to the about page');
  } else {
    response.write('resource not found');
  }
    
  response.write('hello there');
  response.end();
});

server.listen(12345);

```

** Express 
 - Fast, unopinionated, minimalist web framework for Node.js
   - unopinionated <= they do not have a say how users use their framework.
* initial express
 - npm init -y <= create a package.json file to manage packages
 - npm install express --save <= only save local dependency, Not globally, this is no longer needed, since npm now default to local depency and not global

```js
const express = require('express');
const app = express();
const morgan = require('morgan')
//morgan => HTTP request logger middleware for node.js, npm install morgan
//middleware

app.use((req,res) => {
  if(!req.cookies.loggedIn) {
    res.send('stopped by the middleware'); <= this will stop execution of the rest of the code
  }
  next();
});

app.use((req, res, next) => {
  //body parser
  //"username=jstamos&password=1234"
  req.body = {
    username : 'jstamos',
    password: '1234'
  };
  next(); <= means done with this middleware
});

app.use(morgan('dev'));

// add endpoints (VERB+PATH) => the order of the app.get matters, eg duplicate path with different response does not work, only the first response will ever work.

// GET /home
app.get('/home',(req, res) => {
  res.send(`you have visited the home page ${req.body.username}`);
});
// Get /about
app.get('/about', (req, res) => {
 res.send('welcome to the about page');
};

// tell our app to listen on a port
const port = 3333;

app.listen(3333, ()=> {
console.log(`app is listening on port ${port}`);
});
```

** Middleware 
 - code (in the form of a function) that runs between the request and the response.
 - fantastic for parsing (changing the input), body, cookies

request => middleware => route handler => middleware => response

code 304 => not modified, content have not changed sinced last visit, so can use content in memory instead of retreiveing the infomation again.
         =>command shift r to do hard refresh which does not use cache
code 400s => issue with request
code 500s => issue with server

*** W03D02 - CRUD with Express

**Implement CRUD over HTTP with Express
**Render data for the user using EJS template
**Use forms to submit HTTP requests
**Explore the Post-Redirect-Get pattern
**Using Chrome DevTools to see requests and responses
**Practice debugging Express

*CRUD === Create Read Update Delete
*BREAD === Browse(read all resource) Read(only read specific item in resource) Edit Add Delete


*ideas


```js
const express = require('express');
const morgan = require('morgan');
const port = 4567;

// in-memory

const app = express();

app.use(morgan('dev'));

app.listen(port, () => {
  console.log(`app is listening on port ${port}`);
});

```
