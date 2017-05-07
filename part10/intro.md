# Introduction

## Pure Functions
Functions that have no side effect, meaning they return a value without,
- modifying a variable
- modifying datastructure in place
- setting a field
- throwing exception or haulting
- i/o operation

## Function in Scala
Function f with input type A and output type B is represented as A => B read as 'a to b'. This function f relates every value of type A to exactly one value of type B determined soly by the value of A. Any change of state of internal or external process is irrelavent to computation of f(a) - remember definition of pure function. 

### Function 
-block of code with no side effects.
### Procedure
-parameterized block of code that may have side effects.

## Referential transperancy
- An expression e is referentially transparent if, for all programs p, all occurrences of e in p can be replaced by the result of evaluating e without affecting the meaning of p. A function f is pure if the expression f(x) is referentially transparent for all referentially transparent x.

- a fancy way of saying, if you replace an expression in a program with it's value, the program remains unchanged.

### E.g:
- String reverse is referrentially transparent

    val x = "Hello"

    val y = x.reverse

    val z = x.reverse

    y and z are same because reverse on input x produces exactly one output

- StringBuilder's append is not referentially transparent

    val x = new StringBuilder("Hello")

    val y = x.append(" World") // y is "Hello World" and x is also "Hello World"

    val z = x.append(" World") // z and x are both "Hellow World World". Note that x is no longer same after the call to append. The output of append on x(function invoked multiple times) does not produce exactly one output

