# Chord-Based Distributed System with Fault Tolerance

## Overview

This project implements a **Chord-based Distributed Hash Table (DHT)** with added **fault tolerance** mechanisms to ensure reliability and robustness in the presence of node failures. Chord is a distributed system that provides efficient lookups, insertion, and deletion of key-value pairs in a distributed ring topology. The system is designed to handle node failures gracefully, ensuring that the system remains operational even when some nodes become unavailable.

The fault tolerance mechanisms include:
- **Successor List** to maintain multiple successor nodes for better fault resilience.
- **Periodic Health Checks** (ping mechanism) to verify node liveness.
- **Data Replication** across multiple successors to ensure data availability.
- **Graceful Recovery** mechanisms to handle failures and stabilize the ring after node crashes or departures.

## Features

- **Ring-based Architecture**: Each node is assigned an identifier based on a hash of its IP address and port. Nodes are arranged in a logical ring structure where each node has a predecessor and a successor.
  
- **Fault Tolerance**: 
  - **Successor List**: Each node maintains a list of `r` successors to ensure availability if the immediate successor fails.
  - **Failure Detection**: Periodic pings are sent to verify the liveness of nodes, particularly successors and predecessors.
  - **Data Replication**: Data is replicated across multiple successors to avoid data loss in case of node failure.
  
- **Automatic Stabilization**: Nodes automatically stabilize the ring periodically, ensuring that successors and predecessors are updated when necessary.

- **Graceful Node Deletion**: When a node leaves or is deleted, the system ensures that the ring is restructured without any data loss or disruptions. Predecessors and successors are updated accordingly.

## Installation

### Prerequisites

- Python 3.x
- `socket` library for network communication
- `threading` library for multi-threading
- `hashlib` for hashing node IDs
- `sys` for command-line argument parsing

##Usage
Running the System
Creating a New Ring: To create the first node in the ring, run the following command:

bash
python Noddy.py <port_number>

bash
python Noddy.py 5000
This will start the node on port 5000 and it will create the ring as the first node.

Joining the Ring: To add a new node to an existing ring, use the following command:

bash
python Noddy.py <port_number> <existing_node_ip> <existing_node_port>

bash
python Noddy.py 5001 127.0.0.1 5000
This will start a node on port 5001 and connect it to the node running on 127.0.0.1:5000.

Deleting a Node: To delete the current node from the ring, simply type exit in the console. This will trigger the deletion process where the node's successor and predecessor are notified, and the ring is updated.

Checking the Node's State: The system prints useful information during the operation, including:

Node ID
Successor and Predecessor IDs
Finger table
Data store contents
Stabilization status
Available Operations
The system supports the following operations, which can be invoked through RPC calls:

Insert Key: Insert a key-value pair into the system.
Delete Key: Delete a key-value pair.
Search Key: Search for a key in the system.
Notify: Notify neighboring nodes about changes in the successor or predecessor.
Join: Join a new node to the ring.
Leave: Remove a node from the ring.

