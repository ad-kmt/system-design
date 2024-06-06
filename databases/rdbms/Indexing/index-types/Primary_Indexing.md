# Primary Indexing in DBMS

Indexing is a technique used to reduce data access cost or I/O cost.

## What is Primary Indexing?

A Primary Index is an ordered file with records of fixed length containing two fields:
1. The primary key of the data file in an ordered manner.
2. A block pointer that points to the data block where a record containing the key is available.

### Working of Primary Indexing

- The data file is sorted or clustered based on the primary key.
- An index file (also known as the index table) is created alongside the data file.
- The index file contains pairs of primary key values and pointers to the corresponding data records.
- Each entry in the index file corresponds to a block or page in the data file.

[![](https://media.geeksforgeeks.org/wp-content/uploads/20240306162155/Primmary-Index.jpg)](https://www.geeksforgeeks.org/primary-indexing-in-databases/)

### Types of Primary Indexing

1. **Dense Indexing**:
    - Contains an index entry for every search key value in the data file.
    - Ensures efficient data retrieval but requires more storage space.
    - Number of Index Entries = Number of Database Records.

2. **Sparse Indexing**:
    - Has fewer index entries than records.
    - Index entries point to blocks of records rather than individual records.
    - Reduces storage overhead but may require additional disk accesses during retrieval.
    - Number of Index Entries = Number of Blocks.

### Advantages of Primary Indexing

- **Fast Retrieval**: Allows fast retrieval of records based on their primary key values.
- **Reduced Disk I/O**: Reduces the need for full-table scans or sequential lookups, thus reducing disk I/O operations.
- **Organized Data**: Ensures records are stored in a logical order based on the primary key, simplifying range queries and other operations.
- **Efficient Access**: Each block in the data file corresponds to an entry in the primary index. The average number of blocks accessed using the primary index can be estimated as approximately log₂(B + 1), where B represents the number of index blocks.

### Disadvantages of Primary Indexing

- **Additional Space**: Requires additional space to store the index field alongside the actual data records, impacting overall system costs, especially for large datasets.
- **Reorganization Needed**: When records are added or deleted, the data file needs reorganization to maintain the order based on the primary key.
- **Memory Cleanup**: After record deletion, the space used by the deleted record must be released for reuse by other records, which can be complex to manage.

## What's Next?

### Related Topics
- Secondary Indexing
- Clustered and Non-Clustered Indexes
- Multilevel Indexing

### Topics for Deeper Understanding
- Index Maintenance and Optimization
- Performance Implications of Indexes
- Indexing in NoSQL Databases
