## Classes
**access modifiers, try catch, throw exception padne hain bhai**

a Class is like a blueprint of an object, the JVM makes an object out of the class. 
we can create instances of the class to use the methods of the Class.

eg :
```java
class Calculator  
{  
    public int add(int num1, int num2) {  
        return num1 + num2;  
    }  
}  
  
public class Main {  
    public static void main(String[] args) {  
        Calculator calc = new Calculator();  
        int result = calc.add(10,20);  
        System.out.println(result);
    }  
}
```

`object_instance.variable_name` to access any variable made inside a class

#### Constructors in Class
they are defined when we create an instance of the class to initialize it and give it some values at its creation.

## Methods (Functions)

They are created using inside a class using this syntax
```java
public class Main {  
    public int addNums(int num1, int num2) {  
        return num1 + num2;  
    }  
    public static void main(String[] args) {  
        int result = addNums(5,7);  
        System.out.println(result);  
    }  
}
```

you need to specify the return type after `static` keyword. if nothing is to be returned, use `void`. 

***NOTE:*** we can also create methods with same name but they should have different parameters.  This is called **METHOD OVERLOADING**
eg :

```java
class Calculator  
{  
    public static int add(int n1, int n2) {  
        return n1 + n2;  
    }  
    public static int add(int n1, int n2, int n3) {  
        return n1 + n2 + n3;  
    }  
}  
  
public class Main {  
  
  
    public static void main(String[] args) {  
  
        int result = Calculator.add(5,6,7);  
        System.out.println(result);  
    }  
}
```

## Static vs Non Static

**STATIC VARIABLES**
In Java, a `static` variable (also known as a class variable) is a variable that belongs to the class rather than to instances of the class. It is shared among all instances of the class, and there is only one copy of the `static` variable that is shared by all objects of the class. The `static` keyword is used to declare a static variable.
```java
MyClass.staticVariable = 10; // Accessing through the class name
```

```java
class Mobile  
{  
    String build;  
    int year;  
    static String name;  
    // static String name = "Apple"; is also cool  
}  
  
public class Main {  
    public static void main(String[] args){  
        Mobile phone1 = new Mobile();  
        phone1.build = "iOS17";  
        phone1.year = 2023;  
        Mobile.name = "iPhone 15";  
        System.out.println(Mobile.name + " has " + phone1.build + " and was made in " + phone1.year);  
    }  
}
```

we can also create Static methods.

**STATIC METHODS**
- we can use static variables in non static methods
```java
class Hello  
{  
    static String name = "Hello";  
    static void speak(){  
        System.out.println(name);  
    }  
}  
  
public class Main {  
    public static void main(String[] args){  
        Hello.speak();  
    }  
}
```

**USING NON STATIC VARS IN STATIC METHODS**
we cannot use them directly in our static methods because they are present in an instance of the class and not the class itself, so it results in a compilation error. 
There are 2 methods to solve this - 
1. Create a new instance inside the static method and then use it
2. Pass in your instance obj in the arguments
```java
class Hello  
{  
    static String name = "Hello";  
    String lastName = "World";  
    static void speak(Hello _instance){  
        System.out.println(name + _instance.lastName);  
    }  
}  
  
public class Main {  
    public static void main(String[] args){  
        Hello helloInst = new Hello();  
        Hello.speak(helloInst);  
    }  
}
```

**WHY IS MAIN STATIC?**
because if it wasnt then we would have to create a instance of its parent class and then use the method main
## Using Constructors
to define values when we create a new class directly in a single line instead of doing `obj.name = "swayam"` 

```java
class Introduce  
{  
    static int age;  
    String name;  
    String place;  
  
    Introduce(String _name, String _place){    // this is the constructor
        this.name = _name;       // works without 'this' as well
        this.place = _place;  
    }  
  
    static     // constructor for all static variables
    {  
        age = 18;  
    }  
}  
  
public class Main {  
    public static void main(String[] args){  
        Introduce person1 = new Introduce("swayam", "faridabad");  
        System.out.println("My name is " + person1.name + ", I live in " + person1.place + " and my age is " + Introduce.age);  
    }  
}
```

