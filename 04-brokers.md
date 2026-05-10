# Brokers

A Kafka broker or node is a server that stores data and serves clients. It listens to incoming messages from producers, stores those messages in partitions, and serves them to consumers when requested.

Brokers manage storage, consumer's request, and topic's partitions.

A Kafka cluster can have multiple brokers allowing for horizontal scaling and fault tolerance. Each broker in a cluster is identified by a unique ID. It's common to run multiple brokers in a cluster to maintain data availability and system reliability.

Producers send data to topics which are distributed across partitions. Each partition is replicated across multiple brokers for data redudancy. Consumers read messages from these partitions, Kafka ensures are delivered in the correct order and only ONE time.

Brokers are the backbone if a Kafka cluster ensuring data flow and fault tolerance.
