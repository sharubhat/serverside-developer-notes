# Installing Apache Flink on macOS

### Installation instructions

Could not find a brew formula for installing latest Apache Flink, so going with a manual installation.

1. Download Flink for Hadoop 2. This is required if we want Flink to be able to deal with data on Hadoop.
2. tar xzf flink-*.tgz
3. Copy flink-1.1.2 (the latest available version while making these notes) to /usr/Cellar/apache-flink. This is not necessory, however I like to keep the project along with other brew installed softwares.
4. Create following aliases in ~/.profile. Third one is needed for submitting flink jobs

  ```bash
  alias start-flink='/usr/local/Cellar/apache-flink/1.1.2/bin/start-local.sh'
  alias stop-flink='/usr/local/Cellar/apache-flink/1.1.2/bin/stop-local.sh'
  alias flink='/usr/local/Cellar/apache-flink/1.1.2/bin/flink'

  $ source ~/.profile
  ```

5. Start Flink : start-flink

6. Check the JobManager’s web frontend at [http://localhost:8081](http://localhost:8081) and make sure everything is up and running.


### Installation verification instructions

1. Download test data

  ```
  $ wget -O hamlet.txt http://www.gutenberg.org/cache/epub/1787/pg1787.txt
  ```

2. Test WordCount program in current working directory
```
$ flink run ./examples/streaming/WordCount.jar --input file://`pwd`/hamlet.txt --output file://`pwd`/wordcount-result.txt
```

3. Step 2 should generate wordcount-result.txt file in working directory.


### Getting started with IDE debugging

Refer to [this](http://dataartisans.github.io/flink-training/devEnvSetup.html) article which explains how to create a maven project and how to configure IDE.


### Running flink in cluster mode on a single host

1. Create following aliases in ~/.profile.
```bash
alias start-flink-cluster='sudo ifconfig lo0 alias 127.0.0.2 up;sudo ifconfig lo0 alias 127.0.0.3 up;sudo ifconfig lo0 alias 127.0.0.4 up;/usr/local/Cellar/apache-flink/1.1.2/bin/start-cluster.sh'
alias stop-flink-cluster='/usr/local/Cellar/apache-flink/1.1.2/bin/stop-cluster.sh'
```
start-flink-cluster adds alias ip address for localhost which loopback locally. 

2. Update flink-conf.yaml and set taskmanager.numberOfTaskSlots: 3

3. Add following ip address to conf/slaves
```
127.0.0.2
127.0.0.3
127.0.0.4
```
4. Start and stop cluster using aliases created in step 1.
