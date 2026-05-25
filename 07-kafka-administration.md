# Kafka Administration

A Kafka admin is a person who manages clusters, ensure high availability, and optimizes the overall performance of the system.

Admins handle things like cluster creation, partitioning, and replication settings. You need to configure Kafka brokers to meet the demands of your organization. Monitoring Kafkas performance is crucial and admin will track metrics such as throughput, latency, and disk usage.

## Configuration

### Static Configuration

Some cluster configurations are static. When changing a configuration, you edit a properties file, then restart the broker. The configuration must be the same accross all brokers in the cluster. Incosistent configurations can lead to unexpected behaviors.

### Dynamic Configuration

Allows having different configurations for different brokers or topics. For example replication factor can be changed dynamically at the time of topic creation. Dynamic configurations overwrite the static startup configuration.

## KRaft

Kafka originally used ZooKeeper to manage its distributed system but, starting with version 2.8, Kafka introduced a new mode called KRaft, which stands for Kafka Raft Consensus Protocol.

- Raft is a well-understood method for determining consensus in a distributed computing environment. KRaft is the Raft algorithm encoded within Kafka.
- Embedding KRaft within Kafka elminates the need for ZooKeeper, an external consensus system
- Eliminating ZooKeer makes it easier to operate and scale a Kafka cluster
- KRaft consensus guarantees the reliability and consistency of Kafka's metadata, including topics, partitions, and configurations
- KRaft efficiently provides management of group consensus and has fast failover recovery

KRaft stores cluster metadata like:

- Cluster membership
- Controller election
- Topic configuration: # of partitions and current broker assignments
- Access Control lists (ACLs)
- Quotas

In KRaft mode, cluster metadata is stored in a single partition Kafka topic called `__cluster_metadata`. KRaft uses this topic to synchronize cluster state changes across controller and broker nodes. The active controller is the leader of this internal metadata topic. Other controllers are replica failovers.

## Monitoring

Monitoring your Kafka cluster helps you identify issues early, reduce downtime, and maintain high availability.

- Throughput monitoring: Track producer/consumer throughput (messages/sec, bytes/sec)
- Broker resource utilization: CPU, memory, disk I/O, and network bandwidth usage
- Replication efficiency: Check replication lag and ISR (in-sync replicas) count to ensure replicas are keeping up with the leader and avoid data inconsistency
- Producer and Consumer tuning: Optimizing batch sizes, compression settings, and fetch sized based on latency and throughput metrics to enhance data flow
- Garbage collection and JVM performance: JVM metrics, GC and heap memory usage, prevent degradation due to memory issues
- Consumer Lag monitoring: Track consumer lag to ensure messages are being processed on time. High lag may indicate slow consumers or issues with processing
- Broker health metrics: Monitor key metrics like CPI, disk space, request latency, and under-replicated partitions
- Topic and partition monitoring: Keep an eye on partition count, leader election changes, and ISR to maintain data consistency and prevent data loss
- Producer peformance metrics: ACKs, retries, and failed message sends
- Error logs and alerts: Message deliver failures, authentication, configuration mismatches

### JMX

A powerful too that helps monitor JVM applications, including Kafka.

Through JMX you can access:

- Performance metrics
- Configuration information
- Runtime statistics: Number of messages processed, consumer lag, disk utilization

Two kinds of JMX metrics:

- gauge - measure of something right now (offline partitions)
- meter - measure of event occurence over time (count, weight, throughput)

You need to enable JMX by specifying the appropriate port in your Kafka broker configuration file. You can access these metrics using compatible tools like JConsole, grafana, Datadog etc.

### Metrics

- Consumer metrics:
  - Number of messages consumed
  - Consumption rates
  - Lag
- Producer metrics:
  - Number of messages produced
  - Send rates
  - Errors
- Broker metrics:
  - CPU usage
  - Memory utilization
  - Disk space
  - Network traffic
- Topic metrics:
  - Partition size
  - Message backlog
  - In-flight bytes

## Security

Security is crucial to prevent unauthorized access and ensure data protection.

- Authentication: Ensures only trusted clients can connect to Kafka brokers. Various mechanisms like SASL and SSL/TLS.
- Authroization: Ensures the authenticated users are allowed to perform specific actions on Kafka topics. Kafka offers ACLs, allowing you to define who can produce, consume, or administrate topics and other resources. Kafka uses Zookeeper for storing these ACLs.
- Encryption: SSL/TLS encryption for commucation between brokers, clients, and producers. This prevents data from being intercepted or tampered with during transmission. You can configure encryption at rest with third-party tools.
