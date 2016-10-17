* Return type is mandatory for recursive functions. This is because, for non-recursive functions, Scala evaluates the right hand side of the function to find out the return type. This is not always possible in case of recursive functions that do not terminate.

* There are no premitive types in Scala. Everything is a class. 

* When a variable is declared and initialized, it's type is inferred. However it is advisible to specify the type if the variable is being initialized to '_null_'.

```Scala
var x = null        // x will be of type Null
x = 2               // this will result in error as 2 is of type Int

var y: Int = null    // now the type of y will be Int and not inferred as Null
y = 2                // Success
``` 

* Scala string is same as java.lang.String. However Scala string has over 100 methods that are not available in Java. So refer to Scaladocs before coming up with a complex operation on Strings.

* The ++, -- operators do not exist in Scala. Use += instead: counter += 1;

* An Int is automatically converted to a RichInt when one of it's method is needed. e.g.: 1.to(10) automatically converts 1 to a RichInt type and applys '_to()_' method on it.