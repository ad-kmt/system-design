# Clustered vs Non-Clustered Indexing in DBMS

## Introduction
In databases, indexes are used to store records efficiently and improve the speed of data retrieval. An index is a unique key made up of one or more columns. There are two main types of indexes:

1. Clustered Index
2. Non-Clustered Index

## What is a Clustered Index?
A clustered index is an index that specifies the physical arrangement of a database's table records. It determines the way data is stored on disk based on the values of one or more columns. When a clustered index is created, the database system arranges the data in the table according to the order specified by the index, meaning the rows in the table are physically sorted on disk.

**B-trees** and their modified version, **B+ trees**, are common data-structures used to store data on disks.

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*pYX3xh0QF69bGlBsj2Aiog.png)

### Characteristics of a Clustered Index
- **Default Indexing Methodology**: Typically, the primary key is automatically created as a clustered index by default.
- **Single clustered Index per Table**: There can only be one clustered index per table since it defines the physical storage order.
- **Stored with Actual Records**: Indexes are stored in the same table as the actual records.
- **Range Queries**: Facilitates the efficient retrieval of ranges of data, range queries and sorting.
- **Key Lookup Functionality**: Directly accesses data pages.

### When to Use a Clustered Index?
- For queries containing filters on specific columns (e.g., WHERE clauses or JOINS) that are queried frequently.
- When data needs to be returned in a specific order (e.g., ORDER BY clause).
- For tables with a large number of read operations.

### Advantages of Clustered Index
- **Efficient for Range Queries**: Best for range or group queries (e.g., max, min, count functions).
- **Direct Access**: Pointers can directly go to a certain place in the disk.
- **Increased Cache Efficiency**: Helps increase cache hits and decrease page transfers.

### Disadvantages of Clustered Index
- **Constant Page Splits**: Causes numerous page splits, affecting data and index pages.
- **Slower Write Operations**: Insert, delete, and update operations take more time and system resources.
- **Leaf Node Storage**: Most records are located in the leaf nodes, requiring more I/O operations.

## What is a Non-Clustered Index?
A non-clustered index is an index that does not specify the physical arrangement of records in the database’s table. Instead, it creates a logical order of the index that is separate from the physical stored order of the rows on disk. Non-clustered indexes are stored separately.

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*PbuOXeNaOR9e-3CbgGVh4w.png)

### Characteristics of a Non-Clustered Index
- **Stored in Key-Value Pairs**: Tables or views can have indexes created for them, stored as key-value pairs.
- **Separate Storage**: Indexes are stored separately from the table data.
- **Pointers to Records**: Contains pointers to the clustered index records or the heap.
- **Supports Secondary Access**: Provides an alternative method for accessing records.

### When to Use a Non-Clustered Index?
- For multiple queries filtering rows using different columns in WHERE clauses or JOINS.
- When data needs to be returned in a specific order frequently.
- For specific columns frequently used in queries (e.g., Cover Non-Clustered Index).
- To create an index on rows meeting specific criteria (e.g., Filter Non-Clustered Index).

### Advantages of Non-Clustered Index
- **Administrative Efficiency**: Avoids the administrative costs of clustered indexes.
- **Multiple Indexes**: Allows the creation of multiple indexes on a table.
- **Efficient Data Access**: Facilitates easy access to information in the table.

### Disadvantages of Non-Clustered Index
- **Logical Order Only**: Does not physically sort data records.
- **Lookup Cost**: Increases the cost of lookups.
- **Dependent on Clustering Key**: Needs updating if the clustering key is altered.

## Differences between Clustered and Non-Clustered Index
| Clustered Index                    | Non-Clustered Index                    |
|------------------------------------|----------------------------------------|
| Physical structure of data         | Logical structure of data              |
| Faster retreival, more efficient             | Slower retreival compared to clustered index     |
| Stored with the main data          | Stored in a different table            |
| Only one per table                 | Several can be created per table       |
| Represents actual data in table    | Represents order of data in index      |

## Conclusion
Indexes are unique keys made up of one or more columns, enhancing the efficiency of data retrieval. Clustered indexes focus on the physical structure of data, while non-clustered indexes focus on the logical structure. Understanding when and how to use these indexes is crucial for optimizing database performance.

## What Next?
### Related Topics
- Composite Indexes
- Unique Indexes
- Index Maintenance

### Topics for Deeper Understanding
- Indexing in NoSQL Databases
- Index Tuning and Optimization
- Advanced Indexing Techniques (e.g., Full-Text Indexing, Spatial Indexing)

# Resources

https://www.scaler.com/topics/clustered-and-non-clustered-index/

https://tarunjain07.medium.com/clustered-vs-nonclustered-index-b5dfc0221abc
