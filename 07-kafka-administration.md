# Kafka Administration

## KRaft

Kafka originally used ZooKeeper to manage its distributed system but, starting with version 2.8, Kafka introduced a new mode called KRaft, which stands for Kafka Raft Consensus Protocol.

- Raft is a well-understood method for determining consensus in a distributed computing environment. KRaft is the Raft algorithm encoded within Kafka.
- Embedding KRaft within Kafka elminates the need for ZooKeeper, an external consensus system
- Eliminating ZooKeer makes it easier to operate and scale a Kafka cluster
- KRaft consensus guarantees the reliability and consistency of Kafka's metadata, including topics, partitions, and configurations
- KRaft efficiently provides management of group consensus and has fast failover recovery
