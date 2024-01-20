## Conventions
camelCase for variables and methods
first letter capital for class
all caps for constants
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
- to simply swap variables, we can use a 3rd variable, `x, y = y,x` doesnt work here.
	eg : `temp = a; a = b; b = temp;` 


***Rest of the shit comes in Reference Data Types (later)***

### Primitive vs Reference 
- primitive hold data, have 1 value, use less memory and are fast
- reference hold address, have multiple values, use more memory and slow
## Type Conversion and Casting
  
#### Type conversion :
In type conversion, a data type is automatically converted into another data type by a compiler at the compiler time. In type conversion, the destination data type cannot be smaller than the source data type, that’s why it is also called widening conversion. One more important thing is that it can only be applied to compatible data types.
eg : 
```java
int x = 1000;
double y;
y = x;  // 1000.000000
```

#### Type Casting: 
In typing casting, a data type is converted into another data type by the programmer using the casting operator during the program design. In typing casting, the destination data type may be smaller than the source data type when converting the data type to another data type, that’s why it is also called narrowing conversion.
syntax - `destination_datatype = (target_datatype)variable`
eg : 
```java
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
```java
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
```java
result = (condition) ? valueIfTrue : valueIfFalse;
```

#### Switch-Case Statements
its an alternative for using multiple if else statements

eg :
```java
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
```java
int[] numbers = {1, 2, 3, 4, 5};
for (int num : numbers) {
    System.out.println("Number: " + num);
}
```

- `continue` skips the current iteration for a particular condition and `break` stops the execution of the loop


## Arrays
In Java, an array is a data structure that allows you to store multiple values of the same type in a single variable. Arrays are used to organize and access a collection of elements efficiently. Here are some key points about arrays in Java:

**DECLARATION AND INITIALISATION**
```java
// Declaration of an array (integers)
int[] numbers;

// Initialization of the array with size 5
numbers = new int[5];

// Declaration and initialization in one line
int[] numbers = new int[5];
```

- we can also write `int num[]` instead of `int[] num`. the code written above is java standard convention but this syntax is also valid for compatibility with C and C++ language. 


**INITIALISATION WITH VALUES**
```java
// Initialization with values
int[] numbers = {1, 2, 3, 4, 5};
```

**ACCESSING ELEMENTS**
```java
int[] numbers = {1, 2, 3, 4, 5};

// Accessing elements
int firstElement = numbers[0]; // Access the first element (index 0)
int thirdElement = numbers[2]; // Access the third element (index 2)
```

- `arrayName.length` for its length

### Multidimensional Array (MATRIX)

```java
// Declaration and initialization of a 2D array
int[][] matrix = {
    {1, 2, 3, 4},
    {5, 6, 7, 8},
    {9, 10, 11, 12}
};
```

**Creating a new 2-D Array**
```java
int[][] myArray = new int[3][4];
```
This will create a new matrix with 3 rows(outer array with 3 arrays inside) and 4 columns (each inside array has 4 items). the same presentation as the example above this

**3-D Array**
```java
int[][][] = new int[2][3][2];
```
bas number of square brackets badate jao

### Advanced Method for iterating through array
```java
import java.util.Arrays;

int[] numbers = {5, 2, 8, 1, 3};

// Sorting the array
Arrays.sort(numbers);

// Enhanced for loop to iterate through the sorted array
for (int num : numbers) {
    System.out.println(num);
}
```

### How to print an array?
If you try to do `System.out.print(array_name)` then it will print the **memory address** of the array.
to print we need to use the `Arrays.toString()` method in library
```java
import java.util.Arrays;  
  
public class Main {  
    public static void main(String[] args) {  
        int[] nums = {1, 2, 3};  
        System.out.println(Arrays.toString(nums));  
    }  
}
```

**HOW TO PRINT IN A MATRIX FORM**
```java
int[][] numbers = new int[3][4];  
for (int i=0; i < numbers.length; i++){  
    for (int j=0; j < numbers[0].length; j++){  
        System.out.print(numbers[i][j] + " ");  
    }  
    System.out.println();  
}
```

### More on arrays
**WHAT IS A JAGGED ARRAY**
It is an 2D array in which the sub arrays an have different lengths.
either simply create an array or use the `new` keyword to create a new array using the method below.

```java
int nums[][] = new int[3][];
nums[0] = new int[2];
nums[1] = new int[5];
nums[2] = new int[3];
```

**DRAWBACKS OF USING ARRAYS
- an array with different data types cannot be created. If you need to store elements of different data types, you would need to use an array of objects (e.g., `Object[]`), leading to the loss of type safety.
- the size of the array cant be changed later, rather we need to create a new array and copy all previous items there - time taking and consumes extra memory
- searching and filtering takes time
- no built-in methods for insertion and deletion
**NOTE** : the solution to this is *COLLECTIONS*


**CREATING AN ARRAY OF CLASS INSTANCES**
eg : we have a class named 'Student' then,
```java
Student s1 = new Student();
Student s2 = new Student();
Student s3 = new Student();

Student[] students = new Student[3];
students[0] = s1;
students[1] = s2;
students[2] = s3;

// OR SIMPLY WE CAN DO
Student[] students = {s1,s2,s3};
```


## Strings
String is a type of class and also begins with a capital letter 
2 ways of defining string are - 
```java
String name = new String("Swayam") // regular way of creating an instance

String name = "Swayam"; // commonly used
```

- we can concatenate using `+` operator
- we can get the letter at any index using `stringName.charAt(index)`
- by default, strings are immutable, a new string is created when you perform an operation on a string, you get a new reference for the variable
- all the strings are stored inside STRING CONSTANT POOL inside JVM
- **YOU CAN READ ALL METHODS ONLINE OR IN AN IDE**

**HOW ARE STRINGS CREATED INSIDE POOL**
whenever a new string is created, it first checks if it already exists, if it does then it does not create a new object and instead just assigns the variable to that existing string.
if doesnt exist then a new string object is created. 
the address of that particular string is then used to refer the variable to the string :)

**HASHCODE**
The `hashCode()` method returns a 32-bit signed integer hash code for the string.

```java
String name = "Swayam";
int hash = name.hashCode();
```

### Creating Mutable Strings
  
1. **StringBuffer**
	the capacity is 16 bytes ( `str.capacity()` ) and changes as per string
	```java
	StringBuffer name = new StringBuffer("swayam");
	// now you can use methods like insert, delete, append
     ```
 2. **StringBuilder**
	 the default capacity is 16 bytes and changes as per string, same syntax as above

to convert this shit into string, use `str.toString()`

Both `StringBuilder` and `StringBuffer` are mutable, but there is a key difference between them:

- `StringBuilder` is not thread-safe, and it is more efficient in single-threaded scenarios.
- `StringBuffer` is thread-safe, which means it can be safely used in multi-threaded environments. However, its operations are synchronized, which may lead to lower performance compared to `StringBuilder` in single-threaded scenarios.

Choose between `StringBuilder` and `StringBuffer` based on your specific requirements regarding thread safety. If you are working in a single-threaded environment, `StringBuilder` is often preferred for its better performance.