# Spark Structured Streaming with Kafka using PySpark

This project demonstrates a real-time data processing pipeline using Apache Spark Structured Streaming and Apache Kafka. It includes a Kafka producer to simulate transaction data and a PySpark consumer that processes this data in real-time.

## Architecture

The data pipeline follows this flow:
1.  **Kafka Producer**: Generates random transaction data (ID, card type, amount, datetime) and sends it to a Kafka topic.
2.  **Apache Kafka**: Acts as a distributed message broker to store and stream the transaction events.
3.  **Spark Structured Streaming**: Consumes data from Kafka, parses the JSON payload, performs real-time aggregations (e.g., total amount per card type), and outputs the results.
4.  **Output**: Results are written to both the console and an output Kafka topic.

![Project Architecture](file:///c:/GithubProject/structuredstreamingkafkapyspark/structured_streaming_kafka_pyspark.png)

## Project Structure

- `cloudtv_kafka_producer_demo.py`: Python script to produce sample transaction data to Kafka.
- `pyspark_structured_streaming_kafka_demo.py`: Main Spark application that processes data from Kafka in real-time.
- `cloudtv_kafka_consumer_demo.py`: Simple Kafka consumer for testing.
- `kafka-clients-1.1.0.jar` & `spark-sql-kafka-0-10_2.11-2.4.0.jar`: Required JAR dependencies for Spark-Kafka integration.

## Installation & Setup

### Prerequisites
- Python 3.x
- Apache Spark (v2.4.0 recommended for compatibility with included JARs)
- Apache Kafka
- `kafka-python` library (`pip install kafka-python`)

### Running the Project

1.  **Start Kafka & Create Topics**:
    Ensure your Kafka server is running. Create the `testtopic` (input) and `outputtopic` (output).

2.  **Run the Kafka Producer**:
    ```bash
    python cloudtv_kafka_producer_demo.py
    ```

3.  **Run the Spark Streaming Application**:
    ```bash
    spark-submit --jars kafka-clients-1.1.0.jar,spark-sql-kafka-0-10_2.11-2.4.0.jar pyspark_structured_streaming_kafka_demo.py
    ```

4.  **Verify Output**:
    Monitor the console output or use the Kafka console consumer:
    ```bash
    kafka-console-consumer --bootstrap-server localhost:9092 --topic outputtopic
    ```

## Dependencies

- [Spark SQL Kafka Connector](https://mvnrepository.com/artifact/org.apache.spark/spark-sql-kafka-0-10_2.11/2.4.0)
- [Kafka Clients](https://mvnrepository.com/artifact/org.apache.kafka/kafka-clients/1.1.0)
