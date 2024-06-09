# Server-Sent Events (SSE)

## Introduction
Server-Sent Events (SSE) is a technology that enables servers to push real-time updates to clients over a single HTTP connection.

SSE offers a simple and efficient way for server applications to send data to clients.

Unlike traditional HTTP requests where the client must continuously poll the server for updates, SSE allows the server to send data to the client as soon as it becomes available.

This makes SSE ideal for scenarios requiring real-time, one-way data flow.

## What is SSE?

### Definition
Server-Sent Events (SSE) is a server push technology that establishes a long-lasting connection between the client and the server, allowing the server to automatically send updates to the client via an HTTP connection. It uses the EventSource interface in the browser to receive these updates.

![](https://ucarecdn.com/6057a5a8-2aed-4e79-92bf-d0d5d54ec7f7/)

### How SSE Works
**Client-Side**: The client creates an EventSource object with the URL of the SSE endpoint. This establishes a connection and listens for incoming events.
**Server-Side**: The server responds to the client's request with an HTTP status code 200 OK and a Content-Type header set to text/event-stream. It then sends a continuous stream of events.

### Event Format
Events are formatted as plain text with the following structure:

```
event: eventType
data: eventData
```

Events are separated by newlines, and the stream remains open until the client or server closes it.

## Advantages of Using SSE
### Simplicity and Ease of Use
SSE provides a straightforward way to establish a unidirectional connection between the server and the client. The client subscribes to an SSE endpoint, and the server pushes data over this connection without requiring constant client requests.

### Reduced Network Overhead
SSE significantly reduces network overhead compared to polling techniques, as the server only sends data when new information is available, minimizing unnecessary data transfers.

### Standardized Protocol
SSEs use the HTTP protocol, making them easily deployable and compatible with existing web infrastructure. They eliminate the need for additional protocols or libraries.

### Automatic Reconnection
SSEs automatically handle reconnection in case of network disruptions or server failures. The client will try to reconnect to the server and continue receiving events.

### Cross-Domain Support
SSEs support cross-domain communication, making them suitable for scenarios where the server and client are hosted on different domains.

### Compatibility
SSEs are supported by modern web browsers, ensuring broad compatibility without additional plugins or software installations.


## Implementing SSE
### Client-Side Implementation
The client creates a new EventSource object to receive events from the server:

```javascript
const eventSource = new EventSource("/event-stream");

eventSource.onmessage = event => {
  const li = document.createElement("li");
  const ul = document.getElementById("list");

  li.textContent = `message: ${event.data}`;
  ul.appendChild(li);
};
```

## Server-Side Implementation
The server responds to an HTTP request from the client with event messages:

```
HTTP/1.1 200 OK
Content-Type: text/event-stream
Cache-Control: no-cache
Connection: keep-alive

id: 1
event: message
data: Hello, world!
```

The server must maintain a list of connected clients to emit new stream events and handle connection drops gracefully.

## Use Cases for SSE
### Real-Time Notifications
SSE is ideal for broadcasting notifications such as news updates, social media alerts, and live event broadcasting.

### Live Data Updates
SSE can be used for applications requiring frequent updates, such as stock tickers, sports scores, and real-time analytics.

### Progress Updates
SSE allows the server to send periodic updates about the status of long-running processes, enabling users to monitor the operation.

### IoT Applications
SSE can be employed in IoT scenarios to push updates about the status of sensors, alarms, or other devices.

## Security and Performance
### Authentication
SSE uses HTTP for connection initiation, allowing session cookies for authentication. However, handling tokens securely requires additional considerations, such as using third-party libraries.

### Performance
SSE supports high throughput and low latency. Companies like Shopify and Split use SSE in production to handle billions of events with low latency.

### Scalability
SSE can scale to handle many connections, but scaling horizontally requires careful planning, load balancing, and maintaining data consistency using message brokers like Redis.

## Conclusion
Server-Sent Events provide a robust solution for real-time, one-way data updates from the server to the client. They offer simplicity, reduced overhead, and broad compatibility, making them ideal for many real-time applications.

## What Next?
### Related Topics
- **WebSockets**: Understanding full-duplex communication.
- **HTTP/2**: Benefits for SSE and other web technologies.

### Deeper Understanding
**Load Balancing SSE Connections**: Techniques and best practices.
**Security in SSE**: Handling authentication and authorization securely.
**Performance Optimization**: Scaling SSE for high-throughput applications.
