# Introduction

## APIs

Spark core consists of two APIs - unstructured and structured.

**Unstructured APIs** - RDDS(Resilient Distributed Datasets), Accumulators and Broadcast variables. These are mostly meant for manipulation of raw objects.

**Structured APIs** - DataFrames, DataSets, Spark SQL. These are optimized for working with structured data in the form of tables.

## Spark Applications

Consists of a *driver* process and a set of *executor* processes.

Driver runs on driver node - maintains information about the application, responds to user's program, analyzes, distributes and schedules work across executors.

Executor - runs on executor nodes - executes the code assigned by the driver and reports back the results/status to driver node.

Cluster Manager - This is a relevant piece that controls the physical machines and allocates resources to Spark applications. E.g: Spark standalone cluster manager, YARN, Mesos. Note: multiple spark applications can be running on a cluster at the same time.

### SparkSession

It's a new entry point for using DataSets and DataFrames in Spark 2. It is enssentially a combination of SqlContext, HiveContext and future StreamingContext. SparkSession internally has a SparkContext for actual computation.

SparkSession can be accessed in pyspark as 'spark'.

It represents the connection between Spark cluster and the application.

### RDD and lazy evaluation
Statically typed and immutable objects. So transformation on an RDD returns a new RDD object with new definition of RDD's properties.

Can be created by (1) transforming an existing RDD, (2) from a SparkSession.
To create an RDD,
- use makeRDD, or parallelize on local objects
- read from a storage as textFile, binary file, hadoop file or hadoop context.

5 main RDD properties:
Required,
- partitions() - list of partitions objects that make up the RDD
- iterator(p, parentIters) - a function for computing an iterator of each partition
- dependencies() - a list of dependencies on other RDD
Optional,
- partitioner() - for RDDs of rows of key-value pairs represented as Scala tuples
- preferredLocations(p) - for the HDFS file


### DataFrames

Represents a table of data with rows and columns. The list of columns and their types is called as schema. A dataframe can be distributed across several nodes in the cluster. 

### Partitions
Nothing but chunks of data or a collection of rows that sit on a physical machine. A DataFrame consists of

