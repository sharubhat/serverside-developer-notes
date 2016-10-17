1. Return type is mandatory for recursive functions. This is because, for non-recursive functions, Scala evaluates the right hand side of the function to find out the return type. This is not always possible in case of recursive functions that do not terminate.

2. There are no premitive types in Scala. Everything is a class. 