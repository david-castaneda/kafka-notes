# Topics

In Kafka a topic is a group/category/feed where messages are published. It acts as a logical channel that organizes and stores data.

Producers can publish messages to a particular topic. Consumers can read messages from a topic.

Each message published to a topic is part of a partition. Partitions support distributed and parallel processing.

Topics are important for organizing and distributing data across different applications.

A single node can create a bottleneck. Topics are split into partitions allowing Kafka to horizontally scale and manage large volumes of data.

Each partition is an ordered, immutable sequence of messages. Kafka ensures that each message is written to the partition in the order they are received.

Paritions allow Kafka to handle parallel processing. When a producer sends messages, they are distributed across different partitions. This means multiple consumers can read messages concurrently from different partitions speeding up processing.

Each partition is stored on a broker or node. Each message within a partition is assigned a unique offset. The offset is a unique identifier for that message.

Offsets help consumers keep track of which messages they have already read.

Partitions make Kafka a fault tolerant system. If one broker fails, other brokers can take over the partitions and continue delivering data ensuring high availability.
