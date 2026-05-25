# Kafka - System Design Notes

Apache Kafka is a distributed event streaming platform used for building real-time data pipelines and streaming applications.

## Architecture:

- [Messages](./00-messages.md)
- [Topics](./01-topics.md)
- [Producers](./02-producers.md)
- [Consumers](./03-consumers.md)
- [Brokers](./04-brokers.md)
- [Cluster](./05-cluster.md)

## Reference Links:

- https://kafka.apache.org
- https://training.confluent.io/learn/courses/1073/confluent-apache-kafka-fundamentals-course-accreditation

Open questions:

- How does connecting to a broker work? Is there a "master broker" that knows which brokers have which topics / partitions?
- Whats the deal with the terms broker or node or server being thrown around? Are they meaninfully different?
