Run docker
```
docker-compose -f kafka-cluster.yml up
```

add some lines into `input.txt` and execute 

```
docker exec -it worker /opt/kafka/bin/kafka-console-consumer.sh --bootstrap-server kafka1:9092 --topic connect_file_text --from-beginning
```

using rest api get connector(s) details
```
docker exec -t worker curl localhost:8083/connectors/
docker exec -t worker curl localhost:8083/connectors/local-file-source-standalone/tasks
docker exec -t worker curl localhost:8083/connectors/local-file-source-standalone/config
```
