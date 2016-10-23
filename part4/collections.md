# Collections in Scala

---

* Declaring an array usese type Array.
```Scala
val nums = new Array[Int](10)
```
All entries are initialized to 0 in above example.

* Int array is directly mapped to primitive int[] in Java.

* Creating array with initial values
```Scala
val names = new Array("David", "Ben")
```

* Use paranthesis to access the entries instead of square braces like in Java.
```Scala
E.g.:    nums(0) = 22 or val n = nums(2)
```
* Looping throught the elements or looping using indices.

```Scala
E.g.:
for(element <- nums)

for(i <- 0 until nums.length)

Note: 0 to nums.length includes nums.length whereas 0 until nums.length excludes nums.length
```

* ArrayBuffer class in Scala is equivalent of ArrayList in Java. However it's mutable, take extra care while using it.

Some examples of creation, append or +, appendAll or ++
```Scala
val b = new ArrayBuffer[Int]()
b.append(10)
b += 22
b.append(20, 30)
b.appendAll(ArrayBuffer[Int](11, 12, 14))
b ++= ArrayBuffer[Int](100, 200)

for(i <- b) print(i + ", ")

```

* 