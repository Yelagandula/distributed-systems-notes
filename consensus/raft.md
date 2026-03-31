# Raft Consensus Algorithm

## Overview
Raft is a consensus algorithm designed to be more understandable than Paxos.

## Leader Election
- Nodes start as **followers**
- If no heartbeat received within election timeout → becomes **candidate**
- Candidate requests votes from peers
- First to get majority becomes **leader**
- Leader sends heartbeats to prevent new elections

## Log Replication
1. Client sends command to leader
2. Leader appends to local log
3. Leader replicates to followers in parallel
4. Once majority acknowledge → entry is **committed**
5. Leader applies to state machine, responds to client

## Key Properties
- **Election Safety**: at most one leader per term
- **Log Matching**: if two logs have same index/term, all preceding entries are identical
- **Leader Completeness**: committed entries always present in future leader logs
