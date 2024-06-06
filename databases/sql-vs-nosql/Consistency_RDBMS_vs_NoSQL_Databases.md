# Consistency in RDBMS vs NoSQL Databases

## Consistency in Traditional RDBMS
In traditional RDBMS, consistency is strictly enforced, meaning that every transaction will bring the database from one valid state to another valid state. This ensures that all database rules and constraints (like primary keys, foreign keys, and custom constraints) are maintained after each transaction. Consistency in RDBMS is typically managed through locking mechanisms that prevent data from being accessed or changed by simultaneous transactions that could lead to conflicts or inconsistencies.

## MongoDB and Consistency

**Eventual Consistency**: Prior to MongoDB 4.0, MongoDB primarily offered eventual consistency, especially in replica sets. This means that when data is written, the changes are immediately visible on the primary node but might take some time to propagate to the secondary nodes. The data across nodes becomes consistent eventually, but not necessarily immediately after the write operation. This approach enhances performance and availability at the cost of immediate consistency.

**Strong Consistency at the Document Level:** Starting with version 4.0, MongoDB introduced multi-document transactions, which support strong consistency at the document level within the same replica set. This means that all operations on a document are immediately visible and consistent on the primary node, and any read operation will reflect the most recent write operation.

**Tunable Consistency for Distributed Setups**: MongoDB allows for tunable consistency models, especially when dealing with replica sets and sharded clusters. For example, when reading data, clients can specify read preferences such as reading from the primary node (strong consistency), secondary nodes (eventual consistency), or a combination of nodes depending on the desired consistency level and latency considerations.

## Cassandra and Consistency

**Eventual Consistency**: Cassandra is designed with eventual consistency as a default to maximize availability and partition tolerance (as per the CAP theorem). In Cassandra, write operations are confirmed as soon as the data is written to the in-memory structure and the commit log, not necessarily waiting for it to be recorded on all replica nodes. Over time, the data across different nodes is synchronized, ensuring eventual consistency.

**Strong Consistency:** Cassandra offers the concept of tunable consistency, which allows the application to choose the level of consistency it needs for each read or write operation. For example, you can choose 'QUORUM' for both reads and writes, which means that a majority of the nodes hosting the data must agree on the read or write operation for it to be considered successful. This can ensure strong consistency, but at the cost of higher latency and reduced availability.

**Tunable Consistency:** The tunable consistency in Cassandra is highly flexible and can be adjusted per operation based on the application requirements. For instance, using 'ONE' or 'ANY' for writes ensures fast operations with less durability, while 'ALL' ensures that all replicas must acknowledge the write before it is considered successful, providing very strong consistency but at the expense of latency and potential downtime in case of node failures.

## Comparison Summary

- RDBMS enforce strong consistency by default, using transaction locks and synchronous writes across the system, which can limit scalability and performance in distributed environments.
- MongoDB provides a mix of eventual and strong consistency and has introduced tunable consistency mechanisms in recent versions to better support distributed transactions.
- Cassandra optimizes for high availability and scalability by using eventual consistency by default but allows applications to choose higher levels of consistency for critical operations, balancing the needs between consistency, availability, and performance.

Understanding these different approaches to consistency helps in selecting the right database system based on specific application needs, especially when dealing with large-scale, distributed environments.