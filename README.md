# MLOps-apache-kafka
Example project of using Apache Kafka for real time streaming data.

## Objectives
**1. Set up Kafka using Docker Compose:** *Set up Zookeeper and Kafka on Docker*

**2. Manage Kafka topics:** *Create, list, and describe Kafka topics*

**3. Interact with Kafka using Python scripts:** *Write and run Python Producer and Consumer scripts to send and receive messages*

## COMMANDS
Example of how to create a topic:
```bash
   docker exec <container_name> kafka-topics \
     --create \
     --topic <topic_name> (e.g. sample-topic) \ (find this under the ports section of your running container)
     --bootstrap-server localhost:9092 \
     --partitions 1 \
     --replication-factor 1
```
How to list available topics:
```bash
   docker exec <container_name> kafka-topics \
     --list \
     --bootstrap-server localhost:9092
```
How to describe a topic:
```bash
   docker exec admin-kafka-1 kafka-topics \
     --describe \
     --topic sample-topic \
     --bootstrap-server localhost:9092
```
## NOTES
What is a partition in Kafka?
* In Apache Kafka, a partition is a subdivision of a topic that allows Kafka to scale horizontally and support parallel processing of data.
* Each partition is an ordered, immutable log of records.
* Example:
    
    If a topic has 3 partitions:

	    • Messages can be produced to all 3 in parallel.

        • Consumers can subscribe to any or all of the partitions.

	    • 3 consumers in a consumer group can each read from one partition, enabling high-throughput processing.

What is the primary role of Apache Zookeeper in a Kafka distributed system?
* The primary role of Apache ZooKeeper in a Kafka distributed system is to act as a centralized service for maintaining metadata, coordination, and configuration management for the Kafka brokers.

Specifically, ZooKeeper handles:
1.	Leader Election:
ZooKeeper manages which Kafka broker is the controller, responsible for administrative tasks like partition leader elections.

2.	Broker and Topic Metadata Management:
It keeps track of the list of active brokers, topic configurations, and partitions. Kafka clients can discover this metadata via ZooKeeper (prior to Kafka 2.8).

3.	Cluster Membership and Health Monitoring:
ZooKeeper detects broker failures and helps Kafka reassign partition leaders in such cases.

4.	Quorum Management for Consistency:
Ensures that only one broker acts as the leader for a partition at any time, helping maintain consistency.