# Bitmap Index in DBMS

## Overview
Database Management Systems (DBMS) use Bitmap Indexing for large tables to efficiently retrieve rows from columns with low cardinality. Cardinality refers to the count of distinct elements in a column. Columns with fewer distinct elements have low cardinality.

A bit in the bitmap represents the smallest unit of data, with values of 0 and 1 mapped to column values. This enables bitmap indexing to retrieve results faster through bitwise logical operations on columns, optimizing performance in large databases.

For example, a column with low cardinality is the "Gender" column with values like Male and Female, which can be represented as 0 and 1.

*Note: To use bitmap indexing, columns need to be arranged sequentially.*

## Need for Bitmap Indexing
Consider a student table with columns Roll_no, Name, Gender, and Result:

| Roll_no | Name        | Gender | Result |
|---------|-------------|--------|--------|
| 01      | Geeta Raj   | F      | Fail   |
| 02      | Deep Singh  | M      | Fail   |
| 03      | Ria Sharma  | F      | Pass   |
| 04      | Ajit Singh  | M      | Fail   |
| 05      | Jitu Bagga  | M      | Pass   |
| 06      | Neha Kapoor | F      | Pass   |

In a college database storing student information, queries like counting the number of male students who passed or failed can be time-consuming if the table contains extensive data. Bitmap Indexing maps columns with low cardinalities like Gender and Result to bits (0 or 1), allowing for quick data retrieval.

## Bitmap Index Structure
Bitmap combines the terms "Bit" and "Map," where a bit represents the smallest data unit (0 or 1) and a map transforms and organizes data according to assigned values.

![](https://scaler.com/topics/images/how-bitmap-indexing-is-done.webp)

## How Bitmap Indexing is Done
Let's see how Bitmap Indexing is applied to the Student table. For example, to query all female students who passed the exam:

```sql
SELECT Name FROM Student WHERE Gender='F' AND Result='Pass';
```

An AND operation is performed between Gender = 'F' and Result = 'Pass'.
All Gender = 'F' values are mapped to 1 (true) and Gender = 'M' to 0 (false).

Similarly, Pass and Fail are mapped in the Result column.
Bitmap indexing logically operates on bits, making it faster to return results.

![](https://scaler.com/topics/images/how-bitmap-indexing-is-done-2.webp)


The result indicates the names to be retrieved: Ria Sharma and Neha Kapoor.

## Advantages
- Faster record retrieval compared to traditional methods as rows are fetched as bits.
- Multiple bitmap indices can be combined to get desired results.
- Efficient and effective for columns with minimal inserts, updates, and deletions.

## Disadvantages
- Not recommended for tables with few records as the response time is already low.
- Time-consuming and difficult to edit as new records need to be entered frequently, making bitmap indexing more suitable for static tables.
- Record deletion disrupts the sequence of records, creating gaps.

## Conclusion
In DBMS, Bitmap Indexing allows quick data retrieval from frequently used columns with low cardinality. It combines bits (0 or 1) and mapping to organize data, reducing query execution time for larger static tables. This technique is specific to Oracle and not supported by MySQL.

## Related Topics
- B-Tree Indexing: A balanced tree data structure used in DBMS for efficient data retrieval.
- Hash Indexing: A technique where a hash function is used to compute the location of a record.
- Clustered Indexing: An index where the order of the rows in the database table is the same as the order of the rows in the index.
- Non-clustered Indexing: An index that maintains a logical order of data rows, distinct from the physical order in the database.

## Deeper Understanding Topics
- Performance Optimization with Bitmap Indexing: Detailed study on how bitmap indexing optimizes query performance.
- Comparison of Indexing Techniques: A comparative analysis of different indexing techniques used in DBMS.
- Index Maintenance: Strategies and best practices for maintaining various types of indexes in DBMS.