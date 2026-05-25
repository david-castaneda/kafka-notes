# Kafka Performance

## Kafka Architect

An Kafka Architect is responsible for designing, implementing, and managing large-scale event streaming systems. They design scalable and reliable Kafka clusters, ensuring high availability, fault tolerance, and performance. It is the responsibility of a Kafka architect to configure brokers, producers, and consumers to handle specific business needs.

- They design stream-processing solutions using Kafka Streams or Flink to handle real-time data transformations
- They ensure clusters are secure. They implement encryption, authentication, and access controls, using technologies like SSL, SASL, and ACLs
- They oversee performance and ensure optimal configuration for throughput, latency, and system efficiency
- They monitor system health using tools like prometheus and grafana
- They lead development teams, collaborate with steakholders, and ensure best practices
- They design disaster recovery plans and implement failover strategies
- They oversee deployment strategies, ensuring seamless integration with CI/CD pipelines and automated testing
- They stay up to data with the latest Kafka features

There are 4 things that help them:

- Throughput and Latency
- Producer/Consumer perf-test
- Scalability
- Availability

### Throughput

Refers to the amount of records sent from producers to a Kafka cluster in a given period, typically measured in records per second or bytes per second.

Using batching and compression reduces network usage, increasing efficiency.

The following strategies can be used to improve throughput:

- Batching messages: Batching allows multiple records to be sent together in one request. This reduces the number of requests sent to the broker, increasing throughput.
- Linged.ms: The linger.ms parameter controls how long the producer will wait before sending a batch of messages. This is by default set to zero, that means, No wait for a batch to be filled.
- Compression: Can help reduce the size of data being sent, which leads to more efficient network utilization.

### Latency

The time it takes for a message to travel from the producer to the Kafka cluster. Lower latency is critical for real-time applications, but it can often come at the expense of throughput.

Reducing linger.ms ensures messages are sent immediately, and synchronous sends guarantee quick message delivery.

**Synchronous vs. Asynchronous Sends**

- By default producers send messages asynchronously. You can configue it to send messages synchronously.
- While synchronous sends can reduce latency, they can also reduce throughput. Aysnchronous sends can increase throughput, but may slighly increase latency.

Kafka allows you to configure the acknolegment level with the acks parameter. The three possible values are:

- acks=0: No acknowlegment, fastest but most risky
- acks=1:Acknowlegment after the leader replica receives the message
- acks=all Acknowlegement after all replicas receive the message.The safest but with high latency

## How to test producer and consumer performance

Kafka comes with producer and consumer benchmarking tools.

- Producer throughput is typically easy to benchmark. Run the application at a steady state to determine how much data the system can pass.
- Consumer tesing is a bit more challenging. The results depend not just on the actual consumption of Kafka events, but what the consumer then does with those events (write to datastore, process in an application). Consumer throughput depends on many factors:
  - Processing time per message
  - Number of messages fetched per poll
  - Message size (maximum or average)

## Scalability

Kafka can scale both horizontally and vertically.

Horizontal scaling:

- You can add more brokers to the cluster to scale out and increase throughput
- Each broker can handle partitions, and these partitions are distributed across the brokers in the cluser, enabling parallel processing
- As the load increases, you can add more brokers to manage the additional data without compromising on performance
- Kafka achieves scalability though partitioning and replication
- Data within a topic is split into partitions, allowing for parallel processing. Partitions can be distributed across different brokers, allowing each broker to handle a portion of the load. Replication ensures data availability and fault tolerance, as copies of partitions are store on different brokers.
- This guarantees that if one broker fails, the data is still available from another broker

## Availability

Kafka is designed for high availability and fault tolerance.

- How does Kafka prevent data loss? By replicating each partition across mutiple brokers
- What happens when a broker fails? Kafka automatically elects a new leader for affected partitions
- Why is Kafka a robust choice for real-time processing? Fault tolerance, automatic rebalancing, and distributed architecture
