# Kafka

## How to add options to whitelist -- zookeeper:
```commandline
    environment:
      KAFKA_OPTS: "-Dzookeeper.4lw.commands.whitelist=*"
```
This would allow to run the following code to verify its stats:
```commandline
echo stat | nc localhost 2181
```