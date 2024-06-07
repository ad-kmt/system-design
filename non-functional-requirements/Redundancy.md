# Redundancy in Distributed Systems

## What is Redundancy?

In distributed systems, **Redundancy** refers to the duplication of critical components (such as web servers and database servers) to increase reliability and availability. This concept ensures that the system continues to operate even if some components fail, thereby providing a backup or failsafe. The term redundancy is used because the duplicate device or component is idle and redundant when everything is functioning correctly.

### Why is Redundancy Important?

Redundancy prevents a single point of failure, which is a critical aspect in distributed systems. By duplicating or adding components, the system becomes more resilient and less prone to failure.

For example, consider a system with two identical web servers managed by a load balancer. Traffic is evenly distributed between the two servers, but if one fails, the load balancer redirects all traffic to the remaining functioning server, thereby enhancing the reliability of the system.

## Types of Redundancy

### Passive Redundancy

**Passive Redundancy** involves duplicating components in a system without actively using them. When the primary component is functioning correctly, the redundant components remain in a standby or passive state. They monitor the primary component's status and take over if a failure is detected.

#### When to Use Passive Redundancy?

- When the system must ensure that the state of the redundant component is sufficiently fresh before resuming services.
- In scenarios where periodic switchovers (e.g., once a day or once a week) can increase system availability by ensuring standby components are ready.
- For use cases where data retrieval speed is not critical, such as data archiving systems, passive redundancy can be used for backup and recovery purposes.
- Passive redundancy may require other fault-tolerant techniques like active monitoring, regular testing of redundant components, and fault detection mechanisms to ensure reliability.

### Active Redundancy

**Active Redundancy** involves multiple identical components operating simultaneously in parallel, executing tasks concurrently and sharing the workload. All components actively contribute to the system's operations at the same time and work in a coordinated manner.

#### When to Use Active Redundancy?

- When uninterrupted operation is essential (high-availability environments).
- In scenarios demanding fast response and minimal latency.
- When significant processing power is required (high traffic situations).
- For seamless scalability and rapid recovery in the event of a failure.
- Active redundancy ensures smooth failover by automatically transferring the workload from the failed component to the remaining active components.

## Redundancy vs. Replication

While redundancy and replication are often used interchangeably, they serve different purposes:

- **Redundancy** focuses on providing backup components to handle failures, enhancing fault tolerance and availability by minimizing downtime and ensuring continuous operation.
- **Replication** aims to create and maintain consistent copies of data across multiple components, ensuring data consistency, availability, and performance.

Replication can be a part of redundancy because redundant components often require synchronized copies of data to operate effectively.

## Factors Influencing Redundancy

- **Storage Device Impact**: The choice of storage device impacts system performance, reliability, and scalability. Consider factors such as access times, throughput, latency, and durability.
- **Data Consistency**: Mechanisms are required to ensure data consistency in active redundancy.
- **Fault Detection**: Implementing fault detection mechanisms presents challenges that need to be addressed to ensure system reliability.
- **Reliability Measurement**: Quantifying the reliability of redundant systems is essential for understanding their effectiveness.
- **Automated Monitoring**: Automated monitoring and alerting systems play a crucial role in detecting faults and maintaining system health.

# Resources

https://www.enjoyalgorithms.com/blog/storage-and-redundancy/

## What's Next?

### Related Topics

- Load Balancing
- Fault Tolerance
- High Availability

### Deeper Understanding

- Detailed study of fault detection mechanisms
- Advanced replication techniques
- Scalability strategies in distributed systems

