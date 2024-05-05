# Consistency Models in Distributed Systems

## Introduction

In computer science, a consistency model is a contract between a distributed system and the processes that use it, dictating how operations on shared data (reads and writes) appear across different nodes.

This document explores various consistency models, detailing how they handle the visibility and ordering of data operations, crucial for building reliable distributed applications.

## Definition of Consistency Models

Consistency models define the rules and constraints on the order and visibility of operations in a distributed system, ensuring that all processes have a consistent view of the data.

## Dominant Models of Data Consistency

### Strong Consistency

- **Description**: Operations appear to be executed in a total order, ensuring that every read receives the most recent write.
- **Trade-offs**: Offers the highest level of consistency at the cost of performance and scalability due to synchronization overhead.

### Eventual Consistency

- **Description**: Updates to a data item will eventually be visible to all processes, allowing temporary divergences between replicas.
- **Advantages**: Enhances scalability and performance by reducing the need for immediate synchronization.

### Causal Consistency

- **Description**: Ensures that causally related operations (where one operation precedes another) are seen in the same order by all processes.
- **Suitability**: Useful in scenarios where the application logic requires maintaining causality without the overhead of strong consistency.

### Read-Your-Writes Consistency

- **Description**: Guarantees that a process will always see its own writes, ensuring a consistent personal view.
- **Application**: Critical for user sessions or scenarios where a user must see results of their actions immediately.

### Monotonic Reads/Writes Consistency

- **Description**: Ensures that processes see non-decreasing views of the data over time, preventing regressions in data state.
- **Use Case**: Important for applications that rely on incremental and accumulative data processing.

## Approaches to Classifying Consistency Models

### Issue Method

- **Focus**: Concentrates on the sequence and interaction of operations across different processes.
- **Example Models**: Strong and sequential consistency, where operations are strictly ordered and replicated.

### View Method

- **Focus**: Deals with the system states and views observed by different processes during their operation.
- **Example Models**: Read-your-writes and monotonic reads, emphasizing the visibility and state transitions.

## Consistency in Practice

### Strong Consistency Characteristics

- **Sequential Consistency**: Processes see operations in the same sequential order as they were executed.
- **Linearizability**: Operations appear instantaneous, adhering to a global sequence that respects real-time ordering.

### Weak Consistency Characteristics

- **Eventual Consistency**: Guarantees that all copies of data will eventually converge to the same state, suitable for distributed environments where immediate consistency is not critical.
- **Causal Consistency**: Focuses on preserving the order of causally related updates, providing intuitive consistency for operations that have a cause-effect relationship.

## Examples of Consistency Models in Distributed Systems

### NoSQL Databases

- **DynamoDB**: Offers both "Eventually Consistent Reads" and "Strongly Consistent Reads" to balance between performance and data accuracy.
- **MongoDB**: Provides strong consistency for immediate data visibility after write operations.
- **Cassandra**: Features tunable consistency levels, allowing users to choose between strong and eventual consistency based on their specific needs.

## ACID vs BASE Consistency Models

### ACID Model

- **Components**: Atomicity, Consistency, Isolation, Durability.
- **Focus**: Ensures strong consistency and reliability, suitable for transactional systems where integrity is paramount.

### BASE Model

- **Components**: Basically Available, Soft state, Eventually consistent.
- **Focus**: Prioritizes availability and fault tolerance, ideal for large-scale distributed systems where flexibility is required.

## Conclusion

Understanding and selecting the appropriate consistency model is crucial for designing robust distributed systems. Each model offers different guarantees and trade-offs, affecting system performance, scalability, and reliability. Developers must consider their specific application requirements to choose the most suitable consistency model.

# Resources

https://www.scylladb.com/glossary/consistency-models/