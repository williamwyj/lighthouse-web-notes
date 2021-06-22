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
```javascript
  - if only one parameter get rid of parenthesis, if only one line of code get rid of curley brackets, get rid of return status and arrow directly.

* Refactor - use functions to make code blocks for reusability
           - separate code blocks to be less specific functions such that function should only have a single goal
