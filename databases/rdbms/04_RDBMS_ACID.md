# ACID Properties in RDBMS

Relational Database Management Systems (RDBMS) ensure data integrity and transactional reliability through ACID properties. Here is an explanation of each property and a simple mnemonic to help memorize them.

## What is ACID?

ACID stands for Atomicity, Consistency, Isolation, and Durability. These properties are essential for ensuring that database transactions are processed reliably.

### Mnemonic for ACID

- **A** - **Atomicity**: **A**ll or nothing
- **C** - **Consistency**: **C**orrectness is maintained
- **I** - **Isolation**: **I**ndependent transactions
- **D** - **Durability**: **D**ata persists after completion

## Detailed Explanation

### Atomicity

Atomicity ensures that each transaction is treated as a single unit, which is either fully completed or not executed at all. This means if any part of the transaction fails, the entire transaction fails and the database state is left unchanged.

### Consistency

Consistency ensures that every transaction keeps the database in a correct and valid state. This means that after any transaction is completed, the database must not violate any of its defined rules, like data types, unique constraints, or relationship rules. Essentially, the transaction must not leave the database with incorrect or corrupted data.

### Isolation

Isolation ensures that the concurrent execution of transactions leaves the database in the same state that would be obtained if the transactions were executed sequentially. This property prevents transactions from interfering with each other.

### Durability

Durability guarantees that once a transaction has been committed, it will remain so, even in the event of power loss, crashes, or errors. This ensures that the effects of the transaction are permanently recorded in the database.

## Strategies Used by Traditional RDBMS to Implement ACID

Traditional Relational Database Management Systems (RDBMS) employ several key strategies to ensure the ACID properties of transactions. Below, we explore these strategies in more detail:

### Locking Mechanisms

To ensure **Isolation**, RDBMS use various types of locks. Locks prevent multiple transactions from accessing the same data concurrently in a way that would lead to inconsistencies. There are several types of locks:

- **Shared locks** allow multiple transactions to read a database resource but not modify it.
- **Exclusive locks** allow a transaction to modify a database resource and prevent other transactions from accessing it simultaneously.

### Log-based Recovery

To maintain **Atomicity** and **Durability**, RDBMS use transaction logs. Every change to the database is first written to a log before it is applied. This ensures that:

- In case of a failure before a transaction is completed, the RDBMS can roll back to the original state using the log (maintaining atomicity).
- Once a transaction is committed, changes can be recovered from logs even if the system crashes immediately afterwards (ensuring durability).

### Write-Ahead Logging (WAL)

A specific type of logging mechanism, Write-Ahead Logging is crucial for both atomicity and durability. It dictates that all changes to logs must be written before the actual data is written to the database. This strategy ensures that the database can always be brought to a consistent state by replaying or undoing transactions recorded in the logs.

### Concurrency Control Protocols ???

RDBMS implement various protocols to manage concurrent access to data, which is critical for maintaining **Isolation**. Two common protocols are:

- **Two-phase locking (2PL)**: This protocol ensures that all locks are acquired before any locks are released during the transaction. This reduces the risk of deadlocks but can impact performance due to extensive locking.
- **Timestamp ordering**: Transactions are timestamped, and the RDBMS manages access based on these timestamps to ensure a serializable order of transactions.

### Integrity Constraints

To ensure **Consistency**, RDBMS enforce data integrity constraints. These include:

- **Primary key constraints** ensure no duplicate records exist.
- **Foreign key constraints** maintain valid references between tables.
- **Check constraints** verify that data meets specific criteria before being stored.

### Snapshot Isolation

Some RDBMS use snapshot isolation to enhance performance while maintaining consistency and isolation. This involves maintaining a snapshot of the data as it appeared at the start of a transaction, allowing multiple transactions to read from the same snapshot without blocking each other.

These strategies collectively ensure that RDBMS can effectively manage transactions in a reliable and secure manner, adhering to the ACID properties essential for database systems.
