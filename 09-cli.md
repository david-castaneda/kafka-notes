# CLI

## kafka-topics

- List all topics

```sh
kafka-topics --list \
--bootstrap-server kafka:9092
```

- Describe a topic

```sh
kafka-topics --describe \
--bootstrap-server kafka:9092 \
--topic vehicle-positions
```

- Create a topic

```sh
kafka-topics --bootstrap-server kafka:9092 \
--create \
--topic vehicle-positions \
--partitions 6 \
--replication-factor 1
```

- Delete a topic

```sh
kafka-topics --delete \
--bootstrap-server kafka:9092 \
--topic vehicle-positions
```

- Add partitions to a topic

```sh
kafka-topics --alter \
--bootstrap-server kafka:9092 \
--topic vehicle-positions \
--partitions 3
```

## kafka-console-consumer

- Consume data from a topic

```sh
kafka-console-consumer \
--bootstrap-server kafka:9092 \
--topic vehicle-positions
```

Additional flags:

- `--group my-consumer-group` - the name of the consumer group
- `--from-beginning` - start from the beginning of the topic offset
- `--property print.key=true` - print the message key

## kafka-console-producer

- Produce data to a topic

```sh
kafka-console-producer --bootstrap-server kafka:9092 --topic sample-topic
```

Additional flags:

- `--property parse.key=true` - parse user prodvided key
- `--property key.separator` - use `,` as key separator (eg. `1,HelloWorld`)

## kafka-consumer-groups

```sh
kafka-consumer-groups \
--bootstrap-server kafka:9092 \
--group vp-consumer \
--describe
```

> Tip: You can use `watch` to observe in real-time how lag changes when using the above command.

## kafka-metadatas-shell

- Interactive shell for exploring Kafka cluster metadata (KRaft)

```sh
kafka-metadata-shell --directory /tmp/kraft-combined-logs/__cluster_metadata-0
```
