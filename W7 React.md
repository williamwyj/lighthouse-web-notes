# W7D1 React

## What is react?
- Virtual Dom
  - React keep a copy of the real DOM in memory
  - Manipulating the REAL DOM is much slower than manipulating virtual DOM, because nothing gets drawn onscreen
    eg, time to insert on tweet in tweeter using JQuery, can create 10k objects in virtual DOM.
  - A change is made to the virtual DOM, react compare it to the real DOM, and patch the real DOM, not recreate the whole DOM like tweeter.
- Component
``` index.html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8"/>
    <title>Reacrt App</title>
  </head>
  <body>
    <div id="root"></div>
  <body>
</html>
```
``` index.js
import ReactDOM from 'react-dom';
import App from 'App';
//Webpack wont be able to detect changes to the App if in index.js, move App to its own App.js file for real development.



ReactDOM.render(<App />, document.getElementById('root')); //take element App, get element by Id 'root', two parameters, put the element App inside the 'root' container

//JQuery equivalant
const app = <div> Hello World</div>;
$('#root').append(app)
```
```App.js
export default function App() {

  return (
    <div className="App">
      Hello World
    </div>
  );
}
```

## Anatomy of React App
## Create a React app using npx
- npx will allow use npm without installing
- npx create-react-app my-app // create a new react app, installing a react development environment about 200MB, including webpack and babel.
- <noscript>You Need to enable JavaScript to run this app.</noscript>
  - reminds user to turn on JavaScript to run app, history, users used to disable JS for security.
- <React.StrictMode> =>StrictMode is a tool for highlighting potential problems in an application
- webapp, checks change in App.js and render change in react app.

## Components
- building blocks of application

## Anatomy of a Component
- A component is a function, functional components in React.
- functional components vs Class components
  - we will be using functinoal components, new and popular way
  - class components are original way
- a React component is a javascript function that returns JSX.

## JSX
- JS + HTML = JSX
- Babel => transpiler, translate JSX to javascript and html for browser to understanding
- when have more than one item in a component, or variale, must have a single parent
  - fragment => empty bracket <></> can use as a parent placeholder to complete the code
- use curly braces for variables inside markup in JSX
## Common Components
- Button
```
  const onClick = function() {
    console.log("Clicked");
  }
  <button onClick={onClick}>Click Me</button>
```
- Input
```
const [input,setInput] = useState("");

const onChange = function(event)  {
  setInput(event.target.value); //common pattern in react, the value in the input field, this is a state change and will result in re-render of the whole app function, with each input change, whole virtual dom was destroyed and a new virtual dom constructed with the change in input.
};
  <input type="text" value={input} onChange={onChange}/>
```
- List
  - Array, React can render a list of items in an array directly
```
  const listItems = [
      <li>Item 1</li>,
      <li>Item 2</li>
  ];
  <ul>
    {listItems}
  </ul>
```
## State
- Anything that can change on the page
- Hook: a prebuilt react function
```
const [data, setData] = useState([]);

setListItems([
  <li>Item 1</li>,
  <li>Item 2</li>
]);
```
- Use map to insert information into array
```
const testData = [
  {id:1, quote:"Random quote"},
  ...
]
const starArray = data.map(item=>{
  return <li>{item.quote}</li>
});

setListItems(testData); //set the data  arrayas testData

<ul>
  {starArray}
</ul>
```
- do all work outside of the return JSX

## Props & Attributes
  - only see props when there is more than one component.
  - props, pass the attributes when called on the component into the component
```input.js
import {useState} from "react";

const Input = function(props){
  const [input, setInput] = userState("");
  const [text, setText] = userState("");
  
  const onChange = function(event){
    setInput(event.target.value);
  }
  
  const onClick = function(){
    props.onClick(input);
  }
  
  return (
    <>
    <input type="text" value {input} onChange={onChange}/>
    <button onClick={props.onClick}>{props.buttonText}</button>
    </>
  );
};

export default Input;
```
```App.js
import Input from "./Input";

const onClick = function(input){
    setText(input);
}
<Input a='1', b='2', buttonText="Search" onClick={onClick}/>
```

# W07D02
- [ ] Recap: Components, props, and state
- [ ] Immutable Update Patterns with Arrays and Objects
- [ ] Updating Complex State

