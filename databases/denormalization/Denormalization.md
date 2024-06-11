# Data Denormalization

## Introduction

As organizations handle increasing amounts of data, the need for faster data access and processing has become crucial. Data Denormalization is a widely used technique **to enhance database query performance**. This document explores data denormalization, its importance, how it differs from normalization, and various denormalization techniques, along with their pros and cons.

## What is Data Denormalization?

Data denormalization is the process of introducing some redundancy into previously normalized databases to optimize database query performance. It involves adding pre-computed redundancy using various techniques, such as:
- Table splitting
- Adding derived and redundant columns
- Mirrored tables

Explained in coming sections.

### How Data Denormalization Works

#### Understanding Normalized Database

In a normalized database, each piece of information is stored only once, and related data resides in separate tables. Queries are used to combine data from multiple tables for real-world applications. However, as data volume increases or queries become more complex (joining multiple tables), performance of database can degrade and lead to crashes.

**Example Scenario**:
Imagine an e-commerce platform where customer data is stored in one table and order data in another. To display all orders placed by a customer, a join operation between the orders and customer tables is needed. With high volumes of orders and customers, this join can become computationally intensive and slow down the website.

**Solution**: We can introduce data denormalization to improve performance in such circumstances.
- Add a customer name column to the orders table.
- Introduce a separate table merging the data from the two tables.

## Comparing Data Denormalization vs Data Normalization

### Data Normalization

Normalization is the process of removing data redundancy by keeping exactly one copy of each piece of data in tables, maintaining relationships, and eliminating unstructured data.

There are several normal forms: first, second, third normal forms, and Boyce-Codd Normal Form (3.5NF). 

Normalization ensures standardized data across an organization, improves query response time, and reduces data anomalies.

### Data Denormalization

Denormalization combines data from multiple tables into a single table for faster querying. It is useful when joins between tables are costly and there are many read-heavy operations.

### **Key Differences**:
1. **Data Redundancy**:
   - Normalization removes redundancy and maintains non-redundant, standardized data.
   - Denormalization introduces redundancy for performance optimization.

2. **Use Cases**:
   - Normalization is used when joins between tables are less expensive and there are frequent Update, Delete, and Insert operations.
   - Denormalization is used when there are many costly join queries.

## Data Denormalization Techniques

### 1. Introducing a Redundant Column / Pre-joining Tables
Used when expensive join operations and frequently used data from multiple tables can be pre-computed. Frequently used data will be added to one table.

**Example**:
- Customer and Order tables: Add the customer name to the order table to avoid frequent joins.

![](https://www.splunk.com/content/dam/splunk-blogs/images/en_us/2023/03/data-denormalization1.png)

### 2. Table Splitting
Decomposes a table into smaller tables for easier querying and management.

#### Horizontal Table Splitting
Splits table rows into smaller tables with the same columns, useful for region-based or task-based data separation.

**Example**:
- A university's student information table split by departments (e.g., Computer Science, Chemistry).

![](https://www.splunk.com/content/dam/splunk-blogs/images/en_us/2023/03/data-denormalization2.png)

**Use case**: this technique enables faster query performance for department-based queries.

#### Vertical Table Splitting
Splits a table based on columns, applying the primary key to each partition.

**Example**:
- A hospital's 'Patients' table split into 'Patient_details' and 'Patient_medical_history'.

![](https://www.splunk.com/content/dam/splunk-blogs/images/en_us/2023/03/data-denormalization3.png)

**Use Case**: when some table columns are frequently accessed more than others. It will allow getting only the required attributes, eliminating unnecessary data. 

### 3. Adding Derived Columns
Adds columns with pre-computed data to avoid recalculating it on each query.

**Example**:
- Student and Student_Grades tables: Add a total marks column in the Student table.

### 4. Using Mirrored Tables
Creates a full or partial copy of a table optimized for faster query performance.

**Example**:
- Creating a mirrored table with additional indexes and data partitioning for read-heavy workloads.

### 5. Materialized Views
Stores pre-computed query results in a separate table for faster access to frequently used data.

**Example**:
- Using materialized views for 'join' and 'aggregation' queries.

## Pros of Data Denormalization

- **Improves user experience**: Enhanced query performance by reducing the number of joins.
- **Reduces complexity**: Simplifies queries and reduces bugs, keeps the data model simple.
- **Enhances scalability**: Reduces the number of database transactions.
- **Generates reports faster**: Optimizes databases for report generation. 
	- Generating such reports can involve data aggregation by searching the whole data set. Data normalization techniques like mirrored tables allow organizations to optimize the databases specifically for daily report generation without affecting the performance of master tables.

## Cons of Data Denormalization

- **Increased data redundancy**: Leads to storage overhead.
- **Data inconsistencies**: Potential issues with maintaining synchronized data sets.
- **Additional storage costs**: Techniques like table splitting and mirrored tables require more storage.
- **Complexity in maintenance**: Increased complexity of the data schema.
- **Costly Inserts and Updates**: Due to redundancy and complexity.

## Conclusion

Data normalization removes redundant data, ensuring a clean and standardized dataset. In contrast, denormalization introduces redundancy to improve read performance at the expense of write performance. While denormalization offers benefits like enhanced query performance and scalability, it also introduces challenges such as increased redundancy and maintenance complexity.

## Next Topics

### Related Topics
- **Database Normalization**: Understanding normal forms and their importance.
- **Data Warehousing**: Differences between databases and data warehouses.

### Deeper Understanding
- **Advanced Denormalization Techniques**: Exploring more complex denormalization strategies.
- **Performance Tuning**: Techniques for optimizing database performance.
- **Data Consistency and Integrity**: Ensuring data reliability in denormalized databases.
