### W05D05 - Mid-term Project Kickoff

## Pick a project

# 1: Wiki Map
  * Interact with exterior map API, how to render map
# 2: The Quiz App
  * Very Data driven, intensive
# 3: Story Creator
  * Users contribute possible story, owner choose which one
  * Show off personallity
# 4: Decision Maker
  * Voting app, ranked choices
# 5: PasswordKeepR
  * No need to encrypt, can store passwords as plain text
# 6: Smart Todo List
  * Auto categorize todo based on user input
  * API heavy!
# 7: Resource Wall
  * Share info with other users
# 8: Buy/sell market place
  * Buy and sell
# 9: Schoodle
  * schedule events
# 10: Food pick-up ordering app
  * When order created, send text to restaurant. 
  * Both front and back end for user and restaurant

## User Stories
* describes how a user will interact with our app and also why
* Typical format, As a _______, I can______, because_____
* As a user, i can see a list of available maps, because I am interested in things in my area

## Identify the nouns
* Nouns are resources, eg users list maps
* They are to be turned into Tables and subsequently into ERD

## Routes
* create routes to resources, use REST architecture
* BREAD - eg maps
* Browse GET  /maps
* Read   GET  /maps/:id
* Edit   POST /maps/:id OR user method override PATCH /menuitems/:id
* Add    POST /maps
* Delete POST /maps/:id/delete

## MVP
* Minimum Viable Product
* What is the minimum-feature set that we think users will find useful

* Minimum Viable Demo MVD
* If you're not going to demo it, dont build it

## Wireframes/Mockups
* balsamiq, draw.io, moqups, pen && paper
* Copy design of other popular sites eg food for UberEats

### User Login/registration
* Don't do it

```js
// http://localhost:3000/login/2
app.get('/login/:id',(req,res)=> {
  //set the cookie
  res.cookie('user_id',req.params.id);
  //encrypted cookies
  req.cookie.user_id = req.params.id);
  
  res.redirect('/');
});
```

### Stack
* Front End - HTML, CSS, JS, JQuery, SCSS // focus on SCSS most likely to be used in actual job
* Back End - Node, Express, Postgres

## Boiler plate

## SPA vs Multipage
* Not mutually exclusive

## Git collaboration
* merge conflicts - two or more devs touch the same file
* merge locally or in the cloud?
* `git pull` multiple times a day

1. working on my branch
2. there's a new master
3. commit my branch
4. checkout master
5. pull master
6. checkout my branch
7. `git merge master`

## Communication


## Master
* Do not code on master/main

## elephantSQL
## CSS styles, recommand to use flexbox
