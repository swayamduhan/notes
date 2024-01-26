
# Basic shit
-  a computer lang is a software, set of rules, set of programs to interact with device
- a compiler is a pre defined program which converts your code into binary code
- our written code is called **SOURCE CODE**.
# Flow of C program
Source Code ---> Preprocessing ----> Compiler ----(Assembly code)--> Assembler --(Object code)----> Linker (addition of library files here) ----- (final machine code) ---> Loader ----> Primary Memory (RAM) (the final program is loaded here)


- **ASSEMBLY**(CODE) is a low-level programming language that is specific to a particular computer architecture. It is a human-readable representation of machine code, which is the binary code that a computer's central processing unit (CPU) can execute directly. Assembly language uses mnemonic codes and symbolic names to represent the machine instructions and memory addresses. in a `.s` file
- the preprocessing handles the `#include`, `#define` and removes comments to produce pre-processed code saved with a `.i` extension
- The assembler converts the assembly code into **OBJECT CODE (MACHINE CODE)**. output in a `.o` or `.obj` file
- **LINKER** combines multiple source code files and libraries to make a final executable `.exe` for windows and `.out` for unix based systems to run
- when the execution is completed or an error is encountered, a status code is returned (0 for success).

# Standalone applications v/s Web Apps
- Standalone need to be available locally installed. they are available for only single OS (windows wala linux pe nahi chalega)
- Web apps are available online and are OS-independent
- OS File extensions are responsible for these specific OS programmes. `.exe` for windows, `.dmg` for mac, `.tar, .rpm` for linux
- programming langs are standalone apps and installation is mandatory
- C & C++ are platform dependent languages(windows wala compiler windows pe chalega) and can only create STANDALONE APPLICATIONS
- Rest of the langs are independent and can be used to make both web and standalone

# HelloWorld
```c
#include <stdio.h>     // library
int main()
{
	printf("Hello World");    
	return 0;      // code for successful execution
}
```

# Variables (Named Memory Location)
- a computer has many memory locations and each location has an address ( a +ve integer) 
- to store a value in memory we use a identifier (variable name to set a reference)
- `datatype identifier = value;` for declaration or `datatype identifier;` for initialisation

**HOW TO PRINT A VARIABLE?**
we need to specify the format specifier and then the name
`printf("%d", variableName)`

# Data Types
Primary data types in C are fundamental building blocks for representing basic values in a program. They are directly supported by the language and are used to define variables that store specific types of data. Here, I'll explain each primary data type in detail:

1. **int (Integer):**
    
    - Represents whole numbers without decimal points.
    - Size depends on the architecture of the system; typically, it is 2 or 4 bytes.
    - Example: `int age = 25;`
    - `%d` to display (format specifier)
1. **float (Floating-Point):**
    
    - Represents single-precision floating-point numbers.
    - Typically 4 bytes in size. 32 bits of precision. 6-7 decimals
    - Example: `float price = 12.99;`
    - `%f` to display
1. **double (Double Precision):**
    
    - Represents double-precision floating-point numbers.
    - Larger and more precise than `float`. 64 bit precision. 15-16 decimals
    - Typically 8 bytes in size.
    - Example: `double distance = 123.456;`
    - `%lf` to display
1. **char (Character):**
    
    - Represents individual characters, enclosed in single quotes.
    - 1 byte in size.
    - Example: `char grade = 'A';`
    - `%c` to display
5. **\_Bool or bool (Boolean):**
    
    - Represents boolean values, either `true` or `false`.
    - 1 byte in size.
    - Example: `_Bool isDone = 1;` (1 represents `true`, and 0 represents `false`).
    - `%d` to display
6. **String (Array Of Characters)** : 
	- to make strings using an char array
	- Example `char str[] = "BRO";`
	- `%s` to display

The size of these data types may vary across different systems and compilers, but they maintain a consistent behavior based on the C standard.

### More on Booleans
**bool v/s \_Bool**
In C, the `_Bool` data type and `bool` are essentially the same thing. The `_Bool` type is a built-in type introduced in the C99 standard to represent Boolean values, and `bool` is an alias for `_Bool` introduced in the `<stdbool.h>` header, which is part of the C99 standard as well.