## Pizza place app and updating complex state
 - combine multiple states to one state so when the information need to be passed on, it is consolidated into one object or one state. 
 - Can also leave states separate, upto discretion of the developer, does not affect performance either way.
* React is now up to version react 17.0.2, no longer need to import React from 'react';
```header.jsx

// make components as generic as possible, do not store specific data in the component, do not use state in this component, move it up to parent
const Header = (props) => {
  
  return (
    <div>
      <h2>{props.message}</h2>
    </div>
    );
}
expost default Header;

// VisitorCounter.jsx

const VisitorCounter = () => {
  const [counter, setCounter] = userState(0);
  
  const clickHandler = () => {
    setCounter(counter+1);
    setCounter(counter+1);
    setCounter(counter+1); // these will update the counter by 1 only, since counter is declared as an const, in this instance of render, the counter is 0+1, react batch all three together and render them together, counter only update after re-render
    
    setCounter((latestValueForState) => {latestValueForState + 1});
    setCounter((latestValueForState) => {latestValueForState + 1});
    setCounter((latestValueForState) => {latestValueForState + 1}); //this will update the counter by 3, the setFunction always receive the latest value as an argument
   }
  return (
    <div>
      <h2>Visitor Counter</h2>
      <h2>Num visitors: {counter}</h2>
      // <button onClick={setCounter(counter+1)}>Click me!</button> // this is an infinite loop, each time a state is updated, page re-renders, so always use call back
      // <button onClick={() => setCounter(counter+1)}>Click me!</button> // this is not an infinite loop, 
      <button onClick={clickHandler}>Click me!</button>
    </div>
  );
}

// App.js
import Header from './components/Header';
import VisitorCounter from '/*...directory*/';
import { userState } from 'react';

const App = () => {
  const [heading, setHeading] = userState('Placeholder Value');
  
  return (
    <div className="App">
      <Header message={heading} />
    </div>
  );
}
```
```Pizza.jsx
import {userState} from 'react';

const Pizza = () => {
  //const [toppings, setToppings] = useState([]);
  //const [crustType, setCrustType] = useState('deep dish');
  
  const [pizza, setPizza] = useState({
    toppings : [],
    crustType : ''
  }); // do NOT set this to an empty object, for each render, may end up with undefined keys before keys are defined, prefine it a frame of the intended data structure
  
  const [newTopping, setNewTopping] = useState('');
  
  const updateCrust = (event) => {
    setPizza(prevPizza=> ({
      ...prevPizza,
      crustType: event.target.value
    }));
  };
  
  const addTopping = () => {
    toppings.push(newTopping); // do NOT do this, do not mutate state, set a brandnew state instead
    setToppings((prevToppings) ={
      return [
        ...prevToppings,
        newTopping
      ];
    }
    
    setPizza((prevPizza) => ({
      ...prevPizza,
      toppings: [
        ...prevPizza.toppings,
        newTopping
      ]
    }));
    })
    setNewTopping(''); // reset the input field to empty after button clicked
  }
  
  
  return (
    <div>
      <h2>Create your own pizza</h2>
      <div>
        <h2>Crust: {pizza.crustType}</h2>
        <label>New Crust:</label>
        <input
          value={pizza.crustType}
          onChange={updateCrust}
        />
      
      <div>
        <label>New Topping:</label>
        <input 
          value={newTopping}
          onChange={(event)=> setNewTopping(event.target.value)}
        />
        <button onClick={addTopping}>Add topping!</button>
      </div>
      
      <div>
        {toppings.map((topping, index)=> {
          return <h4 key={index}>{topping}</h4> //make a unique key for each element of the array to be rendered, the key is used internally by react, will not see it in the DOM, or be used by anyone other than REACT.
        })}
      </div>
    </div>
  );
};
export default Pizza;
```

## Immutable
  - We never want to change or mutate old state, because if old state and new state are the same, react will not re-render.

# Spread operator ...
  - spread the array into a list of values, ['Alice', 25] => ... => 'Alice', 25
