# Document Databases

## What is a Document Database?

A document database (also known as a document-oriented database or a document store) is a database that stores information in documents. These databases offer a variety of advantages, including:

- **Intuitive data model:** Fast and easy for developers to work with.
- **Flexible schema:** Allows for the data model to evolve as application needs change.
- **Horizontal scalability:** Ability to scale out.

Due to these advantages, document databases are general-purpose databases that can be used in various use cases and industries. They are considered to be non-relational (or NoSQL) databases, using flexible documents instead of fixed rows and columns. Document databases are the most popular alternative to tabular, relational databases.

![](https://webimages.mongodb.com/_com_assets/cms/kq6uev0p1jnpq1ob3-snippet_light.svg?auto=format%2Ccompress&ch=DPR)

## Key Questions

- What are documents?
- What are the key features of document databases?
- What makes document databases different from relational databases?
- How much easier are documents to work with than tables?
- What are the relationships between document databases and other databases?
- Why not just use JSON in a relational database?
- What are the strengths and weaknesses of document databases?
- What are the use cases for document databases?

## What are Documents?

A document is a record in a document database, typically storing information about one object and its related metadata. Documents store data in field-value pairs, which can include a variety of types and structures such as strings, numbers, dates, arrays, or objects. They can be stored in formats like JSON, BSON, and XML.

### Example of a JSON Document

```json
{
  "_id": 1,
  "first_name": "Tom",
  "email": "tom@example.com",
  "cell": "765-555-5555",
  "likes": ["fashion", "spas", "shopping"],
  "businesses": [
    {
      "name": "Entertainment 1080",
      "partner": "Jean",
      "status": "Bankrupt",
      "date_founded": {"$date": "2012-05-19T04:00:00Z"}
    },
    {
      "name": "Swag for Tweens",
      "date_founded": {"$date": "2012-11-01T04:00:00Z"}
    }
  ]
}
```

## Collections
A collection is a group of documents. Collections typically store documents with similar contents. Document databases have a flexible schema, meaning not all documents in a collection need to have the same fields. Some document databases provide schema validation to optionally lock down the schema.

### Example Collection
The document with information about Tom could be stored in a collection named users. More documents could be added to the users collection, such as a document storing information about Donna:


```json
{
  "_id": 2,
  "first_name": "Donna",
  "email": "donna@example.com",
  "spouse": "Joe",
  "likes": ["spas", "shopping", "live tweeting"],
  "businesses": [
    {
      "name": "Castle Realty",
      "status": "Thriving",
      "date_founded": {"$date": "2013-11-21T04:00:00Z"}
    }
  ]
}
```
## CRUD Operations
Document databases typically have an API or query language that allows developers to execute CRUD (create, read, update, delete) operations:

- **Create**: Documents can be created in the database with a unique identifier.
- **Read**: Documents can be read from the database using their unique identifiers or field values. Indexes can be added to increase read performance.
- **Update**: Existing documents can be updated, either in whole or in part.
- **Delete**: Documents can be deleted from the database.

## Key Features of Document Databases
- **Document model**: Data is stored in documents, mapping to objects in most popular programming languages.
- **Flexible schema**: Not all documents in a collection need to have the same fields. Schema validation can be optionally enforced.
- **Distributed and resilient**: Allows for horizontal scaling and data distribution, providing resiliency through replication.
- **Querying through an API or query language**: Allows developers to execute CRUD operations and query for documents based on unique identifiers or field values.

## Differences Between Document Databases and Relational Databases
- **Intuitiveness of the data model**: Documents map to objects in code, eliminating the need for decomposing data across tables or using an ORM layer.
- **Ubiquity of JSON documents**: JSON is an established standard for data interchange, allowing for rich objects, key-value pairs, tables, geospatial and time-series data, or nodes and edges of a graph.
- **Flexibility of the schema**: A document’s schema is dynamic and self-describing, allowing for modifications without disruptive schema migrations.

## Ease of Working with Documents vs. Tables
Developers commonly find working with documents more intuitive than working with tables. Documents map directly to data structures in popular programming languages, eliminating the need for splitting related data across multiple tables or using an ORM.

## Example Comparison

#### Document Database (JSON):

```json
{
  "_id": 1,
  "first_name": "Tom",
  "email": "tom@example.com",
  "cell": "765-555-5555",
  "likes": ["fashion", "spas", "shopping"],
  "businesses": [
    {
      "name": "Entertainment 1080",
      "partner": "Jean",
      "status": "Bankrupt",
      "date_founded": {"$date": "2012-05-19T04:00:00Z"}
    },
    {
      "name": "Swag for Tweens",
      "date_founded": {"$date": "2012-11-01T04:00:00Z"}
    }
  ]
}
```
All of the information about Tom is stored in a single document.

#### Relational Database (Tables):

**Users Table:**

| ID | first_name  |  email | cell  |
| ------------ | ------------ | ------------ | ------------ |
| 1  |  Tom |  tom@example.com | 765-555-5555  |

A user can like many things (meaning there is a one-to-many relationship between a user and likes), so we will create a new table named "Likes" to store a user’s likes. The Likes table will have a foreign key that references the ID column in the Users table.

**Likes Table:**

| ID | user_id | like |
|-------|------|------|
|10|1|fashion|
|11|1|spas|
|12|1|shopping|

Similarly, a user can run many businesses, so we will create a new table named "Businesses" to store business information. The Businesses table will have a foreign key that references the ID column in the Users table.

**Businesses Table:**

|ID|user_id|name|partner|status|date_founded|
|---|---|---|---|---|---|
|20|1|Entertainment 1080|Jean|Bankrupt|2011-05-19|
|21|1|Swag for Tweens|NULL|NULL|2012-11-01|

In this simple example, we saw that data about a user could be stored in a single document in a document database or three tables in a relational database. When a developer wants to retrieve or update information about a user in the document database, they can write one query with zero joins. Interacting with the database is straightforward, and modeling the data in the database is intuitive.


## Relationships Between Document Databases and Other Databases

The document model is a superset of other data models, including key-value pairs, relational, objects, graph, and geospatial. This rich data modeling capability makes document databases versatile and suitable for a variety of use cases.

- **Key-value** pairs can be modeled with fields and values in a document. Any field in a document can be indexed, providing developers with additional flexibility in how to query the data.
- **Relational data** can be modeled differently (and some would argue more intuitively) by keeping related data together in a single document using embedded documents and arrays. Related data can also be stored in separate documents, and database references can be used to connect the related data.
- Documents map to **objects** in most popular programming languages.
- **Graph** nodes and/or edges can be modeled as documents. Edges can also be modeled through database references. Graph queries can be run using operations like $graphLookup.
- **Geospatial** data can be modeled as arrays in documents.

### Why Not Use JSON in a Relational Database?

With document databases empowering developers to build faster, most relational databases have added support for JSON. However, simply adding a JSON data type does not bring the benefits of a native document database. Why? Because the relational approach detracts from developer productivity, rather than improve it. These are some of the things developers have to deal with.

**Proprietary Extensions**
Working with documents means using custom, vendor-specific SQL functions which will not be familiar to most developers, and which don’t work with your favorite SQL tools. Add low-level JDBC/ODBC drivers and ORMs and you face complex development processes resulting in low productivity.


**Primitive Data Handling**
Presenting JSON data as simple strings and numbers rather than the rich data types supported by native document databases such as MongoDB makes computing, comparing, and sorting data complex and error prone.


**Poor Data Quality & Rigid Tables**
Relational databases offer little to validate the schema of documents, so you have no way to apply quality controls against your JSON data. And you still need to define a schema for your regular tabular data, with all the overhead that comes when you need to alter your tables as your application’s features evolve.


**Low Performance**
Most relational databases do not maintain statistics on JSON data, preventing the query planner from optimizing queries against documents, and you from tuning your queries.


**No native scale-out**
Traditional relational databases offer no way for you to partition (“shard”) the database across multiple instances to scale as workloads grow. Instead you have to implement sharding yourself in the application layer, or rely on expensive scale-up systems.

## Strengths and Weaknesses of Document Databases

#### Strengths

- **Ubiquitous and intuitive document model** enabling rapid software development.
- **Flexible schema** allowing data model changes as application requirements evolve.
- **Rich APIs and query languages** for easy interaction with data.
- **Distributed and resilient nature** allowing horizontal scaling and global data distribution.

#### Weaknesses
- Some document databases do not support multi-document ACID transactions. However, many applications do not require them. Databases like MongoDB support multi-document ACID transactions.

**Note** that some document databases like MongoDB support *multi-document ACID transactions.*

##  Use Cases for Document Databases

Document databases serve a variety of use cases for both transactional and analytical applications, including:

- Single view or data hub
- Customer data management and personalization
- Internet of Things (IoT) and time-series data
- Product catalogs and content management
- Payment processing
- Mobile apps
- Mainframe offload
- Operational analytics
- Real-time analytics

## Summary

Document databases utilize an intuitive and flexible document data model for storing data, making them general-purpose databases suitable for a variety of use cases across industries. They offer significant advantages in terms of ease of development, flexibility, and scalability.

# Resources

https://www.mongodb.com/resources/basics/databases/document-databases

## What's Next?

### Related Topics

- NoSQL Databases
- MongoDB
- JSON vs BSON

### Topics for Deeper Understanding

- ACID Transactions in Document Databases
- Advanced Querying in Document Databases
- Scaling Strategies for Document Databases
- Security in Document Databases

# Resources

https://www.mongodb.com/resources/basics/databases/document-databases