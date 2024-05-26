# Scalability for Dummies

## Introduction
Scalability is a critical attribute for any web service aiming to handle a large number of requests efficiently. In this series, we will explore the fundamental concepts and techniques to make a web service massively scalable. We'll cover cloning servers, database scalability, caching strategies, and asynchronous processing.

## What is Scalability?
Scalability refers to the capability of a web service to handle a growing amount of work or its potential to accommodate growth. A scalable web service can efficiently manage increased demand by adding resources such as servers or databases.

## Part 1: Clones

### What are Clones?
Public servers of a scalable web service are hidden behind a load balancer, which evenly distributes load (user requests) across a cluster of application servers. Each server should contain the same codebase and avoid storing user-related data locally.

### Why Use Clones?
Cloning ensures consistent performance and availability by distributing requests across multiple servers. This setup allows for horizontal scaling, enabling the addition of servers to handle increased traffic.

### How to Implement Cloning
1. **Use a Load Balancer:** Distribute user requests evenly across application servers.
2. **Centralize Sessions:** Store sessions in an external database or persistent cache like Redis to ensure consistency across servers.
3. **Deploy Consistently:** Use tools like Capistrano to deploy code changes uniformly across all servers.
4. **Create Server Images:** Create an Amazon Machine Image (AMI) as a "super-clone" for easy deployment of new instances.

### Deployment Considerations
- **Avoid Local Storage:** Do not store user-related data, like sessions or profile pictures, on local disks or memory.
- **Initial Deployment:** After creating the AMI, perform an initial deployment of your latest code to new instances.

### Key Takeaway
By following these steps, your servers can horizontally scale to handle thousands of concurrent requests, ensuring consistent performance.

## Part 2: Database Scalability

### The Problem with Traditional Databases
As your application scales, your database might become a bottleneck. Common issues include slower performance and eventual breakdown due to increased load.

### Path 1: Traditional Scaling
Stick with MySQL and implement master-slave replication. Hire a DBA to manage:
- **Read from Slaves, Write to Master:** Distribute read requests to slave servers and write requests to the master server.
- **Upgrade Hardware:** Continuously add more RAM to the master server.
- **Advanced Techniques:** Employ sharding, denormalization, and SQL tuning.

### Path 2: NoSQL Databases
Switch to a NoSQL database like MongoDB or CouchDB:
- **Denormalize Data:** Avoid joins by denormalizing data and handling relationships in application code.
- **Use NoSQL Features:** Leverage the scalability and flexibility of NoSQL databases.

### Key Takeaway
Choosing the right database strategy early can save time and resources in the long run. Implementing NoSQL databases and avoiding joins can improve scalability significantly.

## Part 3: Caching Strategies

### What is Caching?
A cache is a simple key-value store which involves storing frequently accessed data in a high-speed data storage layer to reduce the time taken to fetch data from the main database. It holds every dataset in RAM and requests are handled as fast as technically possible.

### Why Use Caching?
Caches like Memcached or Redis can handle hundreds of thousands of read operations per second, significantly speeding up data retrieval and improving user experience. Also writes, especially increments, are very, very fast.

### Patterns of Caching

#### Cached Database Queries
This is the most commonly used caching pattern. Whenever you perform a database query, store the result dataset in the cache, using a hashed version of your query as the cache key. The next time you run the query, check the cache first to see if the result is already there.

- **Issues with Cached Database Queries:**
    - **Expiration:** It can be challenging to manage cache expiration. If a piece of data changes, you need to invalidate all cached queries that might include that data.
    - **Complex Queries:** For complex queries, ensuring all relevant cached data is updated or invalidated correctly can be difficult.

#### Cached Objects
This method involves seeing your data as objects, similar to how you structure your code with classes and instances. When your class assembles a dataset from the database, store the entire instance or dataset in the cache.

- **Benefits of Cached Objects:**
    - **Simplified Cache Invalidation:** When an object changes, you can easily remove it from the cache.
    - **Improved Performance:** Reduces the need to repeatedly assemble data from multiple database queries.

- **Example Implementation:**
    - Suppose you have a class called "Product" with a property "data" that contains prices, texts, pictures, and customer reviews.
    - Methods within the "Product" class assemble the "data" array by performing several database requests.
    - After assembling the "data" array, store the complete instance of the "Product" class in the cache.

- **Advantages:**
    - **Easier Cache Management:** You can invalidate the cached object whenever any part of it changes.
    - **Asynchronous Processing:** Enables asynchronous processing by allowing worker servers to assemble objects. The application can consume the latest cached object without frequently accessing the database.

- **Commonly Cached Objects:**
    - User sessions (prefer caching over databases)
    - Fully rendered blog articles
    - Activity streams
    - User-friend relationships


### Key Takeaway
Effective caching can drastically improve the performance and scalability of your web service. Redis is recommended for its persistence and built-in data structures. But if you just need to cache, take Memcached, because it scales like a charm.

## Part 4: Asynchronous Processing

### What is Asynchronous Processing?
Asynchronous processing allows tasks to be handled in the background, improving the responsiveness of your application.

### Why Use Asynchronous Processing?
It prevents users from waiting for long-running tasks, enhancing the overall user experience.

### How to Implement Asynchronous Processing
1. **Pre-computation:** Pre-render dynamic content into static content and store it for fast retrieval.
- **Example:** Pages of a website, are pre-rendered and locally stored as static HTML files on every change. Use a script to pre-render HTML pages and upload them to a CDN like AWS S3 or CloudFront.
2. **Job Queues:** Use job queues like RabbitMQ or Redis lists to manage and process tasks asynchronously.
- **Workflow:**
    1. User initiates a task.
    2. The frontend sends the task to a job queue.
    3. Workers process tasks from the queue.
    4. The frontend notifies the user when the task is complete.

### Benefits of Asynchronous Processing
- **Scalability:** Backends become nearly infinitely scalable.
- **Performance:** Frontends become more responsive, improving user experience.

### Tools for Asynchronous Processing
- **RabbitMQ:** A popular system for implementing async processing.
- **ActiveMQ:** Another robust messaging system.
- **Redis Lists:** Can be used for simple task queues.

### Key Takeaway
Asynchronous processing can make your backend nearly infinitely scalable and your frontend snappy, providing a better user experience.

## What Next?

### Related Topics
- Load Balancing Techniques
- Distributed Systems
- Microservices Architecture

### Deeper Understanding
- Advanced Caching Mechanisms
- Database Sharding Strategies
- Event-Driven Architecture

By understanding and implementing these scalability techniques, you can ensure your web service remains performant and reliable as it grows.

# Resources
https://github.com/donnemartin/system-design-primer?tab=readme-ov-file#step-2-review-the-scalability-article

https://web.archive.org/web/20221030091841/http://www.lecloud.net/tagged/scalability/chrono