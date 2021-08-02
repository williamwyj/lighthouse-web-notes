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
