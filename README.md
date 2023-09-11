# cdc-kafka-setup

Docker setup for a local instance of cdc source that publishes updates to kafka

### Setup

Start up containers

```bash
docker-compose up -d
```

Confirm containers are running

```bash
docker-compose ps
```

Create mysql `users` table

```bash
docker exec -i mysql mysql -uroot -proot mydb < create_table.sql
```

Start mysql CDC connector

```bash
docker exec -it debezium /bin/bash
```

```bash
# Exec this inside debezium shell
curl -i -X POST -H "Accept:application/json" -H "Content-Type:application/json" localhost:8083/connectors/ -d @/debezium-config.json
```

Ingest some data into mysql

```bash
docker exec -i mysql mysql -uroot -proot mydb < insert_data.sql
```

Verify that the data is present in mysql

```bash
docker exec -i mysql mysql -uroot -proot mydb < query_data.sql
```

Verify that the data is replicated into a kafka topic:

```bash
docker exec -it kafka kafka-topics --list --bootstrap-server kafka:9092
```
