# CAP Theorem

A distributed system can guarantee at most **2 of 3**:
- **C**onsistency — every read gets the most recent write
- **A**vailability — every request gets a response
- **P**artition tolerance — system works despite network partitions

## In practice: partition tolerance is mandatory
Networks fail. So you choose between CP and AP.

## CP Systems (sacrifice availability)
- HBase, MongoDB (strong mode), Zookeeper

## AP Systems (sacrifice consistency)
- Cassandra, DynamoDB, CouchDB

## Real example: Cassandra
Tunable consistency: `ONE`, `QUORUM`, `ALL`
- `ONE` → AP (fast, eventually consistent)
- `ALL` → CP (slow, strongly consistent)
