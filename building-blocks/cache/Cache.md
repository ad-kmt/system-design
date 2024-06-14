# Introduction to Caching and Caching Strategies

## What is Caching?
Caching is the process of storing frequently accessed data in a temporary high speed storage called a cache to improve the speed of data access.

## What is a Cache?
A cache is a **high-speed storage** that stores a small proportion of critical data so that requests for that data can be served faster.

## How Caching Works
When a user requests data, the system first checks the cache:
- **Cache Hit:** If the data is found in the cache, it is returned directly.
- **Cache Miss:** If the data is not found in the cache, it is retrieved from the original database, stored in the cache, and then returned.

**Note**: We always try to optimize cache for high cache hits and low cache miss.

![](https://cdn-images-1.medium.com/max/1080/1*KNlUFMg72Ziy4QbbPpOwcw.png)
## Real-Life Examples of Caching
- **Web Browsers (Client side caching):** Store frequently accessed HTML, CSS, JavaScript, and images.
- **Content Delivery Networks (CDNs):** Store static files like images and videos closer to the user.
- **DNS Caching:** Stores the IP address of a domain name for faster retrieval.
- **Web server caching**: Reverse proxies can serve static and dynamic content directly. Web servers can also cache requests, returning responses without having to contact application servers.
- **Database Caching**: database usually includes some level of caching in a default configuration, optimized for a generic use case. Tweaking these settings for specific usage patterns can further boost performance.
- **Application Caching**: In-memory caches such as Memcached and Redis are key-value stores between your application and your data storage. Since the data is held in RAM, it is much faster than typical databases where data is stored on disk. RAM is more limited than disk, so cache invalidation algorithms such as least recently used (LRU) can help invalidate 'cold' entries and keep 'hot' data in RAM.

## Levels of Caching

There are multiple levels you can cache that fall into two general categories: database queries and objects:

- Row level
- Query-level
- Fully-formed serializable objects
- Fully-rendered HTML

### Caching at the database query level
Whenever you query the database, hash the query as a key and store the result to the cache. This approach suffers from expiration issues:

- Hard to delete a cached result with complex queries
- If one piece of data changes such as a table cell, you need to delete all cached queries that might include the changed cell

### Caching at the object level
See your data as an object, similar to what you do with your application code. Have your application assemble the dataset from the database into a class instance or a data structure(s):

- Remove the object from cache if its underlying data has changed
- Allows for asynchronous processing: workers assemble objects by consuming the latest cached object

## Suggestions of what to cache:

- User sessions
- Fully rendered web pages
- Activity streams
- User graph data


## Types of Caching Strategies

When data in the database is constantly being updated, it is important to ensure that the cache is also updated to reflect these changes.
Otherwise, the application will serve outdated or stale data. So, we use cache invalidation techniques or caching strategies to maintain the cache consistency.

## Reads

### Cache-aside Strategy
The application code manages the cache and database independently:
- On a cache miss, data is retrieved from the database and stored in the cache.
- On a cache hit, data is served directly from the cache.

### Read-through Strategy
The cache sits between the application code and the database:
- On a cache miss, data is retrieved from the database, stored in the cache, and returned to the application.

**Use case**: Read Heavy System

#### Read through vs Cache aside
In cache-aside, application code is responsible for retrieving
data from the database and storing it in the cache. In read-through, this is supported by the cache provider.

So read-through strategy simplifies the application code by abstracting away the complexity of cache management.

## Writes

### Write-through Strategy
Writes are first made to the cache and then to the database:
- Ensures consistency between the cache and database.
- Trade off: Increases write latency.

**Use case**: Read heavy applications, with infrequent writes

### Write-around Strategy
Writes bypass the cache and go directly to the database:
- Reduces write operations on the cache.
- Data in the cache may not be up-to-date.

**Use case**: Write heavy applications, infrequent reads.

### Write-back Strategy
Writes are temporarily stored in the cache and then asynchronously written to the database:
- Improves write performance. Lower write latency and higher write throughput.
- Tradeoff: Carries the risk of data loss if the cache layer fails.

**Use case**: Write heavy applications.

## Cache Eviction Policies
When the cache is full, some data needs to be removed to make room for new data. Common policies include:
- **Least Recently Used (LRU):** Removes the least recently used data.
- **Least Frequently Used (LFU):** Removes the least frequently used data.
- **Most Recently Used (MRU):** Removes the most recently used data.
- **Random Replacement (RR):** Randomly selects and removes data.
- **First In First Out (FIFO):** Removes the oldest data first.

## Different Types of Caching Used in System Design
### Browser Caching (Client side caching)
Stores resources like images, HTML, and JavaScript files in the web browser for faster retrieval on subsequent visits.

### Web Server Caching
Stores resources on the server side to reduce the load on the server.

Implementations:
- **Reverse Proxy Cache:** Acts as an intermediary between the browser and the web server.
- **Key-Value store/db:** Caches application data accessed by the application code. (Memcache or Redis)

**Note**:  Unlike reverse proxies, which cache HTTP responses for specific requests, key-value databases can cache any user-specific data or frequently accessed data based on need.

### Content Delivery Network (CDN)
Improves delivery speed of static content by storing it in proxy servers located around the world.

### Distributed Caching
Uses multiple caching servers spread across a network to scale beyond the memory limits (cache size) of a single machine.

**Data distribution**: each caching server maintains a portion of the cached data, and requests for data are directed to the appropriate server based on a hashing algorithm or some distribution strategy.

**Benefits**:
- faster response times
- scalability
- increased availability
- better fault tolerance.

**Use case**: large-scale applications

## Advantages of Caching
- **Faster Access:** Reduces the need to retrieve data from slower data sources.
- **Increased Throughput:** Provides much higher request rates compared to the main database.
- **Scalability:** Improves scalability by offloading backend databases.
- **Cost Reduction:** Reduces overall system cost by offloading backend databases.
- **Offline Access:** Allows access to data even when the network connection is unreliable or offline.

## Disadvantages and Limitations of Caching
- **Data Inconsistency:** Cached data can become outdated.
- **Cache Misses:** Introduce latency.
- **Initial Cache Warm-up:** Can cause temporary performance degradation.
- **Limited Write Performance:** Most caching strategies do not improve write performance.

## Conclusion
Caching is a useful technique for improving performance, reducing cost, and increasing scalability by storing frequently accessed data in fast storage called cache.

# Resources
https://www.enjoyalgorithms.com/blog/caching-system-design-concept/

## What Next?
### Related Topics
- Cache Invalidation Techniques
- Advanced Caching Strategies
- Comparison of Caching Technologies

### Topics for Deeper Understanding
- In-depth Analysis of Cache Eviction Policies
- Performance Metrics for Caching
- Case Studies on Caching in Large-Scale Systems
