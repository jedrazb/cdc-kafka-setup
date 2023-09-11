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

Create mysql table and insert some data, note `cdc-kafka-setup-mysql-1` should match the container name for mysql

```bash
docker exec -i cdc-kafka-setup-mysql-1 mysql -uroot -proot mydb < create_table.sql
docker exec -i cdc-kafka-setup-mysql-1 mysql -uroot -proot mydb < insert_data.sql
```