```
const user = {
  name: 'Alice',
  age: 25,
  name: 'Carol' //this will overwrite the prior name key
  stomach: ['cheerios']
};

const copy = { //this makes a true copy of the object, instead of just a pointer, copy, that points to the same object. 
  ...user
};

copy.stomach.push('new breakfast');But the ... spread operator only copies shallow, so this will update user.stomach as well, solution is to use ... again

const copy = {
  ...user,
  stomach: [
    ...user.stomach
  ] // this will make a new array instead of copy over the pointer for the origin user.stomach
}
}
```
# W7D3 - Side effects & other data fetching

### To Do
- [ ] Rules for Hooks
- [ ] Pure Functions and Side Effects
- [ ] `useEffect`
- [ ] Cleanup
- [ ] Dependencies
- [ ] _useEffect_ Flow

### Rules of Hooks
* called in the same order (not conditionally)
* called inside React functions (components/custom hooks)
* hooks have to start with `use`

### Pure Functions
* no side effects
* always returns the same thing given the same arguments
* side effects are reaching outside the function for a value, change a value, does anything that is not the purpose of the function
```js

let additionValue = 2;

const addTwo = (num) => {
  const result = num + additionValue; //additionValue is defined outside of function, not passed in as input, therefore side effect
  additionValue++;//side effect
  console.log(result) // side effect
  return result;
};
```
* useEffect, react hook for side effect, put all side effects in here, does not return anything
  - executes on every single render
  - can NOT use with conditional eg if statement, use with dependency array. Watches the variable in the array, only render when the variable change in subsequent renders, alway run on first render
  - executes on the first render guaranteed, but only execute again is dependency array changes

* useState, when using a callback function, the parameter is the previous value eg. setState((prevValue)=> {function to set new value})

### React Renders UI -> Browser Display the UI -> Cleanup for previous Effects (if any) -> Run Effects for current render
```js
import {useEffect} from 'react';

const App = () => {
  
  const [counter, setCounter] = useState(0);
  const [searchTerm, setSearchTerm] = useState(0);
  
  useEffect(() => {
    document.title = `(${counter}) welcome to our site`;
    console.log('changed the document title');
  }, [counter, searchTerm]);// the dependency array, if anything in the array changes, this will execute
  
  useEffect(() => {
    setTimeout(()=>{
      console.log(`the current count is ${counter}`);
    }, 3000);
  });
  
  useEffect(() => {
    const interval = setInterval(()=>{ //interval execute every render, this is a memory leak, where interval keeps running long after page renders
      console.log(`the current count is ${counter}`);
    }, 3000);
    
    // clearInterval(interval); // this clears the interval as soon as it is call so no interval will appear
    
    return () => { // in a useEffect, the return function will execute before the new render, in this case clean up anything still executing from the last render
      clearInterval(interval);
      console.log(`interval cleared`); 
    }
  }, [counter]);
  
  return (
    <div className="App">
      <h2>useEffect Hook</h2>
      <h2>Count: {counter}</h2>
      <button onClick={() => setCounter(counter+1)}>Click me</button>
      
      <div>
        <h2>Search term: {searchTerm}</h2>
        <input
          value = {searchTerm}
          noChange = {(event)}
          
    </div>
  );
```
## Data fetching
* Axios, ajax package only, in lieu of JQuery which has front end function as well thats already covered by React
``` Appointments.jsx
import {useEffect} from 'react';
import axios from 'axios';

const Appointments = () => {
  
  const [appointments, setAppointments] = useState({}); //set this to an empty object, because on first render while get request is being process, page is still being rendered, where the .keys.length of the data is still being executed, set this to an empty object so it will not error out
  
  const [selectedAppt, setSelectedAppt] = useState(null);
  const [apptId, setApptId] = useState('');
  
  
  useEffect(()=>{
    //GET /api/appointments
    axios.get('http://localhost:8001/api/appointments')
      .then((response)=>{
        console.log(response.data);
        setAppointments(response.data); //without a condition array, this will result in infinite loop, but react cant catch it because it is async
      });
  }), []); //leave empty, if nothing changes then useEffect wont be called again, depend on nothing so leave it empty.
  
  useEffect(() => {
    const targetAppt = appointments[apptId];
    setSelectedAppt(targetAppt);
  },[apptId]);
  return (
    <div>
      <h2>All the Appointments</h2>
      <h2>Total Appointments: { Object.keys(appointments).length }</h2>
      
      <div>
        <label>Enter an Appt Id</label>
        <br/>
        <input
          value={apptId}
          onChange={(event) => setApptId(event.target.value)}
         />
      </div>
      
        { selectedAppt && ( //conditional render, only evalute the right side of the && when the left side is truthy
        <div> 
          <h2>Selected Appointment Information</h2>
          <h2>Interview #{selectedAppt.id} at {selectedAppt.time}</h2>
          { selectedAppt.interview && (
            <>
              <h2>Student:{selectedAppt.interview.student}</h2>
              <h2>Interviewer:{selectedAppt.interview.interviewer}</h2>
            </>
          )}
          
        </div>
        )}
      
      
    </div>
  );
);

export default Appointments
```
# W7D4 - custom hooks

