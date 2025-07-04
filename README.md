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

Producer:

--compression-codec

To enable message compression, default gzip, possible values 'none', 'gzip', 'snappy', 'lz4', or 'zstd'

--producer-property

To pass in any producer property, such as the acks=all setting

--request-required-acks

An alternative to set the acks setting directly

Producing without keys:

kafka-console-producer --producer.config playground.config --bootstrap-server localhost:9092 --topic first_topic

kafka-console-producer --bootstrap-server localhost:9092 --topic first_topic

If the topic has not been created, and the broker is configured as auto topic creation, if the producer is producing into a non existent topic, then the topic is autocreated.
Cambiar propierdades de server.properties:
auto.create.topics.enable=true
num.partitions=1
default.replication.factor=1
Autocreation is not recommented.

kafka-console-producer --bootstrap-server localhost:9092 --topic noexistedtopic

Producing with acks:

kafka-console-producer --bootstrap-server localhost:9092 --topic first_topic --producer-property acks=all

Producing with keys:

kafka-console-producer --bootstrap-server localhost:9092 --topic first_topic --property parse.key=true --property key.separator=:

Producing with partitioner:

kafka-console-producer --bootstrap-server localhost:9092 --producer-property partitioner.class=org.apache.kafka.clients.producer.RoundRobinPartitioner --topic first_topic

Consumer:

kafka-console-consumer --bootstrap-server localhost:9092 --topic newtopic 

kafka-console-consumer --consumer.config playground.config --bootstrap-server localhost:9092 --topic newtopic 

Consuming from beginnig:

kafka-console-consumer --bootstrap-server localhost:9092 --topic newtopic --from-beginning

kafka-console-consumer --bootstrap-server localhost:9092 --topic newtopic --property print.timestamp=true --property print.key=true --property print.value=true --property print.partition=true --formatter kafka.tools.DefaultMessageFormatter --from-beginning

Consuming int consumer groups:

Have a topic called third_topic with 3 partitions.
Having a producer producing in round robing (1 message to each partition): kafka-console-producer --bootstrap-server localhost:9092 --producer-property partitioner.class=org.apache.kafka.clients.producer.RoundRobinPartitioner --topic third_topic 
Having 1 to 3 consumers in the same group: my-first-application. This makes that each consumer consumes in message from one partition each of them.

kafka-console-consumer --bootstrap-server localhost:9092 --topic third_topic --group my-first-application
kafka-console-consumer --bootstrap-server localhost:9092 --topic third_topic --group my-first-application
kafka-console-consumer --bootstrap-server localhost:9092 --topic third_topic --group my-first-application

Having other consumer in another group: kafka-console-consumer --bootstrap-server localhost:9092 --topic third_topic --group my-second-application --from-beginning

Checking the consumer groups:

List the consumer groups created:
kafka-consumer-groups --command-config playground.config --bootstrap-server localhost:9092 --list
kafka-consumer-groups --bootstrap-server localhost:9092 --list

Describe the consumer group:
kafka-consumer-groups --bootstrap-server localhost:9092 --describe --group my-first-application



Extra Important options you can set (advanced):
--from-beginning

We won't repeat this one enough. To read all historical messages

--formatter

To display messages in a particular format (example below to display keys)

--consumer-property

To pass in any consumer property, such as the allow.auto.create.topics setting

--group

By default a random consumer group ID is chosen, but you can override it with this option. See the demo in the Kafka Consumers in Group CLI Tutorial.

--max-messages

Number of messages to consume before exiting

--partition

If you want to only consume from a specific partition.
