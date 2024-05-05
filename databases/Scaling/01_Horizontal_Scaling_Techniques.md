# Horizontal Scaling Techniques

## Introduction

There are a variety of scaling techniques that depend on the database system and what components are used. However, they all use the concept of a **node**, which is an individual machine storing some or all of the data. A group of nodes that work together is called a **cluster**.

### Common Scaling Techniques

1. **Replication**
2. **Horizontal Partitioning (Sharding)**

## Replication

Replication involves creating copies of a database or database node.

### Benefits

#### 1. Fault Tolerance
With replication, each node in a cluster contains a copy of the data. If one of the nodes goes down, the cluster is still able to serve client requests because the other nodes in the cluster can respond to the requests.

#### 2. Read Capacity
With Replication, client requests can be spread across all the nodes in the cluster instead of overwhelming a single node.

This increases the capacity of the system to handle more database read requests.


## Horizontal Partitioning (Sharding)

Partitioning, or sharding, distributes data across multiple nodes, each holding a portion of the data based on a predefined sharding key.

### Functionality

- **Shard**: Each shard (replica set) stores a subset of the data.
- **Sharding Key**: Determines how data is distributed among the shards.

### Benefits

#### 1. Storage Capacity
- Sharding makes it possible to scale the storage capacity of the cluster virtually without limit.
- More storage capacity as we can add more partitions/shards with commodity hardware.

#### 2. Processing Capacity
- With sharding in place, since each node is only responsible for processing the data it stores.
- This increases overall processing capacity for both reads and writes.

### Example

Consider data divided by dates:
- Each shard might handle data for specific date ranges, allowing the database to scale as data volume grows.

### Challenges

- More complex than replication as it requires routing logic to direct queries to the correct node or nodes.
- Overhead from network transfers when assembling data from multiple nodes into a single query result.


