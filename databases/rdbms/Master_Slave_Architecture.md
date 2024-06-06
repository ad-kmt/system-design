# Master-Slave Replication in RDBMS

## Introduction
Master-Slave Replication, also known as Single Leader Replication, is a method of database replication where data is copied from a primary database (master) to one or more secondary databases (slaves). This replication method ensures data consistency across multiple nodes while distributing the load between read and write operations.

## What is Master-Slave Replication?
In Master-Slave replication, there are two types of nodes:
- **Master (Leader)**: The primary database that handles all write operations.
- **Slave (Follower)**: One or more secondary databases that maintain copies of the master’s data and primarily handle read operations.

### How Does It Work?
1. **Write Operations**: All write queries are sent to the master node.
2. **Data Replication**: The master node replicates the data changes to all slave nodes.
3. **Read Operations**: Read queries are distributed across slave nodes to balance the load.

![](https://ucarecdn.com/1abbe9bf-f823-468b-b230-408f74aa0aa1/)

## Use Cases
Master-Slave replication is ideal for scenarios where the workload is read-heavy, and there is a need to distribute read requests across multiple nodes to improve performance.

Master-Slave replication is used in relational databases like MySQL, PostgreSQL, and Oracle, as well as in NoSQL databases like MongoDB, Cassandra etc.

Leader-based replication is not restricted to only databases.
Distributed message brokers like Kafka and RabbitMQ also use it to provide highly available queues.


## Synchronous vs. Asynchronous Replication
A critical aspect of Master-Slave replication is the replication mode, which can be either synchronous or asynchronous.

### Synchronous Replication
- **Definition**: The master waits for confirmation from all slaves that they have received the data before it is considered committed.
- **Advantage**:
    - Ensures data consistency, follower is guaranteed to have an up-to-date copy of the data that is consistent with the leader.
    - Ensures availability, If the leader suddenly fails, we can be sure that the data is still available to the follower.
- **Disadvantage**: Can cause delays if any slave is unresponsive (due to a crash, network fault, or any other reason)

![](https://ucarecdn.com/7703fb87-6e75-4c6e-9739-d63e4a2da8e4/)

### Asynchronous Replication
- **Definition**: The master considers the data committed as soon as it has been written locally, without waiting for slaves.
- **Advantage**: Faster write operations.
- **Disadvantage**: Risk of data loss if the master fails before replication is complete.

**NOTE**: Overall, the choice of synchronous or asynchronous replication depends on the trade-offs between consistency and performance. Synchronous replication provides stronger consistency guarantees, but it can also result in longer response times. On another side, asynchronous replication provides faster response times but may compromise consistency.

![](https://ucarecdn.com/ed0f25e6-bddb-463d-9bf7-6b928b1335bc/)

### Semi-Synchronous Replication
- **Definition**: Combines synchronous and asynchronous replication. One slave is synchronous, and others are asynchronous.
- **Advantage**:
    - Balances between consistency and performance.
    - ensures that at least two nodes, the leader and one synchronous follower, have up-to-date copies of the data.

![](https://ucarecdn.com/9aca87e9-3c24-4b0a-9e42-497c4e03ca34/)

## Setting Up New Slaves
To add a new slave node:
1. **Take a Snapshot**: Capture a consistent snapshot of the master’s database.
2. **Copy Snapshot**: Transfer the snapshot to the new slave node.
3. **Apply Logs**: The slave node applies all data changes from the snapshot point to catch up with the master.

## Handling Node Failures
Our goal is to keep the system running despite individual node failures and to minimize the impact of a node outage.

The critical question is: How can we achieve high availability and reliability with leader-based replication?

### Follower Failure
- **Recovery**: The slave node uses its log (of the data changes it has received from the leader) to request missing data changes from the master and catch up.

### Leader Failure
Trickier and requires three critical steps:
- **Steps**:
    1. **Detecting Leader Failure**: Use a timeout mechanism to detect the failure.  A timeout is used to assume that a leader node is dead if it doesn’t respond for a certain period of time, typically less than 30 sec or 1 minute.
    2. **Choosing a new leader**: Choose the most up-to-date slave as the new master. To minimize data loss, the replica with the most up-to-date data changes from the old leader is usually chosen as the new leader
    3. **Reconfiguration**: Redirect client write requests to the new master.

## Advantages and Disadvantages

### Advantages
- **Fault Tolerance**: The system can continue operating despite individual node failures.
- **Load Distribution**: Separates read and write operations to balance the load.

### Disadvantages
- **Complex Failover**: Promoting a new master can be complex and may involve data loss.
- **Consistency Issues**: Asynchronous replication may lead to temporary data inconsistency.

## Critical Challenges
- **Split-Brain Scenario**: Occurs when two nodes believe they are the leader, leading to data conflicts.
- **Timeout Configuration**: Balancing the timeout period to avoid unnecessary failovers without delaying recovery.

## Conclusion
Master-Slave replication provides a robust solution for distributing read-heavy workloads while ensuring data availability and consistency. However, it requires careful consideration of replication modes and failure handling mechanisms.

# Resources
https://www.enjoyalgorithms.com/blog/master-slave-replication-databases/

## Next Topics
### Related Topics
- Multi-Leader Replication
- Leaderless Replication

### Deeper Understanding
- Consensus Problem in Distributed Systems
- Chain Replication
- Automatic vs. Manual Failover Strategies

