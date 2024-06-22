# Consistent Hashing

## Introduction
In the world of cloud computing and big data, distributed systems have become increasingly popular and essential. Among these systems, **distributed caches** power many high-traffic websites and web applications. These systems often rely on a particular kind of **distributed hashing**, taking advantage of an algorithm known as **consistent hashing.**

## The Beginning: Understanding Hashing
To understand consistent hashing, it's essential to start with the basics of hashing.

### What is Hashing?
Hashing is a technique that converts input data of arbitrary size into a fixed-size value, typically an integer, known as a hash code. A good hash function distributes hash codes uniformly across the output range to minimize collisions, where different inputs might produce the same hash code.

### Introducing Hash Tables
A hash table uses hash codes to store data efficiently. Instead of searching through a long list, we can directly access the position in the array where our data is stored using its hash code. This makes data retrieval much faster.

## The Need for Distribution: Enter Distributed Hashing
As systems grow, we might need to distribute data across multiple computers (servers). This is where distributed hashing comes into play. By splitting data across several servers, we can overcome the limitations of a single computer's memory.

### Scaling Out
Distributed hashing works by distributing objects across multiple servers. A common use case is in-memory caches, which store data temporarily to speed up access. However, adding or removing servers can disrupt data distribution, causing inefficiency.

## The Rehashing Problem
Initially, a simple method might be used: hashing the data and taking the modulo of the number of servers. This works until the number of servers changes. If a server crashes or a new one is added, all the data needs to be rehashed, leading to significant disruption and inefficiency.

## The Solution: Consistent Hashing
Consistent hashing addresses the rehashing problem by using a more flexible approach that maps both servers and data to positions on a virtual circle (or hash ring).

### How Does Consistent Hashing Work?

1. **Virtual Hash Ring**: Imagine a circle where both servers and keys (data) are placed based on their hash values.
2. **Server Placement**: Servers are hashed using their IP addresses and placed at random positions on the circle.
3. **Key Placement**: Similarly, keys are hashed and placed on the circle.
4. **Key Assignment**: Each key is assigned to the server closest to it in the clockwise direction.

### Example
Imagine we have three servers (A, B, and C) and some keys. The servers and keys are assigned positions on the hash ring based on their hash values. Each key is assigned to the closest server in a clockwise direction.

![](https://miro.medium.com/v2/resize:fit:1400/1*u39w9GNeTHv00kVlwE8WVg.png)

## Benefits of Consistent Hashing
1. **Dynamic Scaling**: Consistent hashing allows for flexible allocation of servers and efficient handling of requests in a distributed system.
2. **Fault Tolerance**: When a server fails, only a minimal number of keys need to be reassigned to other servers, ensuring that the system remains operational.
3. **Load Balancing**: Replicating servers and distributing them around the hash ring ensures a uniform distribution of keys, preventing any single server from becoming a bottleneck.

## Handling Server Changes

### Adding a Server
When a new server is added, it is mapped using the hash function and allocated to a position on the hash ring. Keys that would map to this new server are reassigned accordingly. This helps in scaling and improving the system's throughput and latency.

![](https://cdn-images-1.medium.com/max/800/1*TCyBjcM0inmdwUyBKNeW5Q.png)

### Removing a Server
If a server fails, all keys previously mapped to it are redirected to the next server in the clockwise direction. This reallocation ensures that the service remains active and fault-tolerant.

![](https://cdn-images-1.medium.com/max/800/1*QFOoHHnmshI74uoYnGJOeQ.png)

In general, only k/N keys need to be remapped where k is the number of keys and N is the number of servers. Rest all keys will be untouched.

In our original naive hashing model, it costs us O(k) every time we need to add or remove a node, but inserting or removing a key is O(1). In our consistent hashing model, we can change the number of nodes with only O(k/N + log N) runtime; however, inserting or looking up a cache key will now take O(log N) instead of O(1) because we have to do a binary search to find the next node on the hash ring.

## Challenges and Solutions
### Non-Uniform Distribution
A potential issue with consistent hashing is that all keys might get mapped to the same server, leading to an uneven load. This can be mitigated by replicating servers and distributing these replicas around the hash ring to ensure a more uniform key distribution.

![](https://cdn-images-1.medium.com/max/800/1*XkPxtQv-H4qJ-cHXueyw-w.png)

## Conclusion
Consistent hashing is a crucial concept in designing distributed systems. It tackles scalability challenges with dynamic node assignment and provides fault tolerance. This approach is also useful in system design interviews and real-time applications, allowing for efficient request distribution and data mapping to servers. It helps achieve horizontal scaling, increases throughput, and improves application latency.

# Resources

https://www.enjoyalgorithms.com/blog/consistent-hashing-in-system-design/

https://www.toptal.com/big-data/consistent-hashing

## Next Topics
### Related Topics
- Distributed Systems
- Load Balancing
- Caching Strategies

### Deeper Understanding
- Advanced Hashing Techniques
- Fault Tolerance Mechanisms
- Scalability in Distributed Systems

