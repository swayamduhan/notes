**TYPES OF MEMORY**
In JVM, There exists a *STACK* and a *HEAP*
The stack follows the Last In, First Out concept. all the local variables inside a method are stored here. (arguments)
the variable instances are stored in heap
each class instance created has its own address through which it is linked with the stack.

**HOW TO GET RANDOM NUMBER**
use Math.random() - it produces a random double between 0 and 1
so to get an integer between 0 and 100, multiply it by 100
```java
int randNumber = (int)(Math.random()*100)
```

