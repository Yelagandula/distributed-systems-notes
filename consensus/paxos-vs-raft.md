# Paxos vs Raft

| Property | Paxos | Raft |
|---|---|---|
| Understandability | Hard | Much easier |
| Leader election | Not specified | Built-in |
| Log replication | Flexible | Strict ordering |
| Membership changes | Manual | Joint consensus |

## When to use Raft
- etcd (Kubernetes backing store)
- CockroachDB
- TiKV

## When to use Paxos variants
- Google Chubby (Multi-Paxos)
- Apache Zookeeper (ZAB — Paxos-inspired)
