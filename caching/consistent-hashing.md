# Consistent Hashing

## Problem
With normal `hash(key) % N` — adding/removing a node remaps almost all keys.

## Solution: Hash Ring
- Map both nodes and keys onto a circular ring (0 to 2^32)
- Each key is assigned to the **next clockwise node**
- Adding a node → only keys between new node and predecessor are remapped
- Removing a node → only that node's keys move to successor

## Virtual Nodes
Real systems use **virtual nodes** (vnodes):
- Each physical node owns multiple points on the ring
- Provides better load distribution
- Used in: Cassandra, Amazon DynamoDB, Redis Cluster

## Code sketch
```python
import hashlib, bisect

class ConsistentHash:
    def __init__(self, nodes, replicas=100):
        self.ring = {}
        self.keys = []
        for node in nodes:
            for i in range(replicas):
                h = self._hash(f"{node}:{i}")
                self.ring[h] = node
                self.keys.append(h)
        self.keys.sort()

    def get_node(self, key):
        h = self._hash(key)
        idx = bisect.bisect(self.keys, h) % len(self.keys)
        return self.ring[self.keys[idx]]

    def _hash(self, key):
        return int(hashlib.md5(key.encode()).hexdigest(), 16)
```