**How to use true/false in code**
to use t/f instead of 1/0 you need to include another library `stdbool.h` for this
```c
#include <stdio.h>
#include <stdbool.h>
int main()
{
    _Bool flag = true;
    printf("%d", flag);
    return 0;
}
```
but returns 0 for false and 1 for true by the normal standard, true and false are just for representation
we can use a conditional to print true and false instead 

### More data types
In addition to the fundamental data types (int, float, double, char, and \_Bool), C provides some qualifiers and modifiers that can be used to create more variations of these data types. Here are some additional primary data types and modifiers:

### Type Qualifiers:

1. **const:**
    
    - Indicates that a variable's value cannot be modified after initialization.
    - Example: `const int MAX_VALUE = 100;`
2. **volatile:**
    
    - Informs the compiler that the variable can be changed at any time, without any action being taken by the code the compiler finds nearby.
    - Example: `volatile int sensorValue;`

### Type Modifiers:

1. **short:**
    
    - Modifies the size of an integer to make it occupy less memory. It typically reduces the size to half of the default `int`.
    - Example: `short int smallNumber;` (short int is same as short)
    - `%d`
    - -32,768 to 32,767
2. **long:**
    
    - Modifies the size of an integer to make it occupy more memory. It typically increases the size to twice that of the default `int`.
    - Example: `long int largeNumber;
    - `%ld`
3. **signed:**
    
    - Specifies that a data type can represent both positive and negative numbers (default for int, char).
    - Example: `signed int temperature;
    - `%d`
4. **unsigned:**
    
    - Specifies that a data type can only represent non-negative values.
    - Example: `unsigned int count;`
    - `%u` to display
5. **\_Complex or complex :**
    
    - Represents complex numbers with real and imaginary parts.
    - Example: `_Complex double complexNumber;`
    - if we dont specify any data type in front of complex, then the default is double (bina double likhe bhi chal jayega code)
    - `#include <complex.h>` to work with complex numbers
6. **\_Imaginary or imaginary :**
    
    - Represents imaginary numbers (used with \_Complex).
    - Example: `_Imaginary double imaginaryPart;`

```c
#include <stdio.h> 
#include <complex.h> 
int main() { 
	// Using complex keyword 
	complex z1 = 1.0 + 2.0*I; 
	
	// Using _Complex keyword 
	_Complex z2 = 3.0 - 4.0*I; 
	
	// Perform operations on complex numbers 
	complex sum = z1 + z2; 
	
	// Extract the imaginary part using _Imaginary 
	_Imaginary imagPart = cimag(z2);
	
	// Print the results 
	printf("z1 = %.2f + %.2fi\n", creal(z1), cimag(z1)); 
	printf("z2 = %.2f + %.2fi\n", creal(z2), cimag(z2)); 
	printf("Sum = %.2f + %.2fi\n", creal(sum), cimag(sum)); 
	return 0; 
}
```
7. **long long int** 
	- to represent really large numbers (8 bytes)(-9 quintillian to +9 quintillian)
	- `%lld` to display
	- similarily `unsigned long long` for (0 to +18 quintillion) (`%llu` to display)


### Working with Decimals
**HOW TO SHORTEN DECIMALS**
```c
#include <stdio.h>

int main()
{
    float myFloat = 421.69;
    printf("Default Float  : %f\n", myFloat);
    printf("Float with 2 decimal places   : %.2f", myFloat);
    return 0;
}
```

**CONCEPT OF PRECISION**
```c
#include <stdio.h>

int main()
{
    float myFloat = 11.69;
    double myDouble = 11.69;
    printf("Default Float  : %f\n", myFloat);  // 11.6900000
    printf("Float with 20 decimals: %.20f\n", myFloat);  // 11.68999958038330100000
    printf("Double with same: %.20lf", myDouble);  //  11.69000000000000000000
    return 0;
}
```
hence proves that double is more precise than a float

