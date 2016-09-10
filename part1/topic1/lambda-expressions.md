# Java 8 - lambda expressions

Lambdas are briefly and clearly expressed single method classes that represent a behavior.  They can either be assigned to a variable or passed around to other methods just like we pass data as arguments.  

**Examples:**

```
// concatinate a string 
(String s1, String s2) -> s1+s2; 

// squaring up two integers
(i1, i2) -> i1 * i2;

// Increment salary of Employee 
(Employee e) -> {    
    e.setSalary(e.getSalary() + (e.getSalary() * 0.10));
    return e;
}
```



