## Compile and Run Java Program: It's Two Step Process

Compilation and execution of a Java program is two step process. During compilation phase Java compiler compiles the source code and generates *bytecode*. This intermediate *bytecode* is saved in form of a `.class` file. In second phase, Java virtual machine (JVM) also called Java interpreter takes the `.class` as input and generates output by executing the *bytecode*. Java is an object oriented programming language; therefore, a program in Java is made of one or more classes. No matter how trivial a Java program is, it must be written in form of a class.

## Compile Java Program From Command Prompt

Once the Java program is written and saved, first, it has to be compiled. To compile a Java program from command line we need to invoke the Java compiler by supplying `javac` command. Java compiler comes with JDK (Java Development Kit). JDK is a bundle of software needed for developing Java applications. It includes the JRE (Java Runtime Environment), set of API classes, Java compiler, Webstart and additional files needed to write Java applets and applications.

Now, compile `HelloWorld.java` as follows:

```
[root@host ~]# javac HelloWorld.java
```

The javac `compiler` creates a file called `HelloWorld.class` that contains the bytecode version of the program. As said earlier, the Java bytecode is the intermediate representation of `HelloWorld.java` program that contains instructions the Java interpreter will execute. The Java compiler doesn't execute the Java program \- that is the job of the Java virtual machine. However, the Java virtual machine cannot execute `.java` files directly. The compiler's job is to translate Java source files into "class files" that the virtual machine can execute.

## Run Java Program From Command Prompt

After successful compilation of `HelloWorld.java` to `HelloWorld.class` to actually run the program, we use the Java interpreter, called `java`. To do so, pass the class name `HelloWorld` as a command-line argument, as shown follows:

```
[root@host ~]# java HelloWorld
```

The message `Hello World!` will be printed on the screen as a result of the above command.

It is important to note that in above command we have omitted the `.class` suffix of the byte-code file name (that is `HelloWorld.class` in our case). The `java` command invokes the Java Virtual Machine (will be written JVM hereafter). JVM then loads the specified class mentioned at command line and invokes the method `main` of this class and start executing it, passing it a single argument that is an array of strings. The array of strings passed to `main` is to receive command line arguments. The JVM generally takes the following steps in order to run a Java program.

### Loading of Classes and Interfaces

Loading refers to the process of finding the binary form of a class or interface type with a particular name computed from source code by a Java compiler. This is simply the *bytecode*.

In making initial effort to execute the main method of `HelloWorld` class JVM sees that the class `HelloWorld` is not loaded, means to say that JVM currently does not contain a binary representation of this class . The JVM then uses a class loader to load the class in memory, If the class file is not found at the place then an error is thrown.

### Linking of Classes and Interfaces

Linking is the process of taking a binary form of a class or interface type and combining it into the run-time state of the Java virtual machine, so that it can be executed. A class or interface type is always loaded before it is linked.

Once `HelloWorld` is loaded, it must be initialized before `main` is invoked. And, `HelloWorld` must be linked before it is initialized. Linking involves **verification**, **preparation**, and **resolution**.

- **Verification** ensures that the binary representation of a class or interface is structurally correct. For example, it checks that every instruction has a valid operation code; that every branch instruction branches to the start of some other instruction, rather than into the middle of an instruction; that every method is provided with a structurally correct signature; and that every instruction obeys the type discipline of the Java virtual machine language. If an error occurs during verification, then an instance of the class VerifyError which is a subclass of class LinkageError will be thrown.

- **Preparation** involves creating the static fields (class variables and constants) for a class or interface and initializing such fields to the default values. This does not require the execution of any source code; explicit initializers for static fields are executed as part of initialization, not preparation. Implementations of the Java virtual machine may precompute additional data structures at preparation time in order to make later operations on a class or interface more efficient. One particularly useful data structure is a "method table" or other data structure that allows any method to be invoked on instances of a class without requiring a search of superclasses at invocation time.

- **Resolution** is the process of checking symbolic references from HelloWorld to other classes and interfaces, by loading the other classes and interfaces that are mentioned and checking that the references are correct. 

The resolution step is optional at the time of initial linkage. An implementation may resolve symbolic references from a class or interface that is being linked very early, even to the point of resolving all symbolic references from the classes and interfaces that are further referenced recursively. (This resolution may result in errors from these further loading and linking steps.) This implementation choice represents one extreme and is similar to the kind of "static" linkage that has been done for many years in simple implementations of the C language. 

An implementation may instead choose to resolve a symbolic reference only when it is actively used; consistent use of this strategy for all symbolic references would represent the "laziest" form of resolution. 

In this case, if `HelloWorld` had several symbolic references to another class, then the references might be resolved one at a time, as they are used, or perhaps not at all, if these references were never used during execution of the program.

### Run Java Program - Initialization

The execution of method `main` of class `HelloWorld` is permitted only if the class has been initialized. 

Initialization consists of execution of any class variable initializers and static initializers of the class HelloWorld, in textual order. But before `HelloWorld` can be initialized, its direct superclass must be initialized, as well as the direct superclass of its direct superclass, and so on, recursively. In the simplest case, `HelloWorld` has `Object` as its implicit direct superclass; if class `Object` has not yet been initialized, then it must be initialized before `HelloWorld` is initialized. Class `Object` has no superclass, so the recursion terminates here. 

If class `HelloWorld` has another class `SuperHello` as its superclass, then `SuperHello` must be initialized before `HelloWorld`. This requires loading, verifying, and preparing `SuperHello` if this has not already been done and, depending on the implementation, may also involve resolving the symbolic references from SuperHello and so on, recursively. Initialization may thus cause loading, linking, and initialization errors, including such errors involving other types.

### Run Java Program - Invoking HelloWorld.main

After completion of the initialization for class `HelloWorld` (during which other consequential loading, linking, and initializing may have occurred) the method main of `HelloWorld` is invoked. 

The method main must be declared `public`, `static`, and `void`. It must accept a single argument that is an array of strings.
Finally, A program terminates all its activity and exits when one of two things happens:

1. All the threads that are not daemon threads terminate.
2. Some thread invokes the exit method of class Runtime or class System and the exit operation is not forbidden.

## References

1. http://cs-fundamentals.com/java-programming/how-to-compile-run-java-program-in-linux.php