# Format Specifiers
In C programming, format specifiers are used in functions like `printf` and `scanf` to define the expected type and format of the data being passed or received. Format specifiers begin with the percent sign (`%`) and are followed by a character or characters that specify the conversion type.

Here is a list of common format specifiers used in the `printf` function:

1. **Integer Specifiers:**
    
    - `%d`: Decimal (int)
    - `%u`: Unsigned decimal (unsigned int)
    - `%ld`: Long decimal (long)
    - `%lu`: Long unsigned decimal (unsigned long)
    - `%lld`: Long long decimal (long long)
    - `%llu`: Long long unsigned decimal (unsigned long long)
    - `%x` or `%X`: Hexadecimal (int)
    - `%o`: Octal (int)
2. **Floating-Point Specifiers:**
    
    - `%f`: Floating-point (float or double)
    - `%lf`: Double-precision floating-point (double)
    - `%e` or `%E`: Scientific notation (float or double)
    - `%g` or `%G`: Compact representation (float or double)
3. **Character Specifiers:**
    
    - `%c`: Character
    - `%s`: String (array of characters)
4. **Pointer Specifier:**
    
    - `%p`: Pointer
5. **Special Specifiers:**
    
    - `%%`: Literal percent sign
6. **Width and Precision Specifiers:**
    
    - `%[width]specifier`: Specifies the minimum width of the field.
    - `%.[precision]specifier`: Specifies the number of digits after the decimal point for floating-point numbers.
7. **Extras**
	
	- Left Align `printf("%-100d %d", num, num+1);` adds whitespaces to the right to align to the left
	- Zero Padding `printf("%06d", num);` pads with zeroes instead of whitespaces

# Arithmetic & Assignment Operators
`+` addition, `-` subtraction , `/` division, `*` multiply  , `--` decrement , `++` increment, `%` modulus

