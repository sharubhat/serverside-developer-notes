# Java 8 - lambda expressions

Lambdas are briefly and clearly expressed single method classes that represent a behavior.  They can either be assigned to a variable or passed around to other methods just like we pass data as arguments.

**Examples:**

```
// concatenate a string
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

**Functional interface:**

```
@FunctionalInterface
public interface IApplyable<T> {
    public T apply(T t1, T t2);
} 
```

IApplyable is a generic type interface. Therefore any lambda can be assigned to this interface as long as they have same number of arguments.

**Assigning lambda to functional interface type:**

```
IApplyable<Employee> i = (Employee e1, Employee e2) -> {    
    e1.setSalary(e1.getSalary() + e2.getSalary());    
    return e1;
};

 IApplyable<Integer> intSummer = (Integer i1, Integer i2) -> i1 + i2;  
```

**Using lambda expressions:**

If the lambda expression is assigned to a function interface with a type, the arguments of lambda expression need not specify the type explicitely; they are inferred.concatenate

```
// Lambda for adding two numbers
IApplyable<Integer> intSum = (i1, i2) -> i1 + i2;
IApplyable<Integer> intProduct = (i1, i2) -> i1 * i2;

// this method adds the two numbers using first lambda expression
private void addInteger(Integer i1, Integer i2) {
    System.out.println("Sum : " + intSum.apply(i1, i2));
} 

// this method multiplies two numbers using second lambda expression
private void multiply(Integer i1, Integer i2) {
    System.out.println("Product : " + intProduct.apply(i1, i2));
} 
```

**Passing lambda as method argument:**

```
public Integer applyBehavior(IApplyable<Integer> applyable, Integer i1, Integer i2) {
    applyable.apply(i1, i2);
} 
```

**java.util.Function package:**

**Predicate** interface has a single method '_test\(T t\)_' which accepts a single argument and returns a boolean.

**Function** interface has a single method '_apply\(T t\)_' which accepts an argument of type T and returns a result of type R by applying specified logic on the input via the apply method.



