spark-structured-kafka-stress-app
============

### Introduction
Small long running stress app.

### Build the app
To build, you need Scala 2.11, git and maven on the box.
Do a git clone of this repo and then run:
```
cd spark-structured-kafka-stress-app
mvn clean package
```
Then, take the generated uber jar from `target/spark-structured-kafka-stress-app-1.0-SNAPSHOT-jar-with-dependencies.jar` to the spark client node (where you are going to launch the query from). Let's assume you place this file in the home directory of this client machine.

### spark-submit
```
spark-submit \
  --num-executors 2 \
  --master yarn \
  --deploy-mode cluster \
  --class com.cloudera.spark.examples.StructuredKafkaStress \
  --conf spark.blacklist.enabled=false \
  spark-structured-kafka-stress-app-1.0-SNAPSHOT-jar-with-dependencies.jar \
  "gsomogyi-cdh6x-1.gce.cloudera.com:9092" \
  PLAINTEXT \
  subscribe \
  topic1 \
  topic2
```
