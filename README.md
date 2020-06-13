# kafka-to-postgres
:balloon: Transfer data from kafka to postgres

## QuickStart

### 1）Setting env

```bash
export
DATABASE_URL="postgres://[PG_USER]:[PG_PASSWORD]@[PG_HOST]:5432/[DB_NAME]?currentSchema=public"
export KAFKA_IP=KAFKA_IP_ADDR
export KAFKA_TOPIC=TOPIC_NAME
export CONSUMER_GROUP=GROUP_NAME
```
:loudspeaker: `CONSUMER_GROUP` no setting will auto generate one.

### 2）Launch

```bash
git clone https://github.com/sincerefly/kafka-to-postgres.git
cd kafka-to-postgres
cargo build && cargo run
```

### 3）Message Rules

Message **mush** be json string, with *tablename* and *data* params
**required**. eg:

```json
{
    "schema": "public",
    "tablename": "users",
    "data": {
        "id": "69080fd6-6240-4738-8c68-c91227722bc9",
        "name": "David",
        "age": 42
    }
}
```

and this tool received message will generate sql then post data to
postgres

```sql
INSERT INTO users (age,id,name) VALUES
(42,'69080fd6-6240-4738-8c68-c91227722bc9','David');
```


