
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

- we can use the ***AXIOS*** library to do all this in an easier way
- by default, all requests are GET
syntax : 
```
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

