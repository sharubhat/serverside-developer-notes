# DataStream api basics

```java
public class StreamingJob { 
    public static void main(String[] args) throws Exception { 
        // set up the streaming execution environment 
        final StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment(); 
        /** 
        * Here, you can start creating your execution plan for Flink. 
        * 
        * Start with getting some data from the environment, like 
        * env.readTextFile(textPath); 
        * 
        * then, transform the resulting DataStream<String> using operations 
        * like 
        * .filter() 
        * .flatMap() 
        * .join() 
        * .coGroup() 
        * 
        * and many more. 
        * Have a look at the programming guide for the Java API: 
        * 
        * http://flink.apache.org/docs/latest/apis/streaming/index.html 
        * 
        */ 

        // configure event time 
        env.setStreamTimeCharacteristic(TimeCharacteristic.EventTime); 
        DataStream<Tuple2<String, Integer>> counts = env 
                .socketTextStream("localhost", 9999) 
                .flatMap(new Splitter()) 
                .keyBy(0) 
                .timeWindow(Time.minutes(5)) 
                .sum(1); 
        counts.print(); 
        // execute program 
        env.execute("Flink Streaming Java API Skeleton"); 
    } 

    private static class Splitter implements FlatMapFunction<String, Tuple2<String, Integer>> { 
        @Override public void flatMap(String s, Collector<Tuple2<String, Integer>> collector) 
                    throws Exception { 
            // normalize and split the line 
            String[] tokens = s.toLowerCase().split("\\W+"); 
            // emit the pairs 
            for(String token : tokens) { 
                if(token.length() > 0) { 
                    collector.collect(new Tuple2<>(token, 1)); 
                } 
            } 
        } 
    }
}
```

* **Setting up an execution environment**

  * This is the first step where you decide if your environment is going to be a regular environment where you read a file from disk or operate on a fixed dataset or if it's going to be a streaming environment.

    ```java
    final ExecutionEnvironment env = ExecutionEnvironment.getExecutionEnvironment();
    or
    final StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
    ```

  * This is also where you decide whether to go with event time or the time flink receives the data. Following code enables event time.

    ```java
    env.setStreamTimeCharacteristic(TimeCharacteristic.EventTime);
    ```

* **Setting up Data Sources**

  * Create a DataSet or DataStream object from a file or from elements or from socket stream.


* **Setting up Data Types**

  * This is the generic type of DataSet or DataStream.
  * This is usually Tuple or any POJO. There are 25 Tuple classes available in flink's java library starting from Tuple1 to Tuple 25. Basic types such as String, Long, Boolean, Array are also supported.
  * Requirements for a POJO that can be used as a type in Flink are

    * They have publically accessible fields or default getter setters.
    * They have a public empty constructor.

  * Basic types such as String, Long, Integer, Boolean, Arrays are also supported.



* **Define transformations**

  * This is where the data transformation logic is defined. 
  * Transformations could be creating 
    * map which accepts one object and returns one object or 
    * flatMap that takes one object and produces zero, one ore more objects or 
    * keyBy - helps partitioning the data, i.e. all elements with same key are processed by same operator. keyBy takes an integer that is the index of the entry in Tuple.
    * reduce and fold - reduce conceptually applies an operation such as addition to two arguments. Reduce on a list first applies reduce to first two elements, then applies reduce to result of earlier reduce and next element in the array and so on till all elements are exhausted whereas fold does the same thing but fold starts with an initial value that is supplied as argument.
      * When it comes to streams, reduce and fold can only be used with keyed or windowed streams only.
    * filter, timeWindow, sum etc.


* **User functions**

  * User functions such as Splitter in above example can also be defined and applied.


* **Data Sinks**

  * Could be any data sink or console; print in above example.


* **Execution**.

* **Distribution Strategies**

  * The following let developer control how the data should be distributed between the transformations.
    * Forward: Only local communication
       ```java
          streams.forward();
       ```
    * Rebalance: Round-robin partitioning
       ```java
          streams.rebalance();
        ```
    * Partition by hash
       ```java
          streams.partitionByHash(...);
       ```
    * Custom partitioning
       ```java
          streams.partitionCustom(...);
       ```
    * Broadcast: Broadcast to all nodes
       ```java
          streams.broadcast();
       ```

## Tuples

* Easiest and most efficient way to encapsulate data in Flink.
* Java library supports Tuple1 to Tuple25.
* Zero base index
  ```java
  Tuple2<String, String> person = new Tuple<>("Sharath", "Bhat");
  String firstName = person.f0;
  String lastName = person.f1; etc
  ```

## Keyed Streams

* keyBy() partitions Datastreams on keys. keys are extracted from each element