## custom hooks
* All react must start with the prefix "use"
* can think of custom hooks as helper functions for React, but normal helper function cannot use React Hooks.
* Multiple instances of the same custom hook do not share state
* Custom hooks can use other React hooks
* Best practice, separate folder for custom hooks
* return functions in array when need to use multiple instance of it

# Best pratice, put JS logic outside of the return

```
function App () {
  // const [count, setCount] = useState(0);
  const [count, increment] = useCounter(0);
  // const [item, setItem] = useState(); made into useAxios custom hook
  
  const url ="http://api.kanye.rest";
  
  const {body} = useAxios(url);

  /* useEffect(()=> { made into useAxios custom hook
    axios.get(url)
      .then((res)=>{
        setBody(res.data);
      })
  }, []); */
  
  
  return (
    <div className="App">
      <h1>Custom Hooks!</h1>
      {count}
      <button onClick={increment}>Show/Hide</button>
      
      /* <div>
        {{count % 2 === 0} && <span>Hello There</span>} //&& is called short circuit express
      </div>*/
      
    {(count %2 === 0) &&
    <ul>
      <KanyeQuote/>
    </ul>
    }
    </div>
    
  );
}

export default App;
```
```
//useCounter.js custom hook

import { useState } from "react";
const useCounter =function(initial) {
  const [count, setCount] = useState(initial);
  
  const increment = function() {
    setCount(count+1);
  };
  
  const decrement = function() {
    setCount(count-1);
  };
  
  const clear = function() {
    setCount(0);
  };
  
  return [count, increment, decrement, clear];
  
};

export default useCounter;
```
```Counter.js component
const Counter = function(props){

  const [count, increment, decrement, clear] = useCounter(props.initial);
  return (
      <div>
        {count1}
        <button onClick={increment1}>+</button>
        <button onClick={decrement1}>-</button>
        <button onClick={clear1}>0</button>
      </div>
  )
}
export default counter;
```
```useAxios.js custom hook
const useAxios = function(url) {

  const [body, setBody] = useState('');
  const [error, setError] = useState(null);
  const [pending, setPending] = useState(true);
  
  useEffect(()=> {
    setPending(true);
    axios.get(url)
      .then((res)=>{
        setError('');
        setBody(res.data);
        
      })
      .catch(err => {
        setBody("");
        setError(err.message));
      })
      .finally(()=> setPending(false));
  }, [url]);
  
  return { body, error, pending };
};

export default useAxios;
```
```KanyeQuote.js component
const KanyeQuote = function() {
  const {body, error, pending} = useAxios("http://api.kanye.rest");
  return(
    <li>
      {error && error}
      {body && body.quote}
      {pending && "loading ... "}
    </li>
  )
};

export default KanyeQuote;
```
```officeQuote.js component
const officeQuote = function() {
  const {body, error, pending} = useAxios("http://www.officeapi.dev/api/quotes/random");
  return(
    <li>
      {error && error}
      {body && <div>{body.data.content}<span>{body.data.character.firstname}</span></div>}
      {pending && "loading ... "}
    </li>
  )
};

export default officeQuote;
```
```ronQuote.js component
const ronQuote = function() {
  const {body, error, pending} = useAxios("http://ron-swanson-quotes.herokuapp.com/v2/");
  return
    <li>
      {error && error}
      {body && <div>{body.data.content}<span>{body.data.character.firstname}</span></div>}
      {pending && "loading ... "}
    </li>
  )
};

export default officeQuote;
```
