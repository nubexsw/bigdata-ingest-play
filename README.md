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

Or docker run -e xeotek_kadeck_free="<your_email_address>" -e xeotek_kadeck_port=8080 -p 8080:8080 -v kadeck_data:/home/.kadeck/ xeotek/kadeck:6.1.2

To see the status of Kafka:
brew services info kafka

### Kafka topics





 
