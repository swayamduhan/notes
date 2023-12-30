## Overview
Divided into 4 parts -
1. HTTP Servers
2. Authentication
3. Databases
4. Middlewares

## ECMAScript  vs JavaScript vs Node.js vs Bun
ECMAScript is a scripting language specification over which Javascript is based. All javascript interpreters should follow this script. basically it is the rules for scripting language design. versions like ES5, ES6, ES2015 are updates of the ECMAScript that bring new syntax 

Javascript is a scripting language based on ES and most widely used ES based language.
It supports DOM(Document Object Model) Manipulation which is necessary for web development which is not a part of ECMAScript 
V8 Engine(C++ by chromium for chrome and chromium browsers) and  SpiderMonkey(C and Rust for Firefox) are JS Compilers to convert code into machine level code.

this V8 engine was taken out and extra functionalities were added to it and made into a runtime to compete with Java. Now a very popular backend language. Known as Node.JS (it is not a language, it a javascript runtime)(written in C++)

BUN is a faster runtime than Node.js written in Zig(low latency language)

#### What can be done with Node.JS?
1. Create CLIs(command line interfaces)
2. Create a game
3. Create a video player
4. Create an ***HTTP SERVER***


## What is an HTTP Server??

Hyper Text Transfer Protocol
Protocol defined for machines to communicate
usually for websites to use frontend to talk with your backend

HTTP Protocol - client sends some instructions to server, server performs task by exposing the Model to the input and returns back the output to the user

### Special NOTE :
A server can host multiple websites and they all point to the same server. so, sometimes when we enter the ip address directly instead of the domain name in url, then the backend server gets confused which site to show up.
### Stuff needed for HTTP (client side)
1. Protocol HTTP/HTTPS
2. Address (URL/IP/PORT)
3. Route
4. Headers, Body, Query Params
5. Method

