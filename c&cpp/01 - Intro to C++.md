- very fast execution
- used in extensive graphic applications
- used in video games
- used in finance industry and trading applications
- extension - `.cpp`
- if using vscode, follow the installation instructions for the compiler in vsc docs
- docs - [click here](https://cplusplus.com)

# Hello World in Cpp
```cpp
#include <iostream>

int main()
{
    std::cout << "Hello world!" << std::endl;
    std::cout << "Hello world!\n";
    std::cout << "Hello world!" << '\n';   // generally used
    return 0;
}

```

- the iostream header file contains basic input output functions
- function making is same as C, return 0 for pass return 1 for error
- `std::cout` stands for standard character output, the angulars `<<` mean output
  basically the angular braces are used to stream the shit to the left hand side thingy
  `<<` is called insertion operator

- `//` for singeline comment and `/*  */`  for multiline

# Data Types

1. `int` - stores only integers no decimals
2. `double` - integer with decimals
3. `char` - single character
4. `bool` - `bool student = false`
5. String - represents a sequence of text
```cpp
std::string name = "Swayam Duhan";
std::cout << name;
```

**PRINTING :**
```cpp
 int age = 18;
std::cout << "You are " << age << " years old." << '\n';
```

# Constants (read only)
```cpp
const int MY_CONSTANT = 70;
```

this variable can not be changed in my program later on now

# Namespaces
In C++, namespaces are used to organize code into logical groups and prevent naming conflicts. They provide a way to encapsulate declarations and definitions within a named scope.

```cpp
#include <iostream>

namespace first {
    int x = 1;
}

int main()
{
    int x = 0;
    std::cout << x << '\n';  // 0
    std::cout << first::x << '\n';  // 1
    return 0;
}
```

**grouped namespaces**
```cpp
#include <iostream>

namespace first {
    namespace second {
    int x = 1;
    }
}

int main()
{
    std::cout << first::second::x << '\n';  // 1
    return 0;
}
```

**using namespace to have ease in typing**
```cpp
#include <iostream>

using namespace std;

int main()
{
    cout << "Hello";
    return 0;
}
```

**how to import only 1 item from the namespace**
```cpp
#include <iostream>

using namespace std::cout   // if you want only std::cout to have a short naming

int main()
{
    cout << "Hello";
    return 0;
}
```

**how to type other namespaces if you are importing only one namespace**
```cpp
#include <iostream>

namespace first {
    int x = 1;
}

namespace second {
    int x = 2;
}

int main()
{
    using namespace first;
    std::cout << x << '\n';
    std::cout << second::x << '\n';
    return 0;
}

```


# Typedef and Using keyword
- typedef is same as c
- convention - type `_t` at the end of the variable


```cpp
#include <iostream>

using text_t = std::string;

int main()
{
    text_t name = "swayam";
    std::cout << name;
    return 0;
}
```



# Arithmetical

- all shit same as C

keep in mind : 
```cpp
#include <iostream>

int main()
{
    int students = 20;
    std::cout << students/3 << '\n'; // 6
    double student = 20;
    std::cout << student/3 << '\n';  // 6.66667
    return 0;
}
```

order of priority -> `%` < mul, div < add sub

# Type Conversion 
- same as C

keep in mind : when doing integer division agar decimals mein answer chaiye to convert denominator into double

# Taking inputs
we use `std::cin` ( character in ) followed by `>>` extraction operator

```cpp
#include <iostream>

int main()
{
    std::string name;
    int age;

    std::cout << "Enter name : ";
    std::cin >> name;
    std::cout << "Enter age : ";
    std::cin >> age;

    std::cout << "Your name is " << name << " and age is " << age;
    return 0;
}
```

however if you want to input a string that contains spaces then it will have an error, for that you will use : 

```cpp
#include <iostream>

int main()
{
    std::string name;

    std::cout << "Enter name : ";
    std::getline(std::cin, name);

    std::cout << "Your name is " << name;
    return 0;
}
```

**how to handle our string input from catching newline character from previous input?**
```cpp
std::string name;

std::cout << "Enter name : ";
std::getline(std::cin >> std::ws, name);

std::cout << "Your name is " << name;
```

# Math functions
you can find all at the web

```cpp
#include <cmath>

std::max(5,4)
std::min(5,4)
pow(5,4)
sqrt(4)
round(4.6) // 5
ceil(4.3) // 5
floor(4.9) // 4
abs(-3) // 3
```

# If-Else, Switch, Ternary, Logical Ops
- all same as C

# String Methods *
- it is not bad stuff like C, v cool

```cpp
std::string name = "swayam";

name.length()
name.empty() // returns boolean
name.clear() // clears string
name.append("duhan") // appends at the end
name.at(index) // to get character at index
name.insert(index, "dawg") // to insert string at index
name.find(" ") // finds index of any shit entered
name.erase(begIndex, endIndex) // to erase a portion of string
```

- you can also do `str1 + " " + str2` in cpp unlike c
# For, While, Do-While loops
- same as C
- break and continue usage is also same

# Functions
- same as C

- you can have multiple functions with same name as long as the arguments are different

# Setting precision of decimals

```cpp

```