# Database Sharding

## What is Database Sharding?

Database sharding is the process of storing a large database across multiple machines. A single machine, or database server, can store and process only a limited amount of data. Sharding overcomes this limitation by splitting data into smaller chunks, called **shards**, and storing them across several database servers. All database servers usually have the same underlying technologies, and they work together to store and process large volumes of data.

![](https://www.yugabyte.com/wp-content/uploads/2019/06/Data-Sharding-in-a-Distributed-SQL-db-socmed-1.png)

## Why is Database Sharding Important?

As an application grows, the number of users and the amount of data it stores increase over time.

The database becomes a bottleneck if the data volume becomes too large and too many users attempt to use the application simultaneously.

This slows down the application and affects customer experience.

Database sharding enables parallel processing of smaller datasets across shards, improving performance and scalability.

## Benefits of Database Sharding

### Improve Response Time

Data retrieval takes longer on a single large database. The database management system needs to search through many rows to retrieve the correct data. By contrast, data shards have fewer rows than the entire database, reducing retrieval time.

### Avoid Total Service Outage

If the computer hosting the database fails, the application depending on it fails too. Sharding distributes parts of the database into different computers, preventing total service outages. If one shard becomes unavailable, data can be accessed and restored from an alternate shard.

### Scale Efficiently

A growing database consumes more computing resources and eventually reaches storage capacity. Sharding allows adding more computing resources to support scaling without shutting down the application for maintenance.

## How Does Database Sharding Work?

A database stores information in multiple datasets consisting of columns and rows. Sharding splits a single dataset into partitions or shards, each containing unique rows of information stored separately across multiple computers (nodes). All shards run on separate nodes but share the original database’s schema or design.

### Example of Unsharded and Sharded Database

#### Unsharded:

| Customer ID | Name | State |
|-------------|------|-------|
| 1           | John | California |
| 2           | Jane | Washington |
| 3           | Paulo | Arizona |
| 4           | Wang | Georgia |

#### Sharded:
- Computer A:

| Customer ID | Name | State |
|-------------|------|-------|
| 1           | John | California |
| 2           | Jane | Washington |

- Computer B:

| Customer ID | Name | State |
|-------------|------|-------|
| 3           | Paulo | Arizona |
| 4           | Wang | Georgia |

### Key Components of Sharding

- **Shards**: Logical partitions of data stored on physical nodes.
- **Shard Key**: A column used to determine how to partition the dataset.
- **Shared-nothing Architecture**: Each physical shard operates independently and processes data in parallel.

## Methods of Database Sharding

### Range-based Sharding

Splits database rows based on a range of values and assigns a shard key accordingly.

**Example**: Sharding the data according to the first alphabet in the customer's name as follows.

| Name | Shard key |
|----------|----------------|
| Starts with A to I | A |
| Starts with J to S | B |
| Starts with T to Z | C |

#### Pros and Cons
- **Pros**: Easier to implement.
- **Cons**: Can result in uneven data distribution.

### Hashed Sharding

Uses a mathematical hash function to assign shard keys and distribute data evenly. The hash function takes the information from the row and produces a hash value.

#### Pros and Cons
- **Pros**: Ensures even data distribution.
- **Cons**: Difficult to reassign hash values when adding more shards.

### Directory Sharding

Uses a lookup table to match database information to the corresponding physical shard.

#### Pros and Cons
- **Pros**: Flexible and meaningful data representation.
- **Cons**: Fails if the lookup table contains incorrect information.

|  Color | Shard Key  |
| ------------ | ------------ |
| Blue  | A  |
| Red  | B  |
| Yellow  | C  |
| Black  | D  |

### Geo Sharding

Splits and stores database information according to geographical location. If data access patterns are predominantly based on geography, then this works well.

**Example**: a dating service website uses a database to store customer information from various cities as follows.

| Name  | Shard Key  |
| ------------ | ------------ |
| John  | California  |
| Jane  | New york  |
|  Paul | Arizona  |

#### Pros and Cons
- **Pros**: Faster information retrieval based on geographical proximity.
- **Cons**: Can result in uneven data distribution.

## Hotspots and its consequences
When a data overload occurs on specific physical shards although others remain underloaded, it results in database hotspots.

Hotspots **slow down the retrieval process** on the database, defeating the purpose of data sharding. 

## How to Optimize Database Sharding for Even Data Distribution

### Good Shard-key Selection

Choosing an optimal shard key is crucial for balanced data distribution. Here are the factors to consider:

### Cardinality

- **Definition**: Cardinality refers to the number of unique values a shard key can have.
- **Importance**: High cardinality means more unique values, which allows for a greater number of possible shards.
- **Example**: Choosing a shard key with low cardinality, such as a yes/no field, restricts the number of possible shards to two.

### Frequency

- **Definition**: Frequency is the likelihood of specific data values appearing in a shard.
- **Importance**: High-frequency values can lead to data hotspots where certain shards receive a disproportionate amount of data.
- **Example**: If age is chosen as a shard key for a fitness website, most records might cluster around ages 30–45, causing those shards to be overloaded.

### Monotonic Change

- **Definition**: Monotonic change refers to the tendency of the shard key values to increase or decrease in a uniform manner over time.
- **Importance**: Monotonically increasing or decreasing shard keys can cause unbalanced shards.
- **Example**: In a feedback database split into shards based on the number of purchases (0-10, 11-20, 21+), as the business grows, most data will accumulate in the 21+ shard, leading to imbalance.

## Alternatives to Database Sharding

### Vertical Scaling

Increases the computing power of a single machine by adding resources like CPU, RAM, and storage.

#### Comparison
- **Pros**: Less costly.
- **Cons**: Limited scaling potential.

### Replication

Makes exact copies of the database and stores them across different computers.

#### Comparison
- **Pros**: Fault-tolerant.
- **Cons**: Sharding is better for scaling.

### Partitioning

Splits a database table into multiple groups.

Partitioning is classified into two types:
- **Horizontal Partitioning**: splits the database by rows.
- **Vertical Partitioning**: Creates different partitions of database columns.

#### Database sharding vs partitioning

**Similarity**: Database sharding is like horizontal partitioning. Both processes split the database into multiple groups of unique rows.

**Difference:** Partitioning stores all data groups in the same computer, but database sharding spreads them across different computers.

## Challenges of Database Sharding

### Data Hotspots

Uneven data distribution causing some shards to become overloaded.

#### Solution
Use optimal shard keys for even distribution.

### Operational Complexity

- Managing multiple database nodes instead of a single database.
- When retrieving information, developers must query several shards and combine the pieces of information together. These retrieval operations can complicate analytics.

#### Solution
Automate database setup and operations to streamline tasks.

### Infrastructure Costs

Higher costs due to adding more physical shards.

#### Solution
Use virtual infrastructure managed by cloud providers to save money.

### Application Complexity

Most database management systems lack built-in sharding features.

#### Solution
Use purpose-built databases with horizontal scaling support.

## What Next?

### Related Topics

- Data Partitioning
- Database Replication

### Topics for Deeper Understanding

- Advanced Shard Key Selection Techniques
- Performance Tuning for Sharded Databases
- Implementing Sharding in Different Database Technologies
- Case Studies on Successful Sharding Implementations

