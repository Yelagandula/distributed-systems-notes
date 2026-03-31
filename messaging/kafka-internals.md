# Kafka Internals

## Topics and Partitions
- Topic = logical stream of records
- Partition = ordered, immutable sequence of records
- Each partition is a **commit log**

## Producers
- Choose partition via key hash or round-robin
- `acks=all` → leader waits for all ISR replicas before acknowledging
- Idempotent producers: `enable.idempotence=true`

## Consumers
- Consumer group → each partition consumed by exactly one member
- Offset tracking in `__consumer_offsets` topic
- `auto.offset.reset=earliest` vs `latest`

## Replication
- Each partition has 1 leader + N-1 followers
- ISR (In-Sync Replicas): followers caught up within `replica.lag.time.max.ms`
- Leader election from ISR only

## Retention
- Time-based: `retention.ms=604800000` (7 days)
- Size-based: `retention.bytes`
- Compaction: keep only latest value per key
