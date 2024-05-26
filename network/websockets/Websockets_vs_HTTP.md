# WebSockets vs HTTP

## Introduction

HTTP and WebSocket are both communication protocols used in client-server communication. However, they differ significantly in their design and use cases. This document explores these differences, their respective features, and when to use each protocol.

## What is HTTP?

### Overview

HTTP (Hypertext Transfer Protocol) is a unidirectional communication protocol where the client sends a request and the server sends a response. Each request is associated with a corresponding response, and the connection is closed after the response is received.

[![](https://media.geeksforgeeks.org/wp-content/uploads/20191203183429/HTTP-Connection.png)](https://www.geeksforgeeks.org/what-is-web-socket-and-how-it-is-different-from-the-http/)

### Characteristics of HTTP

- **Unidirectional**: The client sends a request, and the server sends a response.
- **Stateless**: Each request is independent and unrelated to previous requests.
- **Connection-Oriented**: HTTP runs on top of TCP, ensuring reliable data transfer using methods like three-way handshaking and retransmitting lost packets.
- **New Connection per Request**: Each HTTP request opens a separate TCP connection to the server, which is closed after the response is received.
- **ASCII Encoded Messages**: HTTP messages are encoded in ASCII and include details like the HTTP protocol version, methods (GET/POST), headers (content type, content length), and the body containing the actual message.

### Use Cases for HTTP

HTTP is suitable for fetching data that does not require real-time updates or continuous streaming. Examples include:
- Loading web pages
- Fetching old data
- RESTful web services for data retrieval

## What is WebSocket?

### Overview

WebSocket is a bidirectional, full-duplex communication protocol used for real-time communication between client and server. Unlike HTTP, WebSocket connections remain open until terminated by either party.

![](https://media.geeksforgeeks.org/wp-content/uploads/20191203183648/WebSocket-Connection.png)

### Characteristics of WebSocket

- **Bidirectional**: Data can be sent and received simultaneously between client and server.
- **Stateful**: The connection remains open and active until explicitly closed by either the client or server.
- **Persistent Connection**: A single connection channel is used for continuous data exchange, improving performance for real-time applications.
- **Full-Duplex**: Allows simultaneous two-way communication.

### Use Cases for WebSocket

WebSocket is ideal for scenarios requiring real-time updates and continuous data streams. Examples include:
- **Real-Time Web Applications**: Continuously pushing data from the backend server to the client (e.g., live trading platforms).
- **Gaming Applications**: Real-time data updates without refreshing the UI.
- **Chat Applications**: Maintaining a single connection for message exchange, publishing, and broadcasting.

## When Not to Use WebSocket

WebSocket should not be used for fetching old data or data that only needs to be retrieved once. In such cases, HTTP is more appropriate due to its simplicity and efficiency for non-real-time data requests.

## Differences Between HTTP and WebSocket

| Feature | WebSocket Connection | HTTP Connection |
|---------|----------------------|-----------------|
| **Communication** | Bidirectional, data can be sent from client to server and server to client using the same connection. | Unidirectional, client sends request and server sends response, connection closes after response. |
| **State** | Stateful, connection remains open until terminated by either party. | Stateless, each request is independent and closes after response. |
| **Use Cases** | Real-time applications (e.g., trading, monitoring, notifications). | Simple RESTful applications, non-real-time data requests. |
| **Performance** | Faster for frequently updated applications due to persistent connection. | Slower, as each request opens and closes a new connection. |

## Why HTTP Takes More Network Resources and Bandwidth Compared to WebSockets

### Overhead of HTTP Headers
- **HTTP Headers**: Every HTTP request and response includes headers that carry metadata about the data being exchanged. These headers can be quite large relative to the actual payload, especially for small messages.
- **Frequent Handshakes**: Each HTTP request often involves establishing a new connection (unless persistent connections are used), which requires multiple handshakes and header exchanges, adding to the overall overhead.

### Request-Response Pattern
- **Stateless Communication**: HTTP is a stateless protocol, meaning each request is independent and necessitates a full round trip (request and response). This results in additional network traffic for every single interaction.
- **Sequential Requests**: HTTP requests are typically issued sequentially, with the client waiting for a response before sending the next request. This can introduce delays and increase latency, particularly in high-frequency communication scenarios.

### Lack of Efficient Bidirectional Communication
- **Separate Connections**: For bidirectional communication, HTTP often requires two separate connections (one for client-to-server and another for server-to-client communication), doubling the resource requirements.
- **Polling Mechanisms**: Techniques like long polling keep connections open longer but still involve frequent new requests, consuming more bandwidth and server resources.

### WebSocket Efficiency
- **Single Connection**: WebSockets establish a single, persistent connection for full-duplex communication, eliminating the need for repeated handshakes.
- **Minimal Headers**: After the initial handshake, WebSocket frames have significantly smaller headers compared to HTTP, reducing the overhead for each message.
- **Continuous Data Stream**: WebSockets support continuous, low-latency data streams, allowing for more efficient and real-time data exchange without the overhead of multiple HTTP requests.

## Conclusion

Choosing between WebSocket and HTTP depends on the specific needs of your project. WebSocket is suitable for real-time, continuous data streams, while HTTP is better for one-time data retrieval and non-real-time applications.

## What Next?

### Related Topics

- HTTP/2 and its benefits over HTTP/1.1
- Long Polling and Server-Sent Events (SSE) as alternatives to WebSockets

### Deeper Understanding

- WebSocket security considerations
- Advanced use cases of WebSockets in modern web applications
- Detailed comparison of WebSocket with other real-time communication protocols

# Resources
https://www.geeksforgeeks.org/what-is-web-socket-and-how-it-is-different-from-the-http/

