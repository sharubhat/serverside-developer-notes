## RDD first() vs take(1)
rdd.first() returns the element at location 0 of the rdd

rdd.take(1) returns an array consisting of only 0th element of the rdd

So if you need to exclude first line of a file(headers) and you are planning to use filter on rdd, then you need to use first()

e.g(python):

header = lines.first()
rows = lines.filter(lambda x: x != header)

## Key/Value RDD
If you are not modifying the keys from transformation on RDDs, make sure to call mapValues() or flatMapValues() instead of map() or flatMap(). It's more efficient. It allows spark to maintain partitions from original RDDs and not shuffle the data around which can be very expensive when you are running the job on a cluster.

Using these functions means they keys are not being modified and are not being exposed.