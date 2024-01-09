## Classes
**access modifiers, static vs non static, **

a Class is like a blueprint of an object, the JVM makes an object out of the class. 
we can create instances of the class to use the methods of the Class.

eg :
```
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
```
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

```
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
