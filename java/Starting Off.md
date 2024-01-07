## Introduction
- IDEs -> VSC, IntelliJ Idea(currently using), NetBeans, Eclipse
- Java is WORA -> Write Once Run Anywhere
- Compiler -> jdk (java development kit which includes JRE - Java runtime env which further includes JVM - Java Virtual Machine and libraries) (install LTS versions like Java 17)
- use `java --version` and `javac --version` to check for installation confirmation
- extension `.java`
- for mini runtime in terminal, use `jshell`, we can do `System.out.print("")` to print sum'

## How Java Works?
You write Java Code, then compile it using Javac into bytecode then you run it using JVM which runs on the OS which further runs on hardware
we dont directly convert java code into object code as it is machine specific (windows ka sirf windows pe chalega), so we first convert into bytecode with `.class` extension which is cross platform

## Hello World Program
```
class Main
{
    public static void main(String[] args) 
    {
        System.out.print("Hello");
    }
}
```
 JAVA is an Object-Oriented Language so we need to specify classes for the code. without it wont work.
 also, the Java compiler looks for `public static void main(String[] args)` before compiling, it is the starting point of any java program for execution (think of it as some magic spell)
 - we can write any of `String[] args` or `String args[]` . the usually used is the first one, it is a matter of personal preference. any variable name can be used instead of `args`
 - A class is a object of related code (will be explained later in OOP)
 -  `print` doesn't print stuff in newlines while `println`(short for print line) has `\n` at end of line to print in different lines
### Executing in VSC
`java <java code file>` - to directly run program
`javac <javacode>` - to compile code into .class and then `java <class-name>` to run a certain class (preffered way)
### Using IntelliJ Idea
Simply create a new project and click on run to run your java program, you can also use the above method







