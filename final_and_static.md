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
