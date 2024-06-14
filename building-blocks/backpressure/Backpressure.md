# Backpressure in Software Systems

Backpressure (or back pressure) is a concept that nearly every software engineer will encounter, often dealing with it frequently. Despite its importance, the term isn't always well understood. This document aims to clarify what backpressure is, when it commonly occurs, and the strategies to mitigate it.

## What is Backpressure?

In the software world, backpressure is an analogy borrowed from fluid dynamics, where it refers to the resistance or force opposing the desired flow of fluid through pipes. In software, this can be redefined as:

> Resistance or force opposing the desired flow of data through software.

The purpose of software is to take input data and turn it into some desired output data, such as JSON from an API, HTML for a webpage.

Backpressure occurs when the process of turning input into output is resisted, often due to computational speed or other delays like waiting for user actions.

## Examples of Backpressure

### 1. Chocolate Factory
Lucy works at a candy packaging plant, struggling to keep up with a conveyor belt that's moving too fast. This is a classic example of backpressure. Lucy attempts to buffer (set aside candies) and drop (eat or hide them), illustrating common backpressure strategies.

### 2. Reading and Writing Files
Writing to a file is typically slower than reading from it. 

**For example**, with a hard drive that reads at 150 MB/s and writes at 100 MB/s, reading and writing simultaneously would require buffering 50 MB every second. 

This growing memory deficit illustrates the need to only read as fast as you can write, often managed by I/O libraries with "streams" and "pipes."

### 3. Server Communication
In microservice architectures, one server can send requests faster than another can process.

**For example**, if Server A sends 100 requests per second (rps) but Server B can only handle 75 rps, there's a 25 rps deficit.

![](https://miro.medium.com/v2/resize:fit:720/format:webp/1*ZQWlVVyCANAmgUKJU9xUlw.gif)

**3 options:**

**Buffering:**
- Buffering that 25 rps deficit is one option, but if that increase remains constant it’ll soon run out of memory and fall over.

**Dropping**
- Dropping requests is another option, but it’s a pretty common requirement that dropping requests is not acceptable.

**Control rate at requester side**
- The ideal option is for server B to control the rate in which server A sends requests, but again that’s not always viable.
	- if server A is requesting on behalf of a user, you can’t always tell or control the user to slow down, but sometimes you can! 
- Still, it’s often better to have the requesting server buffer, so you can better distribute the memory load down-stream, where the stress is, and not impact other requestors.
	- For example, if three different types of services (A, B, C) all make requests to the same downstream service (Z)  
	- If one of the four (A) is experiencing high load, service Z could effectively tell service A to “slow down” (control the producer) causing service A to buffer the requests. 
	- If that continued, eventually service A would run out of memory, however, the other two services (B, C) would remain up, as would the downstream service Z because it wasn’t allowing one misbehaving service to deny equal access for the others. 
	- An outage in this case might be inevitable, but we limited the scope and prevented a cascading Denial of Service. 
- This would be a case of controlling the producer, who then buffers because they can’t control their own producer (the user). In this case someone has to buffer, but who is the important part.


### 4. Rendering UI
Backpressure in UI apps can occur when rendering speed can't match the rate of incoming data, such as a WebSocket emitting 20,000 events per second. 

Strategies include buffering messages and periodically rendering them or dropping excess messages to maintain performance.

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*feQArAYERutZ451cMQSV6w.gif)

## Strategies for Handling Backpressure
Aside from scaling up your available compute resources, how you handle backpressure can pretty much be summed up with three possible options:

### Control the Producer
Slowing down or speeding up the producer based on the consumer's capacity is the most effective strategy, minimizing memory use and data loss.

### Buffering
Temporarily accumulating data spikes can be effective but dangerous if unbounded. Always ensure buffers have size or time limits to avoid memory crashes.

### Dropping
Sampling a percentage of incoming data is often used alongside buffering to manage excessive data flow without overwhelming the system.

### Ignoring Backpressure
In some non-critical scenarios, it might be acceptable to ignore backpressure if it's not causing significant issues.

## Choosing a Strategy

User experience (UX) can guide the choice of strategy. For instance, updating a table 100,000 times per second might be unnecessary and detrimental to UX. Instead, sampling data and presenting it at a manageable rate could be more effective.

## Backpressure in Code

### Pull-Based Streams
With pull-based streams, the consumer controls the producer, typically in a request-response pattern. Examples include Node.js Streams, Web Streams, and Async Iterators.

### Push-Based Streams
With push-based streams, the producer controls the data flow, pushing it to the consumer when available. This is common in user input scenarios, with popular libraries like RxJS and RxJava.

## Summary

Understanding and managing backpressure is crucial for scaling software systems effectively. From handling rapid mouse movements to managing server loads, backpressure is a challenge that can be addressed with appropriate strategies.

## What's Next?

### Related Topics
- **Chaos Engineering**: Intentionally inducing failures in production to test resiliency and failovers.
- **Reactive Programming**: Utilizing asynchronous data streams and backpressure handling in various programming languages.

### Deeper Understanding
- **Detailed Backpressure Strategies**: Exploring advanced techniques and tools for managing backpressure.
- **Performance Tuning**: Strategies for optimizing software performance while maintaining a good UX.
- **Microservices Architecture**: In-depth study of designing resilient and scalable microservice ecosystems.

