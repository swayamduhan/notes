- Typescript is a superset of Javascript
- helps to write js in a much precise manner
- at the end of the day, ts gets compiled into js , ts is only a development tool
- we have to write more code in ts but it is safer code than js
- Typescript is all about **Type Safety**

## fck is Type Safety?
example : in js, you could do `2 + "2"` and it would return `"22"` which shouldn't be allowed in the first place because the data is of different types
Typescript helps in solving this shit

## Installation
follow the instructions on the website and install it globally using `npm install -g typescript`
`tsc -v` to get the current version installed
do `tsc <file-name>` to convert the ts file into js

## Syntax

```ts
let firstName : string = "swayam"
console.log(firstName);

export {}   // this export is to temporarily remove any red line wierd errors
```

- you define the type of the variable by putting a colon in front of variable name, either `string`, `boolean` or `number`(nothing special for int or float because javascript doesn't have a special runtime value for them)
- here, in the above example, typescript is smart enough to understand that you have input a string and treat it as a string input type, so mentioning string wasn't necessary here
- we also have a type called **any**, it is used to get-away from type checking, it can be declared using `let num: any = "s";` or `let num: any;` or simply `let num;` because ts doesnt know what type is about to be filled here, AVOID USING ANY
- we also have a config called NoImplicitAny that flags all the `any` as an error

## Functions in TS
```ts
function addNums(numOne: number, numTwo: number): number{
    return numOne + numTwo
}

let sum = addNums(5,7);
console.log(sum)
```

- the `:number` after taking args tells ts that we are expecting a number to be returned from the function

- in js, if our function takes in 3 args but we only mention 2 then that doesnt come out as an error, but in ts this is not allowed so we need to specify a default value in case we dont give that argument

```ts
function signUp(email: string, isPaid: boolean = false){} //stuff after '=' is default
signUp("swayam@gmail.com")
```

- for arrow functions ->
```ts
const addNums = (numOne: number, numTwo: number): number => {
    return numOne + numTwo
}
```

- using `void` and `never` for no return type shit
```ts
function printName(name: string): void {
    console.log(name)
}  

function consoleError(errmsg: string): never{
    throw new Error(errmsg)
}
```
- void is used when there is nothing to return, void can also be used in place of never here but according to TS documentation we should stick to using `never` when the function is used in throwing errors or terminating execution

## Using functions to pass objects
- object declarations are same as js
```ts
function createCourse(name : string, price : number):{name : string, cost: number}{
    return {name : name, cost : price}
}
```
- this is a function that takes in a name and price then returns an object with a name string and cost number


## Weird behavior of TS objects
```ts
function createUser({name , isPaid} : {name : string, isPaid : boolean}){}
  
createUser({name : "Swayam", isPaid : true, email : "swayam@gmail.com"})
```

in the above code, the method for destructuring objects and defining their types is shown.
however, if we try to pass an additional parameter like email it fails 
to bypass, use the below code
```ts
function createUser({name , isPaid} : {name : string, isPaid : boolean}){}

let User = {name : "swayam", isPaid : true, email : "swayam@gmail.com"}
createUser(User)

export {}
```
- there are better ways of handling this which will be shown later


## Type Alias
- used to create a new datatype like string number etc.
```ts
type User = {
    name : string;
    email : string;
    contact : number
}

function createUser(user : User) {}  // input user of type User
export {}
```

## READONLY, OPTIONAL, TYPE MIXMATCHING

- example : you are saving data in your mongo db, it puts an `_id` in the object so you want it to not be changed by anyone then you can put a `readonly` tag infront of it
- if you want a field in object to be optional, you can use `?`
```ts
type User = {
    readonly _id : string
    name : string
    contact : number
    creditCardNumber? : number
}
 
const user1 : User = {
    _id : "12234",
    name : "Swayam",
    contact : 99235234
}
```
- here creditcardnumber was optional to give and id cannot be changed now

- now talking about type mixing, we can extend another type using `&`
```ts
type cardNumber = {
    cardNumber : number
}
  
type cardName = {
    cardName : string
}
  
type cardDetails = cardName & cardNumber & {
    cvv : number
}
  
const card : cardDetails = {
    cardNumber: 1234567890,
    cardName : "",
    cvv : 343
}
```

## Arrays in TS
```ts
let newArrayOne : number[] = []
newArrayOne.push(1)
  
let newArrayTwo : Array<number> = []
newArrayTwo.push(1)
  
let newArrayThree : ReadonlyArray<number> = [5,6,2,8];
// push property doesn't exist in a readonly array
  
let newArrayFour = [];
// this is an array of type never and can't store shit
  
type User = {
    name : string
    age : number
}
  
let userArray : User[] = []; // array of type User
userArray.push({name:"John",age:30});
  
let twoDimensionalArray : number[][] = [[255,15,15], []]
twoDimensionalArray.push([5,3,7]);
```

------------------------------------------ continued later -------------------------------------------------

