# MLOps-apache-kafka

A practical example project demonstrating real-time data streaming using Apache Kafka. This project showcases how to set up and interact with Kafka for handling continuous data streams, which is particularly useful for MLOps scenarios where real-time data processing and model inference are required.

## Overview

This repository contains a complete example of setting up and using Apache Kafka for real-time data streaming. It includes:

- A Docker-based Kafka setup with Zookeeper for distributed coordination
- A Python producer that generates and sends timestamped data points
- A Python consumer that processes incoming messages in real-time
- Example commands for Kafka topic management and monitoring

## Project Structure

```
.
├── docker-compose.yml      # Docker configuration for Kafka and Zookeeper
├── python-kafka-producer.py # Python script to produce messages
├── python-kafka-consumer.py # Python script to consume messages
└── README.md              # This file
```

## Prerequisites

- Docker and Docker Compose
- Python 3.x
- Python packages (install via `pip install -r requirements.txt`):
  - kafka-python
  - docker

## Commands
Example of how to create a topic:
```bash
   docker exec <container_name> kafka-topics \
     --create \
     --topic <topic_name> (e.g. sample-topic) \ (find this under the ports section of your running container)
     --bootstrap-server localhost:9092 \
     --partitions 1 \
     --replication-factor 1
   ```

3. **Run the Producer**
   ```bash
   python python-kafka-producer.py
   ```

4. **Run the Consumer**
   ```bash
   python python-kafka-consumer.py
   ```

## Key Concepts

### Kafka Topics and Partitions
- A topic is a category or feed name to which messages are published
- Topics are divided into partitions for scalability
- Each partition is an ordered, immutable sequence of records
- Multiple consumers can read from different partitions in parallel

### Zookeeper's Role
Zookeeper is essential for Kafka's distributed architecture:
- Manages broker metadata and configuration
- Handles leader election for partitions
- Monitors cluster health
- Maintains consistency across the cluster

## Common Operations

### List Topics
```bash
docker exec <container-name> kafka-topics \
  --list \
  --bootstrap-server localhost:9092
```

### Describe Topic
```bash
   docker exec <container_name> kafka-topics \
     --describe \
     --topic sample-topic \
     --bootstrap-server localhost:9092
```

## Use Cases

This project serves as a foundation for building real-time data pipelines, which can be extended for various use cases such as:
- Real-time model inference
- Stream processing for ML features
- Event-driven architectures
- Data pipeline monitoring
- Real-time analytics

**Topic Creation Issues:**
   - Ensure Zookeeper is running
   - Check broker configuration
   - Verify topic name doesn't contain invalid characters
