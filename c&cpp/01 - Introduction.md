
## Basic shit
-  a computer lang is a software, set of rules, set of programs to interact with device
- a compiler is a pre defined program which converts your code into binary code
- our written code is called **SOURCE CODE**.
## Flow of C program
Source Code ---> Preprocessing ----> Compiler ----(Assembly code)--> Assembler --(Object code)----> Linker (addition of library files here) ----- (final machine code) ---> Loader ----> Primary Memory (RAM) (the final program is loaded here)


- **ASSEMBLY**(CODE) is a low-level programming language that is specific to a particular computer architecture. It is a human-readable representation of machine code, which is the binary code that a computer's central processing unit (CPU) can execute directly. Assembly language uses mnemonic codes and symbolic names to represent the machine instructions and memory addresses. in a `.s` file
- the preprocessing handles the `#include`, `#define` and removes comments to produce pre-processed code saved with a `.i` extension
- The assembler converts the assembly code into **OBJECT CODE (MACHINE CODE)**. output in a `.o` or `.obj` file
- **LINKER** combines multiple source code files and libraries to make a final executable `.exe` for windows and `.out` for unix based systems to run
- when the execution is completed or an error is encountered, a status code is returned (0 for success).

## Standalone applications v/s Web Apps
- Standalone need to be available locally installed. they are available for only single OS (windows wala linux pe nahi chalega)
- Web apps are available online and are OS-independent
- OS File extensions are responsible for these specific OS programmes. `.exe` for windows, `.dmg` for mac, `.tar, .rpm` for linux
- programming langs are standalone apps and installation is mandatory
- C & C++ are platform dependent languages(windows wala compiler windows pe chalega) and can only create STANDALONE APPLICATIONS
- Rest of the langs are independent and can be used to make both web and standalone

## HelloWorld
```c
#include <stdio.h>     // library
int main()
{
	printf("Hello World");    
	return 0;      // code for successful execution
}
```

## Variables (Named Memory Location)
- a computer has many memory locations and each location has an address ( a +ve integer) 
- to store a value in memory we use a identifier (variable name to set a reference)
- `datatype identifier = value;` for declaration or `datatype identifier;` for initialisation

**HOW TO PRINT A VARIABLE?**
we need to specify the format specifier and then the name
`printf("%d", variableName)`

## Data Types
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

## Format Specifiers
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

## Operators
`+` addition, `-` subtraction , `/` division, `*` multiply  , `--` decrement , `++` increment, `%` modulus, `+=` and `-=` are also there
- there is no such thing as floor division `//` because the normal division itself is floor if we have int data type eg : `int x = 10; int y = 4;` then x/y = 2 instead of 2.5 because int cannot have decimals

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
## Taking Input (scanf)
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

## Strings
- array of characters, terminated by null character `\0`
```c 
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