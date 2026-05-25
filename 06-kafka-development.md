# Kafka Development

## Producer API

The producer API is used to publish messages to a Kafka topic.

The producer API takes configuration parameter such as:

- Topic name
- Key and Value serializers
- Key producer configs (to control throughput)
- Security configurations etc.

### Features:

#### Control throughput

We can control how many (throughput) and how often (latency) a producer sends messages to the cluster using:

- Batch size
- linges ms
- acks

#### Exactly once semantics

Exactly Once Semantics (EOS) is a producer setting that ensures that each message produced to a topic is delivered exactly once, without duplication or loss.

To achieve this, the producer is configured to enable idempotence, meaning it assigns a unique sequence number to each message. If a message is sent more than once due to a failure or retry, Kafka will recognize it and discard the duplicate.

Consumers guarantee that messages are processed exactly once by ensuring that offsets are commited only when a message has been sucesfully consumed.

The combination of producer idempotence and consumer offset management ensures that Kafka provides strong delivery guarantees, making it ideal for use cases where message accuracy is critical.

## Consumer API

The consumer API is used to read and process messages from a Kafka topic.

The consumer API takes configuration parameters such as:

- Topic name
- Key and Value deserializers
- Key consumer configs to control throughput
- Security configuration etc.

## Kafka Streams

Kafka Streams is a powerful library used to build real-time stream processing applications.

Enables developers to process, transform, aggregate, and join data as it flows through topics while ensuring high throughput and low latency.

## Flink

Flink is an open-source stream processing framework for real-time data processing.

Flink can handle real-time (unbounded) and batch bounded data.

Has 3 APIs for processing:

1. Data Stream API - real-time stream proccesing
2. Data Set API - Batch processing
3. FlinkSQL - Write SQL queries to process real-time streams and batch data (data analytics)

## Kafka Connect

Kafka Connect is a toolset and framework for scalable and reliable streaming data integration.

It simplifies streaming data integrations by providing pre-built connectors and a framework for custom connectors.

A Kafka Connect process is made up of:

- Connector instance - defines interactions between Connect and the external system
- Converter - handles the serialization and deserialization of data a long with schemas
- Single Message Transforms (SMTs) - (optional) performs one or more transformations to data passing through
