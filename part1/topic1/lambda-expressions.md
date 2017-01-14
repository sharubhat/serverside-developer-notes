# Java 8 - lambda expressions

---

### a\) Lambdas

Lambdas are briefly and clearly expressed single method abstract classes that represent a behavior.  They can either be assigned to a variable or passed around to other methods just like we pass data as arguments.

**Examples:**

```java
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

---

### b\) Functional interface:

```java
@FunctionalInterface
public interface IApplyable<T> {
    public T apply(T t1, T t2);
} 
```

IApplyable is a generic type interface. Therefore any lambda can be assigned to this interface as long as they have same number of arguments.

**Assigning lambda to functional interface type:**

```java
IApplyable<Employee> i = (Employee e1, Employee e2) -> {    
    e1.setSalary(e1.getSalary() + e2.getSalary());    
    return e1;
};

IApplyable<Integer> intSummer = (Integer i1, Integer i2) -> i1 + i2;  
```

**Using lambda expressions:**

If the lambda expression is assigned to a function interface with a type, the arguments of lambda expression need not specify the type explicitely; they are inferred.concatenate

```java
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

```java
public Integer applyBehavior(IApplyable<Integer> applyable, Integer i1, Integer i2) {
    applyable.apply(i1, i2);
} 
```

**java.util.Function package:**

**Predicate** interface has a single method '_test\(T t\)_' which accepts a single argument and returns a boolean.

**Function** interface has a single method '_apply\(T t\)_' which accepts an argument of type T and returns a result of type R by applying specified logic on the input via the apply method.

**Consumer** interface provides single method '_accept\(T t\)'_ which can be used for persisting data, emailing etc.

**Producer** interface provides single method '_get\( \)_' which can be used for fetching data from database, loading data etc.

**BiPredicate**, **BiConsumer** and **BiFunction** are also available.

---

### c\) Default methods:

Interfaces in java 8 can have methods with default implementation. This gives ability to add additional functionalities to already published APIs.

```java
@FunctionalInterface
public interface IApplyable {
    // can have only one abstract method. More than one results in compilation error.
    void apply();

    // default method just for the sake of giving an example
    default String getClassName() {
        return "IApplyable";
    }

    // there can be more than one default method
    default String appName() {
        return "DEFAULT APP";
    }
}
```

If interface A has a default method apply\(\), interface B extends A and also provides a default method apply\(\), the class that implements both A and B inherits apply\(\) method of B as it's the closest.

However, if both A and B provide apply\(\) method and both interfaces are unrelated and a class C implements both of these interfaces, it's **must** provide an implementation of apply\(\) method. If apply method of C has same implementation of B, then C can reference to B's method as B.super.apply\(\);

```java
class C implements A, B {
    @Override
    public T apply() {
         return B.super.apply();
    }
} 
```
---
### d\) Method References
Lambda expression like line -> System.out.println(line); can be expressed as System.out::println. Such an expression is called method reference. The :: operator separates the method name from name of the class or an object. There are three principal cases.
* object::instanceMethod
* Class::staticMethod
* Class::instanceMethod

In first two cases, the method reference is equivalent to a lambda expression that supplies the parameters of the method. E.g.: Math::pow is equivalent to (x, y) -> Math.pow(x, y).

The third case, the first parameter becomes the target of the method. E.g: String::compareToIngoreCase is same as (x, y) -> x.compareToIngoreCase(y).

When there are multiple overloaded methods with the same name, the compiler will try to find from the context which one you mean. For example, there are two versions of the Math.max method, one for integers and one for double values. Which one gets picked depends on the method parameters of the functional interface to which Math::max is converted. Just like lambda expressions, method references don’t live in isolation. They are always turned into instances of functional interfaces.




---
References:

* [whats-new-in-java-8-lambdas](https://www.oreilly.com/learning/whats-new-in-java-8-lambdas)
* [Java 8 SE for the Really Impatient](https://www.amazon.com/Java-SE8-Really-Impatient-Course/dp/0321927761)

