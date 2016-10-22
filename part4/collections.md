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


