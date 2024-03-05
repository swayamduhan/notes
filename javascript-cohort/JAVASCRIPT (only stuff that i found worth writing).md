
## Interpreted vs Compiled languages
- compiled need to be compiled before running and dont compile & make a temp file if there is any error in code. eg : cpp
	- write -> compile -> run (put in ram)
- interpreted languages can be run directly and checks code line by line. eg: js
	- write and run
	- they can run partially if error comes later in code

## Static vs Dynamic Languages
C++ is static and strictly typed - you need to specify types for each variable and cant change them later
eg : `if a = 10 then we cant do a = "hello" later on`

Javascript is loosely typed/dynamic which is cool but not so cool in large production.
eg : `let a = 10; a="swayam" is correct`

## Single threaded nature of JS
strictly only uses 1 core of machine
work/code cant be split into many cores to reduce runtime
There is 1 way to do that by using CLUSTER module (taught later)
Java, Cpp, GoLang are multithreaded


## Basic Functionalities

- ##### VARIABLES 
	 let(changeable, can be initialised without value), const(not changeable later on), var(outdated)
- ##### String, Integer, Boolean
- ##### Array, Object
	- if you have a `const` array then you can still change the elements inside the array but you cant change it to a new array
- ##### Functions, Arrow Functions


## Regular Expressions in any Language

- start and end with slashes / /
- g is used after slash to represent 'globally' eg: `/[0-9]/g`
- square brackets `[]` are used to define range eg: `[A-Za-z0-9]`
- `^` inside square brackets is used for negation eg: `/[^0-9]/` means anything except 0-9
- `$` is used to check for end of string
- `^` outside square brackets is used to check the start of string
- `.` means any digit or letter or character
- to actually search for a dot, use escape sequence backslash
{LEARN MORE ONLINE}


## Date() object in JS

- Used to create to create date instances in code
- can be used to get current time, date, hours, seconds, minutes, Day etc.
- can be used to calculate milliseconds in usage of a function by using getTime() function and subtracting initial and final values


## Classes in JS

- Classes are just like STRUCTS in solidity and other languages. Reusable object definitions :)
- refer to mdn web docs for clarity 
- classes are like a blueprint version of objects
- static functions are associated with the class itself and not with the object created using class

- HOW TO DEFINE?
```
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
  increaseHeight(){
    this.height += 5
  }
  static hello(){
    console.log("hello lil bro")
  }
}

// to create a new instance for this class
let rect1 = new Rectangle("10", "5")
rect1.increaseHeight()
Rectangle.hello()
```

- Also read about Extends keyword for defining classes

## eval(expression)
- used to evaluate any mathematical expression with brackets
- useful shit


## JSON (JavaScript Object Notation)
- JSON.parse() - converts string to js object, we usually get data from servers or APIs in string format
- JSON.stringify() - converts js object to string usually to send to someone


## Async vs Sync 

Javascript is single threaded but it can do context switching and delegating to reduce work time and work in a correct manner and efficienty. This is called asynchronous programming

Some async functions provided out of the box - 
- `fs.readFile("something.txt", "utf-8", function(err, data){console.log(data)})` - reads text from file, import fs module first (file system)
- setTimeout
- Fetch (url api fetching method)

High level architecture -
```
setTimeout(()=> console.log("hi"), 10000)

setTimeout(()=> console.log("hi2"), 5000)

  

let sum = 0

for (let i = 0; i < 10000000000; i++){

    sum += i

}

console.log(sum)
```

in the above code, first line starts the clock for 10s then second line starts clock for 5s and then js gets busy doing the loop because it is single threaded. the 5s clock finishes first and goes to the callback queue waiting for the code to finish and similarily the 10s timer finishes and goes to the queue. even tho the 10s clock was written first in code, the 5s clock function will get executed first because it was 1st in the callback queue.


### Promises 
Cleaner way of writing callbacks. used for several reasons for example readability and to prevent callback hell

```
const myPromise = new Promise((resolve, reject) => {
  // Asynchronous operation, e.g., fetching data from an API
  setTimeout(() => {
    const success = true;

    if (success) {
      resolve("Data fetched successfully!");
    } else {
      reject("Error fetching data");
    }
  }, 2000); // Simulating a 2-second delay
});

myPromise
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.error(error);
  });

```

the instance of the promise is returned synchronously there and then only. like if we console log the promise it will show promise pending. the resolve is returned asynchronously.


### Async Await
a better way of writing promises. syntactical sugar :)

```
async function main(){
	const dawg = await blablabla()
}
```


## The Fetch API

- we can use the ***AXIOS*** library to do all this in an easier way. read docs for the same
- by default, all requests are GET
syntax : 
```js
fetch(url, options)
  .then(response => {
    // Handle the response
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    return response.json(); // or response.text() for plain text
  })
  .then(data => {
    // Handle the parsed data
    console.log(data);
  })
  .catch(error => {
    // Handle errors during the fetch operation
    console.error('Fetch error:', error);
  });
```

we can also use simply async await instead of this promise shit
```
async function callApi(){
	const response = await fetch('_url_');
	const finalData = await response.json()
	console.log(finalData)
}
```

for sending post requests we need to mention the options
```
const postData = {
  title: 'foo',
  body: 'bar',
  userId: 1
};

fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify(postData)
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Fetch error:', error));

```

for using query parameters 

```
const params = new URLSearchParams({
  page: 1,
  limit: 10
});

fetch(`https://api.example.com/data?${params}`)
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Fetch error:', error));
```


## try catch

```js
try{
    let a;
    const len = a.length
    console.log("hi after error")
} catch (e) {
    console.log("hi, inside catch")
}
  
console.log("hi, outside")
```
- to catch potential errors
- when err in try then execution of try stops and control reaches catch then moves on outside

## DOM Manipulation
various methods to manipulate html elements and show stuff on the page

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <form id="form-1">
        First Name : <input type = "text" value="swayam"><br>
        Last Name  : <input type="text" value="duhan"><br>
    </form>
    <p>Click the "TRY IT" button to do sum' shit</p><br>
    <button onclick="sayName()">TRY IT</button>
    <p id="test"></p>
  
    <script>
        function sayName(){
            let x = document.getElementById("form-1").elements.length
            let y = document.getElementById("form-1").elements[0].value
            document.getElementById("test").innerHTML = "Found " + x + " elements in the form. The value of 1st element is " + y + "."    
            let para = document.createElement("p")
            para.innerText = "This paragraph was created using DOM"
            document.body.appendChild(para)
        }
        </script>
</body>
</html>
```


- To get elements
	- `getElementById, getElementsByTagname, getElementByClassName, querySelectorAll, querySelector`
	- for query selector - [click here](https://www.w3schools.com/cssref/css_selectors.php)
	- you can further use `.style.property` to change css of selected elements
- `document.forms` to get all form elements. this is called a object collection. more examples include `document.anchors, document.body, document.embeds, document.images, document.links, document.scripts` etc.

Difference b/w HTML Collection and Node List
**HTML** - live list (getElementById, getElementsByClassName), collection of document elements, items can be accessed using name id or index number, live means koi dom ke through change kroge to dikh jayega page pe
**NODE LIST** - not live (querySelectorAll), collection of nodes (element nodes, text nodes, attribute nodes), access only via index number, are static

- Changing HTML Elements
	- `.innerHTML
	- `.style.property`
	- `.setAttribute(attribute, value)`
	- `document.write` - never use this after document is loaded, it will overwrite everything
- `replaceChild`, `appendChild`, `removeChild`, `createElement`, `createTextNode`
- `.childNodes[index]` to access children
- whole document is document node, each element is element node, each text in element is text node
- a text node is the child element of element node

```js
// accessing text inside elements
let text = document.getElementById("demo").firstChild.nodeValue
text = document.getElementById("demo").childNodes[0].nodeValue
text = document.getElementById("demo").innerHTML
```

- siblings are elements with same heirarchy

### DOM EVENTS
```html
<p onclick="this.innerHTML='Oil Up'">Hello Lil Bro</p>
```

eg : code to capitalise all input
```html
Enter Text  : <input type="text" id="demo" oninput="upperCase()">
    <script>
        function upperCase(){
            const elem = document.getElementById("demo")
            elem.value = elem.value.toUpperCase()
        }
    </script>
```

- more events include `ondoubleclick, onmouseover, onmouseout, onmousedown, onmouseup`

**ONLOAD and ONUNLOAD FUNCTIONS**
can be used to check browser version and info when page loading and display correct webpage version based on it

#### DOM Event Listeners
addEventListener and removeEventListener
```js
document.getElementById("demo").addEventListener("input", upperCase)
        function upperCase(){
            const elem = document.getElementById("demo")
            elem.value = elem.value.toUpperCase()
        }
```

```html
<p>Resize your window to change the number below :)</p>
    <p id="demo"></p>
    <script>
        let x = document.getElementById("demo")
        x.innerHTML = Math.floor(Math.random() * 10000)
        window.addEventListener("resize", resize)
        function resize(){
            x.innerHTML = Math.floor(Math.random() * 10000)
        }
    </script>
```

to remove listener
```js
elemReference.removeEventListener("listenerName", functionName)
```
#### Event Bubbling or Event Capturing
`useCapture?` is the third argument of `addEventListener`
in capturing outermost event is handled first then the inner one
bubbling is opposite
`true` for capturing and `false` for bubbling
- default is bubbling

## Hitting backend request using frontend

we use `fetch()` to do this
here's an example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<script>
    function sum(){
        const a =  document.getElementById("num1").value;
        const b = document.getElementById("num2").value;
        fetch(`https://sum-server.100xdevs.com/sum?a=${a}&b=${b}`)
        .then((res)=>{
            console.log(res)
            res.text()
            .then((ans)=>{
                document.getElementById("ans").innerHTML = "The answer is " + ans
            })
        })
    }
</script>
<body>
    <input id="num1" type = "text" placeholder="first number"><br><br>
    <input id="num2" type="text" placeholder="second number"><br><br>
    <button onclick="sum()">calculate sum</button>
    <p id="ans"></p>
</body>
</html>
```

this can be done easily using `axios` done later
- we can use async/await for easier code lmao, forgive me for using promises

### Debouncing
example : on amazon webpage, as you are typing in the bar you keep getting new suggestions (the backend is getting hit with every keystroke)
now if you are typing something very fast then there are no such suggestions and we get suggestions only after we typed
this is called DEBOUNCING and is used to reduce backend calls

example : you create a frontend to get sum of number on every keystroke it will call backend on every keystroke, now if the number you want to enter is known to you then it is simply sending bematlab ki backend calls on each stroke so we need debouncing

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<script>
    let clock;
    function debouncedSum(){
        clearTimeout(clock)
        clock = setTimeout(()=>{
            sum()
        }, 100)
    }
    async function sum(){
        const amount =  document.getElementById("principal").value;
        const rate = document.getElementById("rate").value;
        const time = document.getElementById("time").value;
        const response = await fetch(`https://sum-server.100xdevs.com/interest?principal=${amount}&rate=${rate}&time=${time}`)
        const json = await response.json()
        document.getElementById("ans").innerHTML = `The amount after ${time} years is ${json.total} and interest applied is ${json.interest}`
    }
</script>
<body>
    <input id="principal" oninput="debouncedSum()" type = "text" placeholder="principal amount"><br><br>
    <input id="rate" oninput="debouncedSum()" type="text" placeholder="rate"><br><br>
    <input id="time" oninput="debouncedSum()" type="text" placeholder="time in years"><br><br>
    <p id="ans"></p>
</body>
</html>
```

**DOM MANIPULATION OF PRE REACT DAYS**
- the backend will return a state of the data when fetched after every interval using `setInterval`
- according to the json data, display items on the screen
- better solution - instead of clearing whole data and putting the updated data back on the screen, we should calculate the difference between new and old data and only update what needs to be updated (VIRTUAL DOM - where we have the blueprint of the DOM). this is how react works