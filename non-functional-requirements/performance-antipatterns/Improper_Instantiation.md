# Improper Instantiation Antipattern

## What is the Improper Instantiation Antipattern?

The Improper Instantiation antipattern occurs when new instances of a class are repeatedly created, even though they are meant to be created once and shared. This behavior can severely hurt performance.

## Problem Description

Many libraries provide abstractions of external resources and manage their connections internally. These classes act as brokers that clients use to access resources.

These classes are designed to be instantiated once and reused throughout the application's lifetime. However, a common misunderstanding is that these classes should be acquired only as necessary and released quickly.

### Example Problem

In a web application, if a new `HttpClient` object is created for each user request, this technique is not scalable. Under heavy load, the web server may exhaust the number of available sockets, resulting in `SocketException` errors. This problem is not limited to the `HttpClient` class but also affects other classes that wrap resources or are expensive to create.

## Why is Improper Instantiation a Problem?

### Performance Issues

Repeatedly creating and destroying instances of a shareable object can lead to:

- Exhaustion of resources such as sockets, database connections, file handles, etc.
- Increased memory use and garbage collection.
- Increased network, disk, or database activity.
- Slower response times and increased error rates.

### Scalability Issues

Continuously creating and destroying instances, especially for classes that manage connections or are expensive to instantiate, adversely affects the system's scalability.

## How to Fix the Improper Instantiation Antipattern

If the class that wraps the external resource is shareable and thread-safe, you should create a shared singleton instance or a pool of reusable instances of the class.

### Considerations

- **Thread-Safety**: Objects shared across multiple requests must be thread-safe.
- **Singleton vs. Pooling**: The type of shared resource might dictate whether to use a singleton or a pool of instances.
- **Property Settings**: Be cautious about setting properties on shared objects, as this can lead to race conditions.
- **Resource Scarcity**: Some resources, like database connections, are scarce and should not be held onto unnecessarily.

### Example Solution

A static `HttpClient` instance can be used to share the connection across all requests, ensuring that a single instance is reused throughout the application's lifetime.

## How to Detect the Improper Instantiation Antipattern

Symptoms of this problem include a drop in throughput or an increased error rate. To detect this antipattern:

1. **Process Monitoring**: Monitor the production system to identify when response times slow down or the system fails due to lack of resources.
2. **Examine Telemetry Data**: Determine which operations create and destroy resource-consuming objects.
3. **Load Testing**: Simulate typical operations to identify which parts of the system suffer from resource exhaustion under varying loads.
4. **Source Code Review**: Examine how broker objects are managed in the source code.
5. **Stack Traces Analysis**: Analyze stack traces for slow-running operations or operations that generate exceptions under load.

# Resources

https://learn.microsoft.com/en-us/azure/architecture/antipatterns/improper-instantiation/

## What Next?

### Related Topics

- Singleton Design Pattern
- Resource Pooling
- Thread-Safety in Shared Resources
- Effective Use of Connection Management Libraries

### Topics for Deeper Understanding

- Performance Tuning in High-Load Systems
- Advanced Diagnostics with Application Performance Management (APM) Tools
- Best Practices for Resource Management in .NET Applications

