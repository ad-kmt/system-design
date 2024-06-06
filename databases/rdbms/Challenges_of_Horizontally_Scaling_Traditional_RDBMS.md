# Challenges of Horizontally Scaling Traditional RDBMS

Traditional Relational Database Management Systems (RDBMS) are primarily designed for vertical scaling. However, horizontal scaling, which involves adding more machines to a pool of resources, presents significant challenges. This document explores why traditional RDBMS struggle with horizontal scaling.

## Introduction

Horizontal scaling aims to distribute the load across multiple servers, ideally reducing the load on any single server and increasing the capacity of the system as a whole. Despite its advantages in handling more data and users, horizontal scaling is particularly challenging for traditional RDBMS due to their inherent architectural and operational characteristics.

## Key Challenges in Horizontal Scaling of Traditional RDBMS

### 1. Maintenance of ACID Properties

- **Atomicity and Durability**: Ensuring that a transaction is completely processed or rolled back in a distributed environment requires complex coordination between multiple nodes. This increases the risk of partial updates which can violate atomicity.
- **Consistency**: Maintaining a consistent state across all nodes when data is distributed and replicated is extremely challenging. Ensuring that all nodes reflect the same data state at any given time without performance degradation is hard.
- **Isolation**: Providing effective isolation in a distributed setup, where multiple transactions might interact with the same data across different nodes, can lead to high latency due to extensive locking and synchronization.

### 2. Data Distribution and Replication

- **Sharding**: Distributing data across multiple servers (sharding) can lead to uneven data distribution, which complicates query processing and can lead to performance bottlenecks known as hotspots.
- **Replication**: Keeping data synchronized across servers to ensure high availability and fault tolerance increases the complexity of the database management, especially in maintaining the consistency and currency of replicated data.

### 3. Complex Transactions and Join Operations

- **Transactions**: Managing transactions across multiple databases increases complexity due to the need for distributed transactions protocols like Two-Phase Commit, which can significantly slow down transaction processing.
- **Joins**: Performing join operations across tables that are distributed across multiple servers can be highly inefficient, as it often requires significant data movement that increases response times.

### 4. Network Latency

- **Latency Issues**: Communication between distributed database nodes over a network introduces latency. This affects the performance of query processing, especially when the system has to frequently access data located on different nodes.

## Conclusion

While traditional RDBMS are robust and reliable for managing data with complex transactions on a single server or closely connected data centers, they face significant hurdles in horizontally scaling. These challenges stem largely from the difficulties in maintaining ACID compliance, managing data distribution, and handling complex queries across a distributed architecture. Modern database solutions often address these issues by using different architectures designed to facilitate easier scaling, such as NoSQL databases or NewSQL systems that blend RDBMS ACID compliance with NoSQL-like scalability.

