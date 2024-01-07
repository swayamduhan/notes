## Variables 
- to store values and use in code
- the basic syntax is `<datatype> <variablename> = value`
	eg : `int num = 5`
- we can also just initialize variables and not give them a value

## Primitive Data Types
#### 1. Integer
1. **byte:**
    - Size: 8 bits (1 byte)
    - Range: -128 to 127
2. **short:**
    - Size: 16 bits
    - Range: -32,768 to 32,767
3. **int:**
    - Size: 32 bits
    - Range: -2^31 to 2^31 - 1
4. **long:**
    - Size: 64 bits
    - Range: -2^63 to 2^63 - 1
    - for long we need to put `l` at the end, `long num = 5434l`

#### 2. Float
1. **float:**
    - Size: 32 bits
    - Precision: 7 decimal digits
2. **double:** ( default )
    - Size: 64 bits
    - Precision: 15 decimal digits
- The default data type for decimals is double `double num = 5.6;`
- to define a float, you will need to add a `f` at the end `float num = 5.6f;`
#### 3. Character (char)
to define single **16-bit** UNICODE letters like A, B, c. eg : `char myChar = 'a'`
you can also use escape sequences as a character like `\n`
you can only **use Single Quotes** for defining character literals, double quotes are for Strings
follows ASCII
#### 4. Boolean
true or false, size not defined
doesn't work with 0 and 1 as value
`boolean success = true`

#### More on Literals
- Using Binary literals `int num = 0b101` it means 5 (just add a `0b` at front)
- Using Hexadecimal, add `0x` at start
- Using Octal, add `0` at start
- We can use underscores in our integer for easier representation and it wont affect our number
	eg : `int num = 10_000_000` is same as `int num = 10000000` 
- to use exponentials, `double num = 12e9` which represents 12x10^9
- we can also store integers in double
- we can also perform arithmetic on character literals
	eg : `char myChar  ='A'` then `myChar++` gives `B`
	keep in mind, java treats them as their ASCII unicode codes and performs on that. here, A is 65 and B is 66


***Rest of the shit comes in Reference Data Types (later)***

## Type Conversion and Casting
  
#### Type conversion :
In type conversion, a data type is automatically converted into another data type by a compiler at the compiler time. In type conversion, the destination data type cannot be smaller than the source data type, that’s why it is also called widening conversion. One more important thing is that it can only be applied to compatible data types.
eg : 
```
int x = 1000;
double y;
y = x;  // 1000.000000
```

#### Type Casting: 
In typing casting, a data type is converted into another data type by the programmer using the casting operator during the program design. In typing casting, the destination data type may be smaller than the source data type when converting the data type to another data type, that’s why it is also called narrowing conversion.
syntax - `destination_datatype = (target_datatype)variable`
eg : 
```
byte b = 127;
int a = 12;
b = byte(a);
```
while converting float to int, we lose the decimal

## Operators
**Arithmetic Operators** -
`+` to add, `-` to subtract, `*` multiply, `/` for quotient, `%` for remainder (modulus)
`num++` and `num+=1` also work
`num++` - post increment and `++num` is pre increment. you know the difference.

**Relational Operators** -
`<`, `>`, `<=`, `>=`, `==`, `!=`

**Logical Operators** - 
`&&` for AND, `||` (pipe) for OR, `!` for NOT

## Conditional Statements
code syntax -
```
int a = 9;  
if (a > 15) {  
    System.out.println("Hello");  
} else if (a > 10) {  
    System.out.println("Hello2");  
} else {  
    System.out.println("Hello3");  
}
```

the curly brackets are optional if we have only 1 line of code in the statement
eg - `if (a<16) System.out.print("cool")`

- we can also use ***terniary operator*** like JS
```
result = (condition) ? valueIfTrue : valueIfFalse;
```

#### Switch-Case Statements
its an alternative for using multiple if else statements

eg :
```
int dayOfWeek = 3;
String dayName;

switch (dayOfWeek) {
    case 1:
        dayName = "Monday";
        break;
        
    case 2:
        dayName = "Tuesday";
        break;

    case 3:
        dayName = "Wednesday";
        break;

    case 4:
        dayName = "Thursday";
        break;

    case 5:
        dayName = "Friday";
        break;

    case 6:
        dayName = "Saturday";
        break;

    case 7:
        dayName = "Sunday";
        break;

    default:
        dayName = "Invalid day";
}

System.out.println("The day is: " + dayName);

```

the `break` keyword is used to break out of the switch, if we dont, then all the cases will be executed after a single case matches

## Loops
`for`, `while`, `do while`  same as JS

for-each loop for iterating over items of an array
```
int[] numbers = {1, 2, 3, 4, 5};
for (int num : numbers) {
    System.out.println("Number: " + num);
}
```

- `continue` skips the current iteration for a particular condition and `break` stops the execution of the loop