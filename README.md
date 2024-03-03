# Real Time Sales Analytics with Apache Flink

This repository contains an Apache Flink application for real-time sales analytics built using Docker Compose to orchestrate the necessary infrastructure components, including Apache Flink, Elasticsearch, kafka and Postgres. The application processes financial transaction data from Kafka, performs aggregations, and stores the results in both Postgres and Elasticsearch for further analysis.

## Tools Used
- `Apache Flink`
- `Kafka`
- `ZooKeeper`
- `PostgreSQL`
- `Elasticsearch`
- `Kibana`

## Requirements

- Docker
- Docker Compose

## Architecture

![Alt Text](https://github.com/TVR28/Realtime_Sales_Analytics/blob/main/System%20Architecture.png?raw=true)


## Installation and Setup

1. Clone this repository.
2. Navigate to the repository directory.
3. Run `docker-compose up` to start the required services (Apache Flink, Elasticsearch, Postgres).
4. The Sales Transaction Generator `main.py` helps to generate the sales transactions into Kafka.

## Usage

1. Ensure all Docker containers are up and running.
2. Run the `FlinkCommerce` application provided in this repository to perform real-time analytics on financial transactions.

## Application Details

The `DataStreamJob` class within the `FlinkCommerce` package serves as the main entry point for the Flink application. The application consumes financial transaction data from Kafka, performs various transformations, and stores aggregated results in both Postgres and Elasticsearch.

### Components

- **Apache Flink**
  - Sets up the Flink execution environment.
  - Connects to Kafka as a source for financial transaction data.
  - Processes, transforms, and performs aggregations on transaction data streams.
- **Postgres**
  - Stores transaction data and aggregated results in tables (`transactions`, `sales_per_category`, `sales_per_day`, `sales_per_month`).
- **Elasticsearch**
  - Stores transaction data for further analysis.

### Code Structure

- `DataStreamJob.java`: Contains the Flink application logic, including Kafka source setup, stream processing, transformations, and sinks for Postgres and Elasticsearch.
- `Deserializer`, `Dto`, and `utils` packages: Include necessary classes and utilities for deserialization, data transfer objects, and JSON conversion.

### Configuration

- Kafka settings (bootstrap servers, topic, group ID) are configured within the Kafka source setup.
- Postgres connection details (URL, username, password) are defined in the `jdbcUrl`, `username`, and `password` variables.

### Sink Operations

- The application includes sink operations for Postgres using JDBC to create tables (`transactions`, `sales_per_category`, `sales_per_day`, `sales_per_month`) and perform insert/update operations.
- Additionally, it includes an Elasticsearch sink to index transaction data for further analysis.
