## Reset consumer group offset

start producer and write some messages
```
docker exec -it kafka_test /bin/bash
/opt/kafka/bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test
```

start consumer
```bash
docker exec -it kafka_test /bin/bash
/opt/kafka/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --consumer-property group.id=readers --consumer-property client.id=client-1 --from-beginning
```

describe consumer group
```
docker exec -it kafka_test /bin/bash
./kafka-consumer-groups.sh --bootstrap-server localhost:9092 --describe --group readers
```

sample output 
```
TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID     HOST            CLIENT-ID
test            0          1154            1154            0                                               client-1
```

*stop consumer*

reset offset
```
docker exec -it kafka_test /bin/bash
/opt/kafka/bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --reset-offsets --to-offset 1 --group readers --topic test --execute
```

