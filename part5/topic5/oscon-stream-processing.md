# Notes on getting oscon flink demo example to working

Refer to Stream Processing - [simple walkthrough](http://data-artisans.com/robust-stream-processing-flink-walkthrough/) and [video](https://www.youtube.com/watch?v=fstKKxvY23c).

Following changes are needed for the project to work.
* Comment the following create table statement in InfluxDBSink.java
```java
//influxDB.createDatabase(dataBaseName);
```
This is because there is a bug in influxdb-java client. It tries to create a table with IF NOT EXISTS clause, the support for which has been removed in v1.0 of InfluxDB.
* Create sineWave table yourselves.
  * Start influxdb
    ```
    influxd -config /usr/local/etc/influxdb.conf
    ```
  * Connect to influxdb cli via command 'influx' and run the queries
    ```
    $ influx
    > CREATE DATABASE sineWave 
    > CREATE RETENTION POLICY one_day_only ON sineWave DURATION 1d REPLICATION 1 DEFAULT
    ```
* Modify the following line to use newly created retention policy on the table sineWave
```java
//influxDB.write(dataBaseName, "default", p);
influxDB.write(dataBaseName, "one_day_only", p);
```
* Set up grafana query
![](/assets/grafana-pressure.png)