eg : `https://chat.openai.com/backend-api/conversation`
here, `https` is protocol, `chat.openai.com` is url, `backend-api/conversation` is route, `2+2=?` is body and `POST` is method, the cookie is the header ( cookie is a way of authentication for example to know if you're logged in)

### What happens in browser after firing a request?
1. Browser parses the url
2. Does a DNS(DOMAIN NAME SERVICE) Lookup(converts google.com to an IP)
3. establishes a connection to the IP(a handshake)

##### What is DNS resolution?
URLs are like contacts in phone. in the end, they map to an IP. when you buy a DNS, you need to point it to the IP of your server

### HTTP (Server side)
1. Response headers
2. Response body
3. Status codes

### Common methods
1. GET - getting info back from server
2. POST - posting some new info/adding to server
3. PUT - putting some updation 
4. DELETE - deleting some shit

### Status codes
1. 200 - everything good
2. 404 - page/route not found
3. 403 - authentication issues
4. 500 - internal server error
5. 411 - incorrect inputs

## Using Express.JS
popular library to make HTTP Servers. if you want a challenge, create a server normally using C/C++.
express makes it easier.
(Next.JS is becoming more popular for backend recently)

`npm install express` to install 

```
const express = require("express")
const app = express()
const port = 3000

app.get("/", (req, res)=>{          // req - request, res - response
    res.send("hello lil bro")
})

app.listen(port)          // listening to this port
```

run this program using node then open localhost:3000 in browser to run locally 
we can also do res.json and response with an object instead of res.send

- REST APIs are used when another node.js runtime needs to interact with the server. not meant for connection with mobile apps or browsers
- To access the server from our website, we use the `fetch` command in our js code
- a machine can have a single ip address but multiple ports which help to put up multiple http servers. a port can have only 1 server.

#### running locally on phone
get the private ip of your machine using `ipconfig` . connect mobile to same wifi. type in the ip followed by colon port in phone to access. 

#### Accessing body of req
Express doesn't provide a direct method to see the body of request.
instead we can use a body-parser library.
for higher versions, we can simply do `app.use(express.json())` in our code beginning and then we can read the body normally.
for lower versions,
`const bodyParser = require("body-parser")`
`app.use(bodyParser.json())` - these are known as _middlewares_, explained later
then simply you can get your body


#### Using POSTMAN
- we use POSTMAN to check our server by sending get,post & more requests. download it locally. type the url in the space provided and click on the send.
- we can add custom headers to send in a post request to the server using the headers tab in the POST method.

#### NODEMON
It is a package which restarts the server each time we update something in our code and we dont need to re-run it each time.
`npx nodemon fileName.js`


#### Query Parameters
- These are used in GET requests to send a body to the server and get back data. there is no easy way to send body in get.
- where is it in url - 
  everything placed after a question mark at the end is a query.
  eg : ?message=hello%20world, here this is saved inside message key with hello%20world value
  (%20 is used to add a space)
- you can access the above query using `req.query.message`
- to give multiple variables, `?n=30&a=5` means n = 30 and a =5


## More on Express
#### get request
simply pass args in query params
take the params and perform some shit and return using res.json or res.send

#### post request
pass your args in body. use json format in raw type.
to get the body in express use req.body but before this use the middleware `app.use(express.json())` to access body
perform operation and send using res.json or res.send

#### put request
send a put request and simply change the data in code and return empty json or any shit

WE NEED TO PUT CONDITIONS IN CASE WRONG INPUTS ARE ENTERED, WE HAVE TO DEFINE THEM AND SEND STATUS CODES AS ERROR
#### To send back status
if only status is to be sent on error : `res.sendStatus(200)`
if message also : `res.status(411).json({})`


#### Wildcard `:`
This is used when you need a get to handle multiple requests about something similar but different things. eg : you have 5 files in a folder. and whenever you do `localhost:3000/files/filename` then you should be able to read it.

so for that we use a wildcard shit.
eg : 
```
app.get('/file/:filename', (req,res)=>{

  const file = req.params.filename

  fs.readFile(`files/${file}`,'utf-8', (err, data)=>{

    if (err){

      res.status(404).send("File not found")

    } else {

      res.status(200).send(data);

    }

  })

})
```
anything present after : in this /file/ route will get handled by this
the filename is accessed using params

#### How to handle all invalid routes
```
app.all('*', (req, res) => {
  res.status(404).send('Route not found');
})

OR 


app.use((req,res,next)=>{
    res.send(404).json({
        msg : "404, Route Not Found :("
    })
})
```
Both work whenever some wierd route which is not known is hit
- keep in mind, a global catch has an app.use with 4 args not 3, if there are 3 args, acts as catch for invalid routes



## Middlewares
a website does 2 types of checks - an input validation and authentication check

Poor way of doing this shit is using if - else statements
now imagine, you need to do same thing in so many routes. you are making the code DRY (dont repeat yourself bih')
we define middlewares at the top and simply use them in our app.method function arguments to do checkups in the route

we do this by putting multiple callback functions in our app function.
eg : 
```
const express = require("express");
const app = express();


app.get("/yo",(req, res, next) => {
    const x = 1;
    console.log("hi from callback function 1");
    if (x == 2) {
      res.json({
        msg: "yo whats up",
      });
    } else {
    next();
    }
  },
  (req, res) => {
    console.log("Hi from final main function.");
    res.send("we up");
  }
);
  
app.listen(3000)
```
try changing the value of x and see how the code runs
- the next() is used to pass command to the next function
- keep in mind, the server can only respond with a single res.send or json, if it does twice, then error will be there

##### app.use ( _functionName_ )
it means that the middleware inside bracket will be used everywhere in the server
eg : `app.use(express.json())` here, express.json() is a middleware to read the body in a post request
- why do we need this json thing tho, why cant we simply req.body -> this is because express doesnt know if the incoming body is binary or json or html or text data so we need to specify it

also, you only need to write the function name, not call the function, the shit above returns a function

### Global Catches
if the user sends anything weird in the post request body or gives the wrong inputs or hits some wrong route then we use this.
```
app.use((err, req, res, next) => {
  res.json({
  msg : "sorry, something is up with the server"
  })
});
```
also, it helps us to not expose our server and error to the user who sent wrong inputs, could potentially protect from attacks
- it is necessary to use 4 args in this, if we use 3 then it will act as a invalid route handler as mentioned above in the notes :  [[BACKEND DEVELOPMENT#How to handle all invalid routes]]
it is also a middleware that gets called after all requests. THESE ARE KNOWN AS ERROR-HANDLING MIDDLEWARES. they are always defined at the end. take 4 args instead of 3


## Input Validation 
to handle so many validations, input validation libraries are present to do the work

ZOD is the most popular library in node.js for this shit

### ZOD
very easy way to check for inputs. `npm install zod`
ask ChatGPT for help with implementing zod or docs

eg : 
```
const zod = require("zod")
  
// eg : write a schema for a object that takes an email, a pass of 8 letters and a country that is either IN or US

const schema1 = zod.object({
    email : zod.string().email(),
    password : zod.string().min(8),
    country : zod.literal("IN").or(zod.literal("US"))
})  

function validate(obj) {
    const response = schema1.safeParse(obj)
    console.log(response)
}
  
validate({
    email : "swayam@gmail.com",
    password : "Password",
    country : "IN"
})
```

eg : 
```
const express = require("express")
const zod = require("zod")

const schema = zod.array(zod.number())    // tells that schema should be an array of numbers

const app = express()
app.use(express.json())  

app.post('/checkup', (req,res)=>{
    const kidneys = req.body.kidneys
    const response = schema.safeParse(kidneys)
    res.json({
        response
    })
})

  

app.listen(3000)
```

## Authentication
to check if a user has access to a resource or not
dumb way - ask to input username and pass in headers
original method - 
- give the user a token on login
- ask the user to send back the token on each request
- when the user logs out, forget the token or revoke from backend
there are complicated ways to do this, like Login With Google/Facebook/Riot and there is simple way of username password

#### 1. Hashing
 A password when signing up is converting into hash (comb of num & alphabets) and stored in the database. it is only 1-way, a hash cant be converted back to password. a certain combination can have only a single hash, har baar alag hash ni banta. when trying to login, this hash is compared with the hash stored in database and authentication is done. eg : SHA-256 Hashing in crypto for mining blocks

#### 2. Encryption
it is a 2 way method to encrypt or decrypt something but you need to have the encryption key to do so. something like 

#### 3. JWT (Json Web Tokens)
it converts a Json object into a complex long string called token(this string is kinda structured unlike hashing). anyone can decode this string to the original json object but only the server at which this json object is stored can verify it using a password only they have. eg : a cheque with a signature can be seen by everyone but only the bank can verify the signature
you can decode it at jwt website. if someone gets a hand on your jwt token they can misuse stuff.
this is present in authentication header in a http request. everytime you send a request it is sent along
- `const jwt = require("jsonwebtoken")`

#### 4. Local Storage
The JWT Token given to us is stored in the local storage of the browser. this is sent along at every request to the website. When we are logged out of website, this JWT token gets removed from local storage. 
There is another method for authentication using Cookies, it will be discussed later.

