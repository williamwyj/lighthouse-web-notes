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
