## basic Stuff
what react does for you?
whenever you hit the backend for the data, a state of the data gets returned, if we do this manually using DOM Manipulation it takes a lot of time and effort. React makes it easier

- WE WILL BE USING VITE FOR DEVELOPMENT
`npm create vite@latest
we can `npm run dev` to simply start local environment
or we can `npm run build` to spit out html and js file to host on AWS or sum' shit

- we use `React DOM` for websites and `React Native` for mobile apps
- `<App />` and `<App></App>` is the same thing
- we can also use `React.createElement()` syntax insted of JSX (Javascript +XML) `return (<div></div>)`
- a website can be divided into 2 parts, STATE and COMPONENTS
- State is any object on the page that is changing. a state change triggers a re-render. anything that changes dynamically has to be defined as a state
- `import { useState } from 'react'` , this is the **HOOK** used for defining state
- Component is a reusable dynamic snippet
- before hooks came into picture in React 16, classes were used to write code and state management methods
- what is `<React.StrictMode>` in main.jsx file, it is used to render everything twice

- A React side-effect occurs when we use something that is outside the scope of React.js in our React components e.g. Web APIs like localStorage.
- React side-effect is a crucial component of a ReactJS application. It **helps establish communication with external resources, such as local storage and supports utilizing APIs**. However, one should crucially handle them using the useEffect hook; otherwise, it can lead to an application crash in the middle. 
- setTimeout, setInterval, fetch, getting inner html are some side effects

HTML way of creating a react-like way of counter
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="btn-parent"></div>
    <script>
        let state = {
            count: 0
        }
        function btnPress(){
            state.count++;
            reRender();
        }
        function reRender(){
            const parent = document.getElementById("btn-parent")
            parent.innerHTML = "";
            let btn = renderButton(state.count)
            parent.appendChild(btn);
        }
        function renderButton(count){
            const b = document.createElement("button")
            b.innerHTML = "Count " + count;
            b.setAttribute("onclick", "btnPress()")
            return b;
        }
        reRender()
    </script>
  
</body>
</html>
```

REACT Way of doing this : 
```js
import { useState } from 'react'
import './App.css'
  
function App() {
  const [count, setCount] = useState(0)
  
  return (
    <div>
        <button onClick={() => setCount((count) => count + 1)}>
          count is {count}
        </button>
    </div>
  )
}
```

REACT Way along with using component for Button : 
```js
import { useState } from 'react'
import './App.css'

function App() {
  const [count, setCount] = useState(0)
  
  return (
      <div>
        <CustomButton count = {count} setCount = {setCount}></CustomButton>
      </div>
    )
}
  
function CustomButton(props){
  function clickHandler(){
    props.setCount(prevCount => prevCount + 1)
  }
  return (
    <button onClick={clickHandler}>Count {props.count}</button>
  )
}
  
export default App
```


- creating root and rendering in main file
```js
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './index.css'
  
ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

- any js that needs to be written inside html/component we have to use curly braces

- the `.map()` function is very important to work with react
- `...` ellipsis mean all the pre-existing data in variable

**NOTE : any time a parent renders, the children also get re-rendered, there is a way to bypass this using React.memo which we will study later**

- to use CSS in react, we use double curly braces, 1 for writing js and the second for object
```js
<button style={{border : 10}}></button>
```

- instead of using props in function component rendering, the newer way of doing it is object destructuring
example : 
```jsx
// usual
function hello(props){
console.log(props.dawg)
}

// new
function hello({ dawg }){
console.log(dawg)
}
```


- to input data in some shit, we dont use `document.getElementById`, instead we can use states or react-query
example : 
```jsx
import { useState } from "react";
  
