# Load Balancer

## Introduction
Load balancers distribute incoming client requests to computing resources such as application servers and databases. They ensure that the response from the computing resource is returned to the appropriate client. Load balancers are effective at:
- Preventing requests from going to unhealthy servers
- Preventing overloading resources
- Helping to eliminate a single point of failure

Load balancers can be implemented with hardware (which can be expensive) or with software solutions like HAProxy.

## Benefits
### SSL Termination
- Decrypt incoming requests and encrypt server responses to offload this work from backend servers.
- Removes the need to install X.509 certificates on each server.

### Session Persistence
- Issues cookies and routes a specific client's requests to the same instance if the web apps do not keep track of sessions.

### Fault Tolerance
To protect against failures, it's common to set up multiple load balancers, either in active-passive or active-active mode.

## Traffic Routing
Load balancers can route traffic based on various metrics, including:
- Random
- Least loaded
- Session/cookies
- Round robin or weighted round robin
- Layer 4
- Layer 7

## Types of Load Balancing
### Layer 4 Load Balancing
Layer 4 load balancing involves making routing decisions based on IP addresses and TCP or UDP ports. The load balancer views traffic at the packet level, making decisions for each packet independently.

### Layer 7 Load Balancing
A layer 7 load balancer makes routing decisions based on IPs, TCP or UDP ports, or any information it can get from the application protocol (mainly HTTP like HTTP headers etc.).

The layer 7 load-balancer acts as a proxy, which means it maintains two TCP connections: one with the client and one with the server. The packets are re-assembled, and then the load balancer can make a routing decision based on the information it can find in the application requests or responses.

**Note**: At the cost of flexibility, layer 4 load balancing requires less time and computing resources than layer 7, although the performance impact can be minimal on modern commodity hardware.

## Horizontal Scaling
Load balancers can also help with horizontal scaling, improving performance and availability.

Scaling out using commodity machines is more cost-efficient and results in higher availability than scaling up a single server on more expensive hardware, known as vertical scaling.

### Disadvantages of Horizontal Scaling
- Introduces complexity and involves cloning servers.
- Servers should be stateless: they should not contain any user-related data like sessions or profile pictures.
- Sessions can be stored in a centralized data store such as a database (SQL, NoSQL) or a persistent cache (Redis, Memcached).
- Downstream servers such as caches and databases need to handle more simultaneous connections as upstream servers scale out.

### Disadvantages of Load Balancers
- The load balancer can become a performance bottleneck if it does not have enough resources or if it is not configured properly.
- Introducing a load balancer to help eliminate a single point of failure results in increased complexity.
- A single load balancer is a single point of failure, and configuring multiple load balancers further increases complexity.

## Conclusion
Load balancers are essential for distributing client requests and improving the availability and reliability of applications. They come with various benefits such as SSL termination, session persistence, and fault tolerance. However, they also introduce complexity and potential performance bottlenecks.

## Next Topics
### Related Topics
- **Reverse Proxy**: Understanding how reverse proxies work and their use cases.
- **High Availability**: Strategies and configurations to ensure high availability in systems.
- **Caching**: Implementing caching mechanisms to reduce load on backend servers.

### Topics for Deeper Understanding
- **Advanced Load Balancing Algorithms**: Exploring more sophisticated algorithms for load balancing.
- **Load Balancer Configuration**: Best practices for configuring load balancers for optimal performance.
- **Security in Load Balancers**: Ensuring load balancers are secure and do not introduce vulnerabilities.

