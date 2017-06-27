# Getting Started

Scana REPL has paste mode to type in multi line code
- Type :paste and hit enter at _scala>_ prompt. Hit cntrl+d to end paste mode.

## object
_object_ keyword creates a new _singleton type_. Declaring _object_ in Scala is like creating an instance of anonymous class.

Note: Scala has no equivalent of _static_ keyword. An _object_ is used in Scala where you might use a class with static members in Java.

## types
### Array
Equivalent of [] in java is _Array_

### Unit
Equivalent of _void_ in java

### Primitive types
Java's primitive types such as int, float are not supported. However Scala has equivalent primitives represented as Int, Float etc.

### Operators
Scala has no special notation of operators.
1 + 2 is nothing but 1.+(2), i.e. calling method '+' on object 1. Again, note that there are no primitives. 1 is an Int object.

Above example introduces another concept. Any method name can be used infix like that, ommitting the dot and paranthesis when calling it with a single argument.

## Higher Order Functions
In Scala, functions are values and can be assigned to variables, stored in data structures and can be passed as arguments to functions. 

Functions that accept functions as arguments are called higher order functions.

### Loops and recursion
Implementing while loop in Scala is possible but rarely necessary and is considered bad practice. Tail recursion is used instead.

### Tail calls
A call is said to be in tail position if the caller does nothing other than return the value of the recursive call.

Use @annotation.tailrec to suggest compiler that we assume the call to be converted to a loop, so the compiler can throw exception if it's not possible.