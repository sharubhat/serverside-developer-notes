# Installing Apache Flink on macOS

### Installation instructions

Could not find a brew formula for installing latest Apache Flink, so going with a manual installation.

1. Download Flink for Hadoop 2. This is required if we want Flink to be able to deal with data on Hadoop.
2. tar xzf flink-*.tgz
3. Copy flink-1.1.2 (the latest available version while making these notes) to /usr/Cellar/apache-flink. This is not necessory, however I like to keep the project along with other brew installed softwares.
4. Check the JobManager’s web frontend at http://localhost:8081 and make sure everything is up and running.

### Installation verification instructions

1. Download test data
```
wget -O hamlet.txt http://www.gutenberg.org/cache/epub/1787/pg1787.txt
```
2. Test WordCount program in current working directory
```
./bin/flink run ./examples/streaming/WordCount.jar --input file://`pwd`/hamlet.txt --output file://`pwd`/wordcount-result.txt
```
3. Step 2 should generate wordcount-result.txt file in working directory.

