# Chord Protocol with Fault Tolerance Enhancements

## Overview

This project implements the **Chord Distributed Hash Table (DHT)** protocol with **robust fault tolerance mechanisms**. It simulates node joins, departures, and failures in a peer-to-peer ring topology, ensuring the system remains consistent, available, and resilient.

The implementation enhances standard Chord with:
- **Successor lists**
- **Failure detection (ping mechanism)**
- **Data replication**
- **Graceful exit and stabilization**

---

## Key Features

- **Efficient Lookup**: O(log N) hop complexity using finger tables
- **Self-Stabilization**: Handles joins and failures using periodic stabilization
-  **Fault Tolerance**: Redundant successors and data replication ensure high availability
-  **Graceful Exit**: Nodes exit without disrupting the ring structure

---

## About Chord

Chord is a decentralized protocol for efficient key-value lookups in a dynamic peer-to-peer network. Nodes are arranged in a logical ring, and data is distributed using consistent hashing.

Each node:
- Has a unique ID in a `2^m` identifier space
- Maintains:
  - A **successor pointer**
  - A **predecessor pointer**
  - A **finger table** for fast routing

---

## Fault Tolerance Mechanisms Implemented

1. **Successor List**
   - Each node maintains a list of `r` successors.
   - Used as backup if the immediate successor fails.

2. **Ping Mechanism**
   - Periodic heartbeats to detect failed neighbors.
   - Removes dead nodes from the ring automatically.

3. **Data Replication**
   - Data is replicated across the `r` successors.
   - Ensures availability even when nodes fail.

4. **Graceful Exit**
   - Transfers keys and updates neighbors before a node leaves.

---

## Ring Management

### Joining the Ring

1. New node contacts any known node.
2. Runs `find_successor(ID)` to find its place.
3. Updates its successor/predecessor.
4. Receives key responsibilities and updates routing tables.

### Stabilization

- Periodic process to:
  - Fix broken successor/predecessor links
  - Update finger tables
  - Handle newly joined or failed nodes

### Leaving the Ring

- Keys are transferred to the node's successor.
- Neighbors are notified to update pointers.
- Finger tables are gradually fixed via stabilization.

---

## Time Complexity Analysis

| Operation                  | Time Complexity  |
|---------------------------|------------------|
| Lookup                    | O(log N)         |
| Successor List Updates    | O(r)             |
| Failure Detection (Ping)  | O(r)             |
| Data Replication          | O(r) per key     |
| Lookup with Fault Tolerance | O(log N + r)   |

*Note: `r` is a small constant (e.g., 3–5).*

---

## Testing & Simulations

The system has been tested for:

- Random node joins and leaves
- Multiple node failures
- Data recovery using replication
- Self-healing via stabilization

---

## Future Improvements

- **Dynamic replication factor** based on node churn and network conditions
- **Advanced failure detection** (e.g., gossip-based heartbeat protocols)
- **Load balancing** for skewed data distribution
- **Security features** such as TLS encryption and node authentication

---