export function CreateTodo(){
    const [title, setTitle] = useState("")
    const [description, setDescription] = useState("")
  
    return (
        <div>
            <input id="tit" style={{padding : 10, margin : 10}} type="text" placeholder = "title" onChange={function(e){
                const value = e.target.value
                setTitle(value)
            }}></input>
            <input id="desc" style={{padding : 10, margin : 10}} type="text" placeholder="description"  onChange={function(e){
                const value = e.target.value
                setDescription(value)
            }}></input>
            <button onClick={async()=>{
                const res = await fetch("http://localhost:3000/todo", {
                    method : "POST",
                    body : JSON.stringify({
                        title : title,
                        description : description
                    }),
                    headers : {
                        "content-type" : "application/json"
                    }
                })
                const json = await res.json();
                console.log(json)
            }}>add todo</button>
        </div>
    )
}
```

- to grab each keystroke in react state, we can use onChange as seen in the code above

**BUG IN USING FETCH**
if we use fetch directly in code and change a state variable according to backend response, then component gets re-rendered and fetch will run again creating an infinite loop, so we use `useEffect` to handle that. 


## return only 1 single parent element?
just like how you cannot assign 2 values to any variable and not return 2 variables in a function, you cannot return 2 higher level sibling elements in a react function 

we need to create an outer div and put all code inside it
it also **helps in easier reconciliation**

to bypass an extra div in html code we can use `<> </>` or `<React.Fragment> </React.Fragment>` (both are same) to not put extra div in code

## re-renders
a re-render is when a component gets loaded again and react did some work to update this  
in real life and bigger applications, we should minimize re-renders in the app/website
we can use *React Developer Tools Extension* to visualize re-renders (check the highlight components setting in component bar in inspect window)

- jis function mein state hoti hai vo poori state render maarti hai brah 

when does re-render happen - 
- a state variable is changed that re-renders a component
- a parent component re-renders leading to all children rendering

## minimising re-renders (react - memo)
1. push the state down the hierarchy 
	to minimize whole parent rendering. if 2 siblings are using any state, you should always keep the state at the lowest ancestor

2. using **React-Memo**
	we can use it to skip re-rendering if the props of the component are unchanged
	syntax : 
```jsx
import { memo } from 'react'
const Header = memo(function Header({ title }){
	return (
		<div>{title}</div>
	)
})
```


## keys in react
we should add a key to the prop of a component, this helps react in uniquely identifying an element in the state array
example : if we undergo sorting in the array, then react will simply remove earlier elements and add newer elements in place of them but on the other hand if we used id/key then instead of doing this, react will simply change the place of the dom elements which is better to do 

```jsx
return (
	<>
		{todos.map((todo)=>return <Todo key={todo.id} title={todo.title} />)}
	</>
)
```

## wrapper component
it is used when you have similar shit for many components and instead of repeating the code we can create an outer component to wrap the inside shit
example : all cards in a website have a blurred light grey border

```jsx
import React from 'react'
  
function App() {
  return (
    <>
      <CardWrapper innerComponent={<TextComponent />} />
    </>
  )
}
  
function TextComponent(){
  return <div>
    hello there
  </div>
}
function CardWrapper({ innerComponent }) {
  return (
    <div style={{border : "2px solid black"}}>
      {innerComponent}
    </div>
  )
}
  
export default App
```

**BETTER WAY OF WRITING**

```jsx
import React from 'react'
  
function App() {
  return (
    <>
      <CardWrapper>
        <TextComponent />
      </CardWrapper>
    </>
  )
}
  
function TextComponent(){
  return <div>
    hello there
  </div>
}
function CardWrapper({ children }) {
  return (
    <div style={{border : "2px solid black"}}>
      {children}
    </div>
  )
}
  
export default App
```
anything inside the CardWrapper will come under children


## what are hooks?
hooks are functions that allow you to "hook into" react state and lifecycle features from function components
shit that starts with `use` are hooks, discussed till now : `useState`

## useEffect
when a component mounts, do something (mount means when something is put on the screen for the first time, not re-rendering)
syntax : first is a function  to run and the second is dependency array which means kiske change hone pe useEffect wala function chalana hai
does the same shit as 'componentDidMount' 'componentDidUnmount' and 'componentDidUpdate'
used to do side effects in react
syntax : 
`useEffect(callback function, [condition or dependency array])`
if the dependency thing changes then useEffect calls the function
dependency array takes in a state variable as parameter

- useEffect cant directly take in an async function : `useEffect(async()=>{}, [])` is wrong, instead we have to define another async function and pass it in inside the useEffect's callback
- possible bug -> for example we send 2 requests because of state changes and the latest request comes back first and earlier request comes back late for some reason then we will do shit wrong in our app
- to fix -> use asyncuseEffect library 

- to use component unmount in useEffect, we use a return statement in the callback function
example : 
```jsx
useEffect(()=>{
	const int = setInterval(()=>alert("hello"), 1000)
	return ()=> clearTimeout()   // you need to return a cleanup function
}, [input])
```


## useMemo
it means remembering some output given an input and not computing it again
it is like caching something, we dont have to recompute something

problem before useMemo - 
```jsx
import React, {useState} from 'react'
  
function App() {
  const [counter, setCounter] = useState(0)
  const [input, setInput] = useState(0)
  
  let count = 0;
  for(let i = 0; i <= input; i++){
    count += i;
  }
  
  return (
    <>
    <input onChange={function(e){
      setInput(e.target.value)
    }} placeholder='enter number'></input>
    Sum from 1 to {input} is {count}
      <button onClick={function(){
        setCounter(counter + 1)
      }}>Counter ({counter})</button>
    </>
  )
}
  
export default App
```

here, the count loop which is an expensive operation runs again when the button counter is clicked and app is rendered which is unoptimal. 
Yes, there are many ways to solve this using useEffect etc. but lets solve it using useMemo. the problem with useEffect is that we will have to introduce another state variable that will cause re-renders

Solution - 
```jsx
// modified count loop
let count = useMemo(()=>{
    let count = 0;
    for (let i = 0; i <= input; i++){
      count += i
    }
    return count;
  }, [input])
