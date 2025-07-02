# bigdata-ingest-play
Core functions that helps to ingest data, as part of the Big Data Ecosystem. Uses Kafka Connect, Apache NiFi, Apache Flume (Hadoop Framework) and Apache Sqoop (Hadoop Framework)

Steps:
1. Big data Ingest (HERE we are)
2. Data Validation, Cleanup and Processing
3. Data Analytics
4. Data Visualization


## Kafka

1. Use Confluent or Conduktor or any cloud solution

https://conduktor.io/get-started

curl -L https://releases.conduktor.io/quick-start -o docker-compose.yml && docker compose up -d --wait && echo "Conduktor started on http://localhost:8080"
https://confluent.cloud/environments/env-gxqv7v/add-cluster?attr=welcome%20page

2. Use a local installation of Kafka using brew intall kafka (v4)

kafka-server-start /usr/local/etc/kafka/server.properties

Installed in port 9092

Install a UI: https://www.datastreamhouse.com/get-started
https://learn.conduktor.io/kafka/kafka-topics-cli-tutorial/

Or docker run -e xeotek_kadeck_free="<your_email_address>" -e xeotek_kadeck_port=8080 -p 8080:8080 -v kadeck_data:/home/.kadeck/ xeotek/kadeck:6.1.2

To see the status of Kafka:
brew services info kafka

### Kafka Commands

Have a playground.config as:

security.protocol=SASL_SSL
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="" password="";
sasl.mechanism=PLAIN

Create topic: 

kafka-topics --bootstrap-server localhost:9092 --topic first_topic --create --partitions 3 --replication-factor 1
kafka-topics --command-config playground.config --bootstrap-server localhost:9092 --topic first_topic --create --partitions 3 --replication-factor 1

List topics:

kafka-topics --bootstrap-server localhost:9092 --list
kafka-topics --bootstrap-server localhost:9092 --topic first_topic --describe
kafka-topics --bootstrap-server localhost:9092 --describe

Delete topics:

kafka-topics --bootstrap-server localhost:9092 --topic first_topic --delete




 
