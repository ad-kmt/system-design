# Busy Front End Antipattern

## Problem Description

In front-end apps, performing asynchronous work on a large number of background threads can starve other concurrent foreground tasks of resources, leading to decreased response times and high latency.

Offloading a resource-intensive task to a separate thread helps keep the application responsive while processing happens in the background. However, tasks on background threads still consume resources. Too many such tasks can starve threads handling user requests.

### Key Issues

- **Resource Utilization**: High CPU, memory, network, or disk I/O consumption can degrade performance.
- **Monolithic Design**: Applications developed as monolithic pieces often encounter this issue, where all business logic is combined into a single tier shared with the presentation layer.

## How to Fix the Problem

### Solution: Separate Back End

Move resource-intensive processes to a separate back end. The front end should place these tasks onto a message queue. The back end picks up tasks for asynchronous processing, using the queue as a load leveler to buffer requests. Autoscaling can be configured to handle increased queue lengths.

### Implementation

1. **Message Queue**: Use a Service Bus queue for task management.
2. **Back End Processing**: Handle tasks asynchronously in the back end, ensuring that the front end remains responsive.

### Considerations

- **Complexity**: Complexity increases with the need to handle queuing and dequeuing safely.
- **Dependencies**: Introduces reliance on additional services for message queuing.
- **Scalability**: The processing environment must scale to handle workload and throughput.
- **Task Duration**: While front end responsiveness improves, back end task completion may take longer.

## How to Detect the Problem

### Symptoms

- **High Latency**: During resource-intensive tasks.
- **Extended Response Times**: End users report slow performance or failures.
- **HTTP Errors**: 500 (Internal Server) or 503 (Service Unavailable) errors in logs.

### Diagnostic Steps

1. **Process Monitoring**: Identify slow response times.
2. **Telemetry Data**: Analyze operation mix and resource usage during slowdowns.
3. **Correlations**: Find links between poor performance and specific operations.
4. **Load Testing**: Determine resource-heavy operations.
5. **Code Review**: Inspect source code for excessive resource consumption causes.

### Example Diagnosis

#### Identify Points of Slowdown

- **Instrumentation**: Track duration and resource consumption of each request.
- **Monitoring**: Observe how requests compete and affect each other, especially under stress.

#### Examine Telemetry Data

- **Metrics Analysis**: CPU and network I/O rates during load.
- **Hypothesis Confirmation**: Isolate operations causing high resource usage.

#### Perform Load Testing

- **Controlled Environment**: Compare performance with and without specific requests.
- **Results**: Identify operations that significantly reduce performance.

#### Review Source Code

- **Asynchronous Operations**: Avoid CPU-intensive tasks on background threads.
- **Thread Limits**: Be aware of server thread limitations and potential exceptions.

## Implementing the Solution and Verifying Results

### Performance Monitoring

- **Post-Implementation**: Monitor system under similar loads to compare performance.
- **Improved Metrics**: Expect faster response times and increased request volume handling.

### Example Metrics

- **CPU Utilization**: Should not reach 100%.
- **Network Requests**: Volume should be higher and more stable than before.

# Resource

https://learn.microsoft.com/en-us/azure/architecture/antipatterns/busy-front-end/

## Next Topics to Cover

### Related Topics

- **Asynchronous Programming Best Practices**
- **Service Bus Queue Management**
- **Load Balancing Techniques**

### Deeper Understanding

- **Scalability Strategies**
- **Resource Management in Distributed Systems**
- **Advanced Telemetry and Monitoring Tools**
