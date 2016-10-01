# DataStream API - Time and Windows

Most of these points are from dataartisans training slides. However I am jotting them here so that I need not go back and forth between slides.

### Windows

* You can not count all records of an infinite stream which means aggregations on DataStream are different from aggregations on DataSet.
* DataStream aggregation makes sense only on windowed streams which are finite subset of streams.

### Types of Windows

* Tumbling Windows - Aligned, fixed length, non-overlapping windows.
* Sliding Windows - Aligned, fixed length but overlapping windows also known as rolling windows.
* Session Windows - Non-aligned\(session window of one user need not align with another user in time axis\), variable length windows with possible session gap for a single user.

### Specifying time window

```java
// (name and salary of employees)
DataStream<Tuple2<String, Double>> employeeSalary = ...

employeeSalary
    // group by employees with same salary
    .keyBy(1)
    // window definition: tumbling window of 5 minutes
    .timeWindow(Time.minutes(5));
```

### Predefined Keyed Windows
* Tumbling time window
```java
    .timeWindow(Time.minutes(1))
```
* Sliding time window
```java
    .timeWindow(Time.minutes(1), Time.seconds(10))
```
* Tumbling count window
```java
    .countWindow(100)
```
* Sliding count window
```java
    .countWindow(100, 10)
```
* Session window
```java
    .window(SessionWindows.withGap(Time.minutes(30)))
```

### Predefined Non-keyed Windows

Windows on non-keyed streams are not processed in parallel.
* Time window - tumbling, 10 seconds

```java
    .timeWindowAll(Time.seconds(10))
```

* Count window - sliding 20/10

```java
    .countWindowAll(20, 100)
```


### Aggregation on Windowed Streams
```java
// (name and salary of employees)
DataStream<Tuple2<String, Double>> employeeSalary = ...

employeeSalary    
    // group by employees with same salary    
    .keyBy(1)    
    // windows that are 1 minute long
    .timeWindow(Time.minutes(1))
    // apply a custom window function on window data
    .apply(new CountBySalary());

public static class CountBySalary implements WindowFunction<
    Tuple2<String, Double>,        // input type
    Tuple3<Double, Long, Double>   // output type
    Tuple,                         // key type
    TimeWindow> {                  // window type

    @Override
    public void apply(
        Tuple key,
        TimeWindow window,
        Iterable<Tuble2<String, Double>> employees,
        Collector<Tuple3<Double, Long, Double>> out) {

        double salary = ((Tuple1<Integer>)key).f0;
        double cnt = 0.0;

        for(Tuple2<String, Double> e : employees) {
            cnt++;
        }
        out.collect(new Tuple3<>(salary, window.getEnd(), cnt));
    }
}

```
