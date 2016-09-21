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

