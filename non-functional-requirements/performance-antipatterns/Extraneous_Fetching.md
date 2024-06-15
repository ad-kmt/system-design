# Extraneous Fetching Antipattern

## Introduction
Extraneous Fetching is an antipattern in software design where more data than necessary is retrieved for a business operation.

This often leads to unnecessary I/O overhead and reduced responsiveness. It is crucial to recognize and rectify this antipattern to enhance the efficiency and performance of applications.

## Examples of Extraneous Fetching Antipattern
Extraneous fetching can occur when an application attempts to minimize I/O requests by fetching all the data it might need in one go. This is often an overcompensation for the Chatty I/O antipattern.

For instance, fetching details for every product in a database when only a subset is needed can result in unnecessary data retrieval. Even when browsing an entire catalog, paginating the results is more efficient.

Another common scenario involves poor programming practices where the application fetches complete details only to filter and discard unnecessary data later.

### Example 1: Fetching Complete Details
An application retrieves all product details and then filters them in memory to return a subset of fields.

### Example 2: Client-Side Aggregation
An application retrieves all order records to calculate total sales, which could be done more efficiently by the database.

### Example 3: Inefficient LINQ Queries
LINQ queries using methods that cannot be mapped to SQL (e.g., `AddDays`) result in fetching all rows and filtering them in memory, causing excessive data transfer.

## How to Fix Extraneous Fetching Antipattern
To mitigate this antipattern:
1. **Fetch Only Required Data**: Retrieve only the necessary columns and rows for the operation.
2. **Perform Aggregations in the Database**: Conduct aggregations like sum calculations within the database to reduce data transfer.
3. **Optimize LINQ Queries**: Ensure LINQ queries use the `IQueryable` interface, and avoid methods that cannot be translated to SQL.

### Example Fixes
1. **Fetching Required Fields**: Modify queries to select only the necessary fields.
2. **Database-Side Aggregation**: Perform sum calculations in the database rather than in application memory.
3. **Refactor Queries**: Adjust LINQ queries to remove non-translatable methods, enabling efficient database-side filtering.

## Considerations
- **Horizontal Partitioning**: Improve performance by partitioning data horizontally, reducing contention.
- **Pagination**: Implement pagination for unbounded queries to fetch a limited number of entities at a time.
- **Utilize Database Features**: Leverage built-in database functions for aggregations and other operations.
- **Avoid Unnecessary Fields**: Ensure queries do not fetch more fields than necessary, and use database-side filtering.

# Resources

https://learn.microsoft.com/en-us/azure/architecture/antipatterns/extraneous-fetching/

## Related Topics
- **Chatty I/O Antipattern**: Understand the converse issue of making too many small I/O requests.
- **Monolithic Persistence Antipattern**: Explore related antipatterns involving data persistence.
- **Data Partitioning**: Learn about partitioning strategies to improve data access performance.

## Topics for Deeper Understanding
- **Advanced Query Optimization**: Techniques for optimizing complex database queries.
- **Efficient Data Retrieval Practices**: Best practices for minimizing data retrieval overhead.
- **Performance Tuning**: Strategies for enhancing application and database performance under high load.
