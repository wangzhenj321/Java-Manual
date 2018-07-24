## Part 1: Compile-time constant

***References:*** https://stackoverflow.com/questions/9082971/compile-time-constants-and-variables

> A constant variable is a final variable of primitive type or type  String that is initialized with a constant expression (§15.28).

From this definition, we can discern that a constant must be:

- declared `final`
- primitive type or type `String`
- initialized within its declaration (not a `blank final`)
- initialized with a constant expression

What about compile-time constants?

The JLS does not contain the phrase compile-time constant. However, programmers often use the terms compile-time constant and constant interchangeably.


## Part 2: Static variables

***References:*** https://stackoverflow.com/questions/8704423/when-are-static-variables-initialized

> These variables will be initialized first, before the initialization of any instance variables.


## Part 3: Initialization of `final` instance variable

***References:*** https://www.geeksforgeeks.org/instance-variable-final-java/

> If the instance variable declared as final, then we have to perform initialization explicitly whether we are using it or not and JVM won’t provide any default value for the final instance variable.

1. **Initialization before constructor completion:** For final instance variable we have to perform initialization before constructor completion. We can initialize a final instance variable at the time of declaration.

```java
// Java program to illustrate that 
// final instance variable
// should be declared at the 
// time of declaration
class Test {
    final int x = 10;
    public static void main(String[] args)
    {
        Test t = new Test();
        System.out.println(t.x);
    }
}
```

2. **Initialize inside a non-static or instance block:** We can also initialize a final instance variable inside a non-static or instance block also.

```java
// Java program to illustrate 
// that final instance variable
// can be initialize within instance block
class Test {
    final int x;
    {
        x = 10;
    }
    public static void main(String[] args)
    {
        Test t = new Test();
        System.out.println(t.x);
    }
}
```

3. **Initialization in default constructor:** Inside default constructor we can also initialize a final instance variable.

```java
// Java program to illustrate that 
// final instance variable
// can be initialized 
// in the default constructor
class Test {
    final int x;
    Test()
    {
        x = 10;
    }
    public static void main(String[] args)
    {
        Test t = new Test();
        System.out.println(t.x);
    }
}
```
