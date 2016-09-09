# Hello world in Java

```
public class HelloWorld {    
    public static void main(String[] args) {
        System.out.println(“Hello”);
    }
}
```

 What does each keyword mean?

* public - Should be visible to JVM

* class - Everything in java is a an object which is an instance of class

* HelloWorld - class name, same as file name if class is public. Only one public class per .java file

* static - static means the method is part of class and not it’s instance. If it’s non-static, then instance needs to be created which is not realistic.

* void - return type 
* main\(\) - program entrance 
* String\[\] - array of strings that can be sent to help with program initialization

Bytecode from javac is not readable

javap -c gives disassembled code

e.g.: javap -classpath . -c HelloWorld

-verbose instead of -c gives more details

### **Execution**

First steps: Load, link, initialize - before executing main method

**Load:**

Load binaries from class\/interface into JVM

**Link: **

Incorporate binary type data into run-time state of JVM.

Three steps:

* Verification: Verify the structure of class\/interface

* Preparation: Allocate memory needed for class\/interface

* Resolution: Resolve symbolic references


**Initialization: **

Assign class variables with proper initial values

![](/assets/F0BA6469-B8EA-4089-A9D1-EA3F247FF605.png)

Loading:

done by Java classloaders. JVM loads three class loaders when it starts up

* Bootstrap class loader: loads core java libraries from \/jre\/lib

* Extensions class loader: loads code in extension directories \/jre\/lib\/ext

* System class loader: loads code found on CLASSPATH