```

syntax is just like useEffect, takes in a callback function and dependency array

- you will personally rarely use this hook brah

## useCallback
it is used to memoize functions , helps in optimizing performance especially in cases where child components rely on reference equality to prevent re-renders
reference equality refers to place in memory

- generally, if we are using a state variable inside a useCallback or useMemo then we should pass it as dependency or else the function signature will always store the state of variable when it was made and not updatea

example : if we have a function in app which is passed down to a React.memo component, now if the app re-renders then the memory allocation of the function will change and cause react to re-render the component for no reason.
solution - useCallback
```jsx
import React, {memo, useCallback, useMemo, useState} from 'react'
  
function App() {
  const [count, setCount] = useState(0)
  
  const a = useCallback(()=>{
    console.log("hi there from a")
  }, [])
  
  return (
    <>
      <button onClick={function(){setCount(count + 1)}}>Counter ({count})</button>
      <Demo a={a} />
    </>
  )
}
  
const Demo = memo(function({ a }){
  console.log("re-rendered")
  return <>hi there {a}</>
})
  
export default App
```

explanation : 
if you have 2 objects or 2 functions a and b which have everything same inside them and you do `a==b`, it will return false, thats why react re-renders
on the other hand, if you have a simple variable containing number or string, then it returns true on equality and react will not re-render even though they are referencially unequal


## custom hooks

original code : 
```jsx
const [todos, setTodos] = useState([])
  useEffect(()=>{
    fetch('https://sum-server.100xdevs.com/todos')
      .then(response => response.json())
      .then(data => setTodos(data))
  },[])
```

easier code with custom hooks : 
```jsx
function useTodos(){
  const [todos, setTodos] = useState([])
  useEffect(()=>{
    fetch('https://sum-server.100xdevs.com/todos')
      .then(response => response.json())
      .then(data => setTodos(data))
  },[])
  return todos
}
  
function App() {
  const todos = useTodos()
  // ..... and more
 } 
```

both codes have exactly same functionality 

## reconciliation
it is how react works - 
- you give your state to react, react does all the heavy work and calculates the differences which is known as reconciling
- it then makes it appear on the DOM
- can you do it without react? yes
- example : you have high income, you hire a CA to calculate your expenses, profit and taxes


## useRef
it is a way of accessing dom elements
one way is simply using getElementById but that way we are confusing react by changing the dom without letting react know

```jsx
import React, {useState, useEffect, useRef } from 'react'
  
function App() {
  const [tax, setTax] = useState(250)
  const divRef = useRef()
  
  useEffect(()=>{
    setTimeout(()=>{
      divRef.current.innerHTML = 10
    }, 5000)
  }, [])

  
  return (
    <>
      Hi There, your tax is <div ref={divRef} id='tax-div'>{tax}</div>
    </>
  )
}

  
export default App
```

this way you can create a reference to the actual element
if you log `divRef.current`, it will return the actual element


**ANOTHER USE-CASE OF useRef**
to create variable that stores value across renders and doesnt cause any re-render
the value is persisted across renders
example : 
```jsx
import React, { useState, useCallback, useRef } from 'react';
  
// Create a component that tracks and displays the number of times it has been rendered. Use useRef to create a variable that persists across renders without causing additional renders when it changes.
  
export function Assignment2() {
    const [, forceRender] = useState(0);
  
    const numberOfRenders = useRef(0)
  
    const handleReRender = () => {
        // Update state to force re-render
        forceRender(Math.random());
    };
  
    numberOfRenders.current += 1
  
    return (
        <div>
            <p>This component has rendered {numberOfRenders.current} times.</p>
            <button onClick={handleReRender}>Force Re-render</button>
        </div>
    );
};
```
instead we could use a state variable for counting renders but that would cause another unwanted re-render
instead we could have used a global variable outside function to track this shit but it is unconventional in react to have global variables
so this is the only wayin ea



## routing
in pre-react days, getting a route on a page you would send req to backend and it would appear and then if you switch to messages you would again send a req to get whole of html css js back and do a hard reload of the page

in react, it is a *single-page application*, all the stuff gets back in the first request and routes are handled by react, you are just changing the view instead of hard reload
it is called **client-side routing** 
the whole html css js huge file is called **client-side bundle** 

- we use [react-router-dom](https://reactrouter.com) to do this shit
`npm install react-router-dom`

example : 
```jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom'
import { Landing } from './components/Landing'
import { Dashboard } from './components/Dashboard'
  
function App() {

  
  return (
    <BrowserRouter>
      <Routes>
        <Route path='/' element={<Landing />} />
        <Route path='/dashboard' element={<Dashboard />} />
      </Routes>
    </BrowserRouter>
  )
}
```

- this is how react routing is done
- next.js uses file based routing which will be studied later

how to make something constant in the page apart from routing, example - linkedin has the same topbar on all pages - simply put it outside browser routes
```jsx
return (
    <>
    <div style={{backgroundColor : 'black', color : 'white'}}>Hi this is the topbar</div>
      <BrowserRouter>
        <Routes>
          <Route path='/' element={<Landing />} />
          <Route path='/dashboard' element={<Dashboard />} />
        </Routes>
      </BrowserRouter>
    </>
  )
```