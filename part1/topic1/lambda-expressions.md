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

// expect no arg and invoke another method
() -> doSomething(); 
```

Type of any lambda is a functional interface.

Functional Interface is a special interface with one and only one abstract method. It's recommended to use @FunctionalInterface annotation with the interface.

```
@FunctionalInterface
public interface IApplyable<T> {
    public T apply(T t1, T t2);
} 
```

IApplyable is a generic type interface. Therefore any lambda can be assigned to this interface.

```
IApplyable<Employee> i = (Employee e1, Employee e2) -> {    
    e1.setSalary(e1.getSalary() + e2.getSalary());    
    return e1;
};

 IApplyable<String> stringAdder = (String s1, String s2) -> s1 + "_new" + s2;  
```





