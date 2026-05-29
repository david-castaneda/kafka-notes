# Messages

Messages (or events) is the fundamental unit of data in Kafka.

A message consists of a few compoonents:

- Key: Optional, helps determine which partition a message will go to. Messages with the same key will go to the same partition. Important for maintaining message order and grouping related data together.
- Value: Actual content of the message. It can be any type of data - JSON, Plain Text, Avro, or binary data.
- Timestamp: Either producer provided timestamp or one assinged when the message is received by the cluster.
- Headers: Light-weight metadata.

Message are immutable. Once a message is written to a topic it cannot be modified. Ensures data integrity and consumers to replay data.

Messages are stored in topics. Topics represent a logical way to group Messages. Producers publish messages to topics. Consumers subscribe to topics and consume the Messages.

Messages are stored with a timestamp and are typically kept for a configurable period (retention period). This retention period allows consumers to read messages at their own time and speed. The default retention period is 7 days.
