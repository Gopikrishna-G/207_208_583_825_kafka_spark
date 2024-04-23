# 207_208_583_825_kafka_spark

For this project we used Ubuntu 22.04.

This project is about using Apache Spark and Kafka to process streaming data. The data being considered here are Twitter feeds stored in a MySQL Database. This data is continuously stored at random intervals and includes a random number of tweets by Kafka.
The project involves executing multiple workloads, such as Spark SQL queries, to perform actions, transformations, or aggregations on the input data. Additionally, Twitter Data may be retrieved because of a certain SQL query.
The project focuses on four topics: tweets, hashtags, top_tweets, and top_hashtags. There are subscribers, both streaming consumers and batch consumers, who subscribe to the topic on a random basis. Metrics are run on the same data in both streaming mode and batch mode, and the accuracy and performance of these two modes are compared.
The project also includes computation examples like counting tweets within a window and applying aggregation functions on numeric data with each tumbling window. The window size for this project is significant and suitable to the chosen domain problem. For example, one window might include 15-30 minutes of tweets.

## Tools used
Mysql (8.0.36) - To install: 'sudo apt-get install mysql'

Zookeeper (3.4.13-6ubuntu4.1) - To install: 'sudo apt-get install zookeeper'

Apache Kafka (3.7.0) - https://dlcdn.apache.org/kafka/3.7.0/kafka_2.13-3.7.0.tgz

Apache Spark (3.5.1) - https://dlcdn.apache.org/spark/spark-3.5.1/spark-3.5.1.tgz

PySpark (3.5.1) - To Install: 'pip3 install pyspark=="3.5.1"'

## Steps for execution:

1) Open Mysql terminal and load the sql file to the database named "twitterDatabase", change the username and password in the kafka_producer.py file.
2) Run the following commands-
   1) Terminal-1:
   sudo systemctl start zookeeper
   
   sudo systemctl start kafka

   /path-of-kafka-bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic tweets

   /path-of-kafka-bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic hashtags

   /path-of-kafka-bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic top_tweets

   /path-of-kafka-bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic top_hashtags

   /path-of-spark-sbin/start-all.sh

   python3 kafka_producer.py

   2) Terminal-2:
   spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.2.3 spark_consumer-streaming.py

   3) Terminal-3:
   spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.2.3 spark_consumer-batch.py