in the above code, the static block is executed first as per java hierarchy. it is only called once when the class loads and is not called everytime a new instance is created.
class loads first then objects are instantiated. the JVM has a special place called Class Loader
the constructor is called after the static block to take the values of vars as args.

##### WHAT IS `this` KEYWORD
The `this` keyword in Java is a reference to the current instance of the class. It is primarily used to distinguish between instance variables (fields) and local variables when they have the same name. Here are the main uses of the `this` keyword in Java classes:

1. **Distinguishing Between Instance and Local Variables:**
    
    - When a method has a local variable with the same name as an instance variable, the `this` keyword is used to differentiate between the two.
2. **Referring to the Current Object:**
    
    - Inside an instance method, `this` is implicitly used to refer to the current object. It can be used to access instance variables or call other methods of the same object
    
3. **Returning the Current Object:**
    
    - The `this` keyword can be used to return the current object from a method. This is useful for method chaining.
```java
Introduce speak() {  
    this.name = "rahhhhhhh";  
    return this;  // returns the current instance of class
}
```

##### THE CLASS GETS LOADED INTO CLASS LOADER ONLY AFTER YOU CREATE AN OBJECT. WHAT IF YOU WANT TO LOAD IT WITHOUT INSTANTIATING?
We can use a class in Java called `Class` for this. it uses the Class Loader to achieve this
`Class.forName("class-name")`


## Encapsulation
Encapsulation is one of the four fundamental Object-Oriented Programming (OOP) concepts, and it refers to the bundling of data (attributes) and methods (functions) that operate on the data into a single unit known as a class. Encapsulation helps in hiding the internal implementation details of a class and exposing only what is necessary for the outside world to interact with.

Key principles of encapsulation include:

1. **Data Hiding:**
    
    - Encapsulation allows you to hide the implementation details of an object and only expose a well-defined interface.
    - Internal details, such as the state of an object (attributes or fields), are kept private within the class.
2. **Access Control:**
    
    - Access modifiers (like `private`, `protected`, and `public`) are used to control the visibility of fields and methods.
    - Private members can only be accessed within the class, protecting the internal state from direct external modification.
3. **Getters and Setters:**
    
    - Encapsulation often involves providing public methods (getters and setters) to access and modify the private fields.
    - This allows controlled access to the internal state, enabling validation or additional logic as needed.
4. **Modularity:**
    
    - Encapsulation promotes modularity by grouping related functionalities and data together.
    - Changes to the internal implementation details of a class do not affect other parts of the program as long as the public interface remains the same.
eg : 
```java
public class BankAccount {
    private String accountHolder;
    private double balance;

    // Constructor
    public BankAccount(String accountHolder, double initialBalance) {
        this.accountHolder = accountHolder;
        this.balance = initialBalance;
    }

    // Getter for accountHolder
    public String getAccountHolder() {
        return accountHolder;
    }

    // Getter for balance
    public double getBalance() {
        return balance;
    }

    // Setter for balance with validation
    public void setBalance(double newBalance) {
        if (newBalance >= 0) {
            this.balance = newBalance;
        } else {
            System.out.println("Invalid balance. Balance cannot be negative.");
        }
    }

    // Additional methods can be defined to perform operations on the account
}

```

## Access Modifiers
In Java, access modifiers are keywords used to control the visibility or accessibility of classes, methods, and fields (variables) within a program. These modifiers help enforce encapsulation and define the level of access that other classes or code can have to the elements of a class.

Java has four main access modifiers:

1. **Public (`public`):**
    
    - The `public` modifier makes a class, method, or field accessible from anywhere in the program.
    - If a class or method is marked as `public`, it can be used by other classes even if they are in different packages.
    
2. **Private (`private`):**
    
    - The `private` modifier restricts the access of a class, method, or field to only within the same class.
    - Private members are not visible or accessible from outside the class, even from subclasses.
    
