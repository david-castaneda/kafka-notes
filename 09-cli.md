# CLI

## kafka-topics

- Print all topics

```sh
kafka-topics --list \
--bootstrap-server kafka:9092
```

- Print information about a topic

```sh
kafka-topics --describe \
--bootstrap-server kafka:9092 \
--topic vehicle-positions
```

- Delete a topic

```sh
kafka-topics --delete \
--bootstrap-server kafka:9092 \
--topic vehicle-positions
```

## kafka-console-consumer

- Consume data from a topic

```sh
kafka-console-consumer \
--bootstrap kafka:9092 \
--topic vehicle-positions
```