`+=`, `*=`, `/=` and `-=` are also available for assignment
- there is no such thing as floor division `//` because the normal division itself is floor if we have int data type eg : `int x = 10; int y = 4;` then x/y = 2 instead of 2.5 because int cannot have decimals
- there is no operator for doing power, we have `pow` which is discussed in [[#Useful MATH Functions]]

**HOW TO GET DECIMALS THEN??**
convert denominator and final reference variable to float
```c
#include <stdio.h>
int main()
{
    int x = 10;
    float y = 4;
    float z = x/y;
    printf("%f", z);
    return 0;
}
```
# Taking Input (scanf)
```c
#include <stdio.h>

int main()
{
    int num, int num2;
    printf("Enter your numbers  : ");
    scanf("%d %d", &num, &num2);  // way to accept 2 vars in a single scan
    return 0;
}
```
in this scan %d are spaced by a single space, so while doing your input you can either put a space to enter your second input or simply press enter to go to the next line and then input your second number, works either way.

another example for better understanding : 
```c
#include <stdio.h>

int main()
{
    char name[25], last[25];
    printf("Enter your name and lastname : ");
    scanf("%s dawg %s", &name, &last);
    printf("\nYour name is %s and lastname is %s", name, last);
    return 0;
}
```
here, you will have to input `swayam dawg duhan` for it to read data correctly

# Strings
- array of characters, terminated by null character `\0`
```c 
// initializing
char greeting[20]; // mentioning size is necessary
// declaring
char greeting[6] = {'H', 'e', 'l', 'l', 'o', '\0'}; 
// or 
char greeting[] = "Hello";
```

- taking inputs is kinda tricky, as an array size cannot be changed after execution (shit aint dynamic), we need to specify the array size before hand

```c
#include <stdio.h>
int main()
{
    char name[25];
    printf("Enter your name and lastname : ");
    scanf("%s", &name);
    printf("\nYour name is %s", name);
    return 0;
}
```

#### HOW TO HANDLE A STRING WITH SPACES???
there are 2 methods - 
1. **using `fgets()` method (safe)**
	- it is an alternative for scanf (also used to read from files, discussed later)
	- it is a part of `<stdio.h>` library
	- it takes 3 inputs, var-name, size of variable and the file stream (or simply stdin which is default) to read characters
	- it reads characters until a newline character appears or n-1 amount of characters are already read
	- prevents BUFFER OVERFLOW(array se zyada characters scan ho jana) by only reading the n amount of characters from sentence

```c
#include <stdio.h>
int main()
{
    char input[100];
    printf("Enter your sentence : ");
    fgets(input, sizeof(input), stdin);  // we can simply put 100 instead of sizeof
    printf("\nYour sentence is : %s", input);
    return 0;
}
```

2. **using `%[characters]` method**
	- this makes the scan to read all characters until a certain character set or character is present in the string 
	- eg : `%[^\n]` this makes scanf to read until a newline is detected, `^` means it will match any character that is not present in the character set
	- eg : `%[^,]` will read until a comma appears

```c
#include <stdio.h>

int main()
{
    char name[25];
    printf("Enter your name and lastname : ");
    scanf("%[^\n]", &name);             // input = swayam duhan
    printf("\nYour name is %s", name);  // output displayed correctly
    return 0;
}
```

***NOTE :*** when you take input by `fgets` method, the last character `\n` is captured by the method and is given as the last character of string
so to fix it we can do :  (simple text formatting)
`strname[strlen(strname) - 1] = '\0'`, dont forget to `#include <string.h>` at the top

- to convert to uppercase, you can use `toupper()` method

# Useful MATH Functions
to use, do `#include <math.h>`

```c
#include <stdio.h>
#include <math.h>

int main()
{
    double a = sqrt(9);  // for sqaure root
    double b = pow(5,2); // for power
    int c = round(3.6); // for rounding off
    int d = ceil(3.2); //  for round up to next number
    int e = floor(3.8); // for round down
    double f = fabs(-100); // for absolute value
    double g = log(2); // natural log (ln)
    double h = sin(45);
    double i = cos(45);
    double j = tan(45*M_PI/180); // M_PI represents value of pi
    printf("%lf", g);
    return 0;
}
```

similar to `M_PI`, we have `INFINITY` for infinity and `-INFINITY` for negative infinity

# Other Operators
**RELATIONAL OPERATORS**
`==`, `!=`, `<`, `<=`, `>`, `>=`

**LOGICAL OPERATORS**
`&&` - AND, `||` - OR, `!` - NOT

**BITWISE OPERATORS**
they are used to perform operations at bit level, the bits of both numbers get lined up when 2 number manipulation is present
1. Bitwise AND (`&`) - agar dono 1 hai to 1 nahi to 0. 
2. Bitwise OR(`|`) - ek bhi 1 hai to 1, agar dono 0 hai to 0
3. Bitwise XOR(`^`) - agar dono ke bits alag hain to 1, nahi to 0.
4. Bitwise NOT(`~`) - number ke bits ko flip krdeta(0 ka 1, 1 ka 0).
5. Left Shift (`<<`) - shifts bits of left operand to left by specified number `num << 2`, this means multiplication by 2^2.
6. Right Shift(`>>`) - shifts to the right, division by 2 to the power specified num

# Conditional Statements
- if-else same as java, terniary operator `?` also available
- **switch case** statements also same as java

# Functions in C
`int main()` itself is a function that the compiler finds to run the program
to define a function, `returnType funcName(args){}`
`void` for no return shit

```c
#include <stdio.h>

double square(double x){
    return x*x;
}

int main()
{
    double squared = square(5);
    printf("%lf", squared);
    return 0;
```

when you call the function before defining it, you can run into some errors like 
- c doesnt care about if all the arguments have been given in the function or not, it will still compile and execute and give partial result. 
- it will give random errors like implicit function declaration, type mismatch and undefined reference

# Function Prototypes
- it is a function declaration without a body before main
- it ensures that call to the function is made with correct arguments
- no issues of maintaining function order

```c
#include <stdio.h>

double square(double x, double num); // args ka naam same hona zaruri ni hai, chahe mention hi mat karo var names

int main()
{
    double squared = square(5,10);
    printf("%.lf", squared);
    return 0;
}

double square(double x, double num){
    printf("\nYour number is %.lf\n", num);
    return x*x;
}
```

# Some String Functions

```c
#include <stdio.h>
#include <string.h>

int main()
{
    char name[] = "Swayam";
    char lname[] = "Duhan";

    strupr(name); // to uppercase
    strlwr(name); // to lowercase
    strcat(name, lname); // appends string2 to string1
    strncat(name, lname, 3); // appends n characters from s2 to s1
    strcpy(name, lname); // copies s2 to s1
    strncpy(name, lname, 3); // copies n chars from s2 to s1

    strset(name, '?'); // changes all letters of string to specified letter
    strnset(name, '?', 3); // changes first n letters
    strrev(name); // reverses a string
    printf("%s", name);

    int result = strlen(name); // length of string
    int result = strcmp(name, lname); // returns 0 if strings equal , read more online
    int result = strncmp(name, lname, 2); // compares first n chars
    int result = strcmpi(name, lname); // ignores case and compares (not case sensitive)
    int result = strnicmp(name, lname, 2); // ignores case and compares n chars
    
    printf("%d", result);
    return 0;
}
```

- more string methods are available but before that we should understand pointers

# Loops
- for, while, do while, break, continue same as java

# Arrays
- a structure to store many values of the same data type

**TO DECLARE**
```c
double prices[] = {1.0, 15.0, 6.0, 5.5};
```
**TO INITIALISE AND THEN SET VALUE**
```c
double prices[5];
prices[1] = 5.5;
```
**HOW TO GET THE LENGTH OF AN ARRAY??**
- the `sizeof()` function will return the byte size of the array , i.e, size of data type multiplied by number of items
- so to get the length, we can divide size of array in bytes by size of the data type in bytes
```c
#include <stdio.h>
int main()
{
    double prices[] = {5.0, 5.5, 10.2, 15.0};
    int length = sizeof(prices)/sizeof(double); // or sizeof(prices[0]) instead of double
    printf("%d", length);
    return 0;
}
```

**2D ARRAYS**
- in C, it is not necessary to specify number of rows. only columns are necessary
```C
int nums[3][2]; // initialization (rows, columns)
int numbers[][] = {{1,2,3}, {4,5,6}, {7,8,9}};
```

**PRINTING 2D ARRAYS**
```C
#include <stdio.h>

int main()
{
    int nums[][3] = {{1,2,3}, {4,5,6}, {7,8,9}, {10,11,12}};
    int rows = sizeof(nums)/sizeof(nums[0]);
    int columns = sizeof(nums[0])/sizeof(nums[0][0]);
    for(int i = 0; i < rows; i++){
        for(int j = 0; j < columns; j++){
            printf("  %d  ", nums[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```

# Array Of Strings
- it is a 2d array of char
eg : 
```c
#include <stdio.h>

int main()
{
    char cars[][20] = {"Mustang", "Ford", "Camaro", "Lambo"};
    int length = sizeof(cars);
    printf("%d", length);
    return 0;
}
```
- use `strlen(cars[0])` to get the length of a specific string, in the above example the sizeof will return 20 while strlen will return actual string length
- however, `cars[1] = "Dodge"` is not possible directly like normal arrays, instead we have to use the strcpy method in the below way
```c
#include <stdio.h>
#include <string.h>

int main()
{
    char cars[][20] = {"Mustang", "Ford", "Camaro", "Lambo"};
    strcpy(cars[0], "Dodge");
    printf("%s", cars[0]);  // prints Dodge
    return 0;
}
```


# Swapping 2 Variables
```c
#include <stdio.h>
#include <string.h>

int main()
{
    char a[15] = "hello";
    char b[15] = "bye";
    char temp[15];
    strcpy(temp, a);
    strcpy(a, b);
    strcpy(b, temp);
    printf("a is %s and b is %s", a, b);
}
```
- here, if we dont mention the array size in brackets then we will run into an error when size of a is bigger than b.

# Using BUBBLE SORT to sort an array

- the basic concept is to check the numbers at the current index and the next index, if aage wala chota hai to swap kardo
- this will make the biggest number go to the end and smallest in beginning
- by ChatGPT, Bubble sort is a simple sorting algorithm that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The pass through the list is repeated until the list is sorted. The algorithm gets its name because smaller elements "bubble" to the top of the list.
- it is very slow and complex and suitable for only educational purposes (easy shit) and small datasets
- time complexity : O(n^2)

```c
#include <stdio.h>

int main()
{
    int nums[] = {6,3,7,2,5,11,10};
    int length = sizeof(nums)/sizeof(int);
    for(int j = 0; j < length - 1; j++){
        for(int i = 0; i < length - 1; i++){
            if (nums[i] > nums[i+1]){
                int temp = nums[i];
                nums[i] = nums[i+1];
                nums[i+1] = temp;
            }
        }
    }

    for(int i = 0; i < length; i++){
        printf("\n%d", nums[i]);
    }
    return 0;
}
```

we need 2 loops for this, it will iterate through the array length - 1 times and in each iteration swap the larger number by the smaller number as explained above
in each iteration, the largest number gets placed at the end 
basically, in the first iteration 11 will be pushed all the way back to the last

**OPTIMISING BUBBLE SORT** - 
we can reduce the workload and execution time by doing `i < length - j - 1` in the code
WHY?? because in each iteration the large number gets placed at the last and we need not check for it again
logic : after first iteration, the last element will be 11 
in the second iteration, the last if statement will check if 10 > 11 which is completely unnecessary 
so, after every n iterations, n large elements get placed at the end

# Structs
(similar to structs in solidity)
- collection of related members (different variables) under one name
- very similar to classes in other languages but doesnt have any methods
- listed under one name in a block of memory
- can be of different data types

```c
#include <stdio.h>
#include <string.h>

struct Person
{
    char name[25];
    int age;
};

int main()
{
    struct Person person1;
    person1.age = 18;
    strcpy(person1.name, "Swayam");
    printf("\nYour name is %s and age is %d", person1.name, person1.age);
    return 0;
}
```
- here, person1 is the name of an instance of Person struct

**TO INITIALISE WITH VALUES IN A SINGLE LINE**
```c
struct Person person1 = {"Swayam", 18};
printf("\nYour name is %s and age is %d", person1.name, person1.age);
```
in the above example the order in which you pass info matters

```c
 struct Person person1 = {
        .age = 18,
         .name = "swayam"
         };
printf("\nYour name is %s and age is %d", person1.name, person1.age);
```
in this way, you need to specify which argument you are giving

- we can also create an array of structs like other languages

# Typedef 
- used to give an existing data type a nickname
- useful to reduce number of words typed (no special use case as such)
- makes code more readable

simple use - 
```c
#include <stdio.h>

typedef int myInt;
int main()
{
    myInt num = 25;
    printf("%d\n", num);
    hello();
    return 0;
}

void hello()
{
    myInt num = 20;
    printf("%d", num);
}
```
as seen in the code above, you should define it outside the main function so that other functions can also use it.

usage with strings - 
```c
#include <stdio.h>
typedef char User[25];
int main()
{
    User user1 = "swayam";
    printf("%s\n", name);
    return 0;
}
```

usage with structs - 
```c
#include <stdio.h>
typedef struct
{
    int x;
    int y;
} Num; 

int main()
{
    Num nums = {5, 7};    // here the whole syntax of struct <name> is replaced by Num
    printf("%d %d", nums.x, nums.y);
    return 0;
}
```


# enum
- user defined data type that consists of a set of named integer constants
- in real world, can be used to define ERROR_CODES or GAME_OPTIONS(NEW_GAME, LOAD_GAME, SAVE_GAME etc.)
- they dont have strings attached to them, means you cant access the strings they are referenced to
- by default the numbering starts from 0 but we can specify custom numbers like in the example below

```c
#include <stdio.h>

enum Day{SUNDAY = 1, MONDAY = 2, TUESDAY = 3, WEDNESDAY = 4, THURSDAY = 5, FRIDAY = 6, SATURDAY = 7};

int main()
{
    printf("%d", today);
    return 0;
}
```

you can do a switch case to check todays day in the above example : 
```c
#include <stdio.h>

enum Day{SUNDAY = 1, MONDAY = 2, TUESDAY = 3, WEDNESDAY = 4, THURSDAY = 5, FRIDAY = 6, SATURDAY = 7};

int main()
{
    enum Day today = TUESDAY;
    switch(today){
    case SUNDAY :   // you can either write SUNDAY or 1, both are same
        printf("Today is Sunday");
        break;
    case MONDAY :
        printf("Today is Monday");
        break;
    case 3 :
        printf("Today is Tuesday");
        break;
    case 4 :
        printf("Today is Wednesday");
        break;
    case THURSDAY :
        printf("Today is Thursday");
        break;
    case 6 :
        printf("Today is Friday");
        break;
    case SATURDAY :
        printf("Today is Saturday");
        break;
    default :
        printf("Aaj kuch bhi nahi hai T-T");
        break;
    }
    return 0;
}
```

# Generating a Random Number
- they are statistically random so dont use for cryptography
- In C, you can generate random numbers using the `rand()` function from the `stdlib.h` library. However, it's important to note that the `rand()` function generates pseudorandom numbers, meaning the sequence of numbers it produces is determined by an initial seed value. To get different sequences of random numbers, you can set a different seed using the `srand()` function.
- the `rand()` function gives a random number between 0 and 32767
Here's a simple example of generating random numbers in C:

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

int main()
{
    srand(time(0));
    int random = (rand() % 100) + 1;
    printf("%d", random);
    return 0
```
rand() % 100 will give a random number between 0 and 99 and then +1 will make it between 1 and 100.

# Memory Addresses
- memory is an array of bytes within RAM(street)
- memory block is a single unit (byte) within memory used to hold some value 
- memory address is the address of where that memory block is located

**TO GET THE ADDRESS OF A VARIABLE**
```c
#include <stdio.h>
int main()
{
    char a = 'X';
    char b = 'Y';
    char c = 'Z';
    printf("%p\n", &a);  // 000000000061FE1F is returned
    printf("%p\n", &b);  // 000000000061FE1E is returned
    printf("%p\n", &c);  // 000000000061FE1D is returned
    return 0;
}

```

- `%p` is the format specifier here and `&` is the operator for getting the address of a variable
- notice how there is only a difference of 1 in the memory addresses, this is because char uses up only 1 memory block (1 byte), however if we use int then there would be a difference of 4 because it takes up 4 bytes

# Pointers
- Pointers in C are variables that store memory addresses. They are a powerful feature that enables direct manipulation of memory, dynamic memory allocation, and efficient data access. Understanding pointers is fundamental for programming in C.
- In a 32-bit system, where memory addresses are typically represented using 32 bits, pointers are usually 4 bytes in size. This is because 2^32 memory addresses are possible, and each address corresponds to a byte in memory. In a 64-bit system, where memory addresses are represented using 64 bits, pointers are typically 8 bytes in size. This allows for a much larger address space (2^64 possible addresses).

- the asterisk `*` means the ***in-direction operator***.
```c
int num = 42;
int *pNum = &num; // Pointer initialized with the address of 'num'
```
here's a pointer pointed to an int memory address

**ADVANTAGES -**
1. Less time in program execution
2. we can create data structures like LinkedList, Stack, Queue using pointers
3. dynamically memory allocation
4. returning more than one value from function
5. searching and sorting large data very easily

*Naming Convention :*  small p in front of variable name then basic camel case

**DEFERENCING A POINTER (ADDRESS USE KARKE VALUE NIKAALNA)**
use a `*` asterisk again 
```c
#include <stdio.h>
int main()
{
    int num = 69;
    int *pNum = &num;
    int deferencedNum = *pNum;
    printf("%d", deferencedNum);
    return 0;
}
```
or simply do `printf("%d", *pNum)`

**GOOD PRACTICE TO DECLARE POINTERS (INITIALIZING AND THEN DECLARING**
```c
#include <stdio.h>

int main()
{
    int age = 18;
    int *pAge = NULL;
    pAge = &age;
    printf("%p", pAge);
    return 0;
}
```

# File Handling
1. **OPENING AND CLOSING A FILE**
```c
FILE *filePointer = fopen("example.txt", "r"); // opening
fclose(filePointer)   // closing
```

- while opening, the second argument takes either `r` for reading, `w` for writing(overwrites existing data in file), `a` for appending
- appending uses the same methods as writing, it just doesn't overwrite
- writing will remove all the existing data and write new data
- `FILE` is the data type here to begin file handling
- when file doesnt open (basically koi opening error ya galat path diya ho), then `NULL` is returned so you can handle errors accordingly

2. **WRITING**
	1. fputs() - to write a single character to the file
	2. fputs() - to write a string to the file
	3. fprintf() - to write formatted data to the file
```c
#include <stdio.h>

int main()
{
    FILE *f = fopen("swayam.txt", "w");
    int value = 55;
    fputc('C', f);
    fputs("\nHello Bro", f);
    fputs("\nThis string got appended", f);
    fprintf(f, "\nThe Value is : %d", value);
    fclose(f);
    return 0;
}
```
the above code returns -
```txt
C
Hello Bro
This string got appended
The Value is : 55
```

**why didn't it overwrite??**
because in this code, file open kari aur jab fputc kara to sab overwrite hokar C aagaya aur uske baad sab append hota gaya 
ek baar open krne pe sab append hota jayega jab tak close ni karoge
overwrite krne ke liye re-open krna padega

3. **READING**
- fgetc() - to get character
```c
#include <stdio.h>

int main()
{
    FILE *f = fopen("swayam.txt", "r");
    char letter = fgetc(f);  // returns 1st letter
    char letter2 = fgetc(f); // returns 2nd letter
    printf("%c %c", letter, letter2);
    fclose(f);
    return 0;
}
// fgetc will return the next character every time we call it and return NULL when the file finishes, similar for fgets
```
so the below example will print the whole txt letter by letter
how? - fgetc() returns EOF when there is nothing else to get anymore which means END OF FILE
```c
#include <stdio.h>

int main()
{
    FILE *f = fopen("swayam.txt", "r");
    char letter;
    while((letter = fgetc(f)) != EOF){
        printf("%c", letter);
    }
    fclose(f);
    return 0;
}
```
why did we do `letter = fgetc(f)` inside the while loop condition.. this is because if we called the fgetc 2 times in the printf and condition then it would get called 2 times, basically we would skip 1 letter in each iteration this way

- fgets() - to read a line string from file
```c
#include <stdio.h>

int main()
{
    FILE *f = fopen("swayam.txt", "r");
    char buffer[100];
    fgets(buffer, 100, f);
    printf("%s", buffer);
    return 0;
}
```
this above program will read the first line from the file
syntax - `fgets(buffer string jismein data daalna, integer value of jitne characters chaiye, file pointer)`

another example - 
```c
#include <stdio.h>

int main()
{
    FILE *f = fopen("swayam.txt", "r");
    char buffer[100];
    fgets(buffer, 10, f);
    printf("%s", buffer);
    fgets(buffer, 10, f);
    printf("%s", buffer);
    return 0;
}
```
in this code, maanlo first line mein 15 chars hain then pehle fgets se 10 char read kiye then second fgets se agle 5 char read kiye aur next line pe nahi gaya jabki integer value abhi bhi 5 ki bach rahi thi, this is because fgets() only reads a line
agar dobara se fgets() use krenge tab jaake next line read hogi

**TO READ WHOLE DOCUMENT**
- fgets returns NULL when file ends
```c
#include <stdio.h>
int main()
{
    FILE *f = fopen("swayam.txt", "r");
    char buffer[255];
    while(fgets(buffer, 255, f) != NULL){
        printf("%s", buffer);
    }
    return 0;
}
```

- fscanf() - to read formatted data

4. **ERROR HANDLING**
- errors can be handled using `feof()` and `ferror()` - read about them online

5. **DELETING A FILE**
- for this we can use the `remove()` method
- it returns 0 for success
```c
#include <stdio.h>
int main()
{
    if (remove("swayam.txt") == 0){    // dont use pointer in place of file address
        printf("Successfully Deleted!");
    } else {
        printf("Error in deletion!");
    }
    return 0;
}
```