3. **Protected (`protected`):**
    
    - The `protected` modifier allows access to a class, method, or field from within the same package and from subclasses, even if they are in different packages.
    - Protected members are not accessible by classes outside the package unless they are subclasses.
    
4. **Default (Package-Private):**
    
    - If no access modifier is specified (also known as package-private or default access), the class, method, or field is accessible only within the same package.
    - Default members are not accessible from outside the package.


Access modifiers provide a mechanism to control the visibility of class members and support the principles of encapsulation. By choosing the appropriate access modifier, you can restrict or allow access to specific elements of a class, helping to create well-organized and maintainable code.

```java
class Human  
{  
  private String name;  
  private double netWorth;  
  
  public void setName(String _name){  
      this.name = _name;  
  }  
  public void setNetWorth(double _worth){  
      this.netWorth = _worth;  
  }  
  
  public String getName(){  
      return this.name;  
  }  
  public double getNetWorth(){  
      return this.netWorth;  
  }  
}  
  
public class Main {  
    public static void main(String[] args)  {  
        Human person1 = new Human();  
        person1.setName("swayam");  
        person1.setNetWorth(1095090.57);  
        System.out.println("The net worth of " + person1.getName() + " is $" + person1.getNetWorth());  
    }  
}
```

## SuperClass and SubClass
super is parent and sub is derived or child
a superclass is inherited or extended by other classes
a subclass inherits the superclass and over that provides additional attributes
It (Inheritance) allows code reuse and prevents DRY

```java
class Animal  
{  
    public Animal(){  
        System.out.println("in Animal");  
    }  
    public void speak(){  
        System.out.println("Hello lil bro");  
    }  
}  
  
class Dog extends Animal  
{  
    public Dog(){  
        System.out.println("in Dog");  
    }  
}  
  
public class Main {  
    public static void main(String[] args)  {  
        Dog dalmatian = new Dog();  
        dalmatian.speak();  
    }  
}
```

- java runs both the constructors (first the superclass then the subclass)
- the subclass has methods from superclass automatically 

**NOTE** : if we have parameterized constructors in both sub and super and we create an instance of the sub using parameters,
then the para constructor of the sub will run and default constructor of super will run, para wala ni chalega
you can run the code below to test
```java
class Animal  
{  
    public Animal(){  
        System.out.println("in Animal");  
    }  
    public Animal(int a){  
        System.out.println("In Parameterized Animal");  
    }  
}  
  
class Dog extends Animal  
{  
    public Dog(){  
        System.out.println("in Dog");  
    }  
    public Dog(int a){  
        System.out.println("In Parameterized Dog");  
    }  
}  
  
public class Main {  
    public static void main(String[] args)  {  
        Dog dalmatian = new Dog(5);  
    }  
}
```

#### The SUPER Keyword
`super` represents the immediate parent class
Use Cases :-
1. to run methods from the parent class eg : `super.bark()`, same as openZeppelin in solidity
2. to run constructors from the parent class
eg : if in the above example, we specify that we need to run the parameter constructor in parent then only parameterized constructor will run
```java
class Dog extends Animal 
{
	public Dog(int a){
		super(a);
		System.out.print("In parameter Doggo")
	}
}
```

- by default, all the constructors in classes have a `super()` at the beginning
```java
public Dog(){
	a = 5;
}
// is same as 
public Dog(){
	super();
	a = 5;
}
```


**SO WHAT IS THE MEANING OF SUPER IN THE UPPERMOST PARENT CLASS  ????**
Every class in java extends `Object` class by default and we dont need to specify it
```java
class Animal{}
// is same as
class Animal extends Object{}
```

**HOW TO RUN BOTH PARAMETERIZED AND DEFAULT CONSTRUCTOR OF A CLASS??**
using the `this()` keyword

```java
class Animal  
{  
    public Animal(){  
        System.out.println("in Animal");  
    }  
    public Animal(int a){  
        this();  
        System.out.println("In Parameterized Animal");  
    }  
}  
  
public class Main {  
    public static void main(String[] args)  {  
        Animal dog = new Animal(5);  
    }  
}
```