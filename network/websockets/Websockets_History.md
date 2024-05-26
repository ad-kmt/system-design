# History of WebSockets

## Introduction
WebSockets have revolutionized the way we build realtime web applications by providing a full-duplex communication channel over a single, long-lived connection. This markdown file explores the evolution of web technologies leading to the advent of WebSockets, highlighting their significance and use cases.

## The Road to WebSockets

### The Birth of the World Wide Web
In 1989, Tim Berners-Lee, a software engineer at CERN, proposed the "WorldWideWeb" project to facilitate access to information stored on different computers. This project led to the creation of the web by combining hypertext and the internet, resulting in three core technologies:
- **HTML**: The markup language of the web.
- **URI**: Unique addresses identifying each resource on the web.
- **HTTP**: The protocol used for requesting and receiving web resources.

The initial version of HTTP (HTTP/0.9) was very basic, consisting of single-line requests and simple hypertext responses. As interest in the web grew, HTTP evolved to include headers, status codes, and support for additional content types, leading to the development of HTTP/1.0 and HTTP/1.1 with enhanced features and performance optimizations.

### JavaScript Joins the Fold
In 1995, Netscape introduced JavaScript, a scripting language that allowed dynamic interactions on the web. This addition enabled the creation of more interactive and responsive web applications, marking a significant step towards realtime web experiences.

### Hatching the Realtime Web
The late 1990s saw the emergence of the first web applications using JavaScript and HTTP. To deliver realtime experiences, developers initially relied on HTTP-based techniques like AJAX and Comet.

#### AJAX (Asynchronous JavaScript and XML)
AJAX allows asynchronous data exchange with a server without reloading the entire web page. This technique involves:
- HTML and CSS for presentation.
- DOM for dynamic display.
- XMLHttpRequest for asynchronous communication.
- JavaScript for binding everything together.

[![](https://websocket.org/_astro/how-ajax-works.f030a959_1037l0.webp)](https://websocket.org/guides/road-to-websockets/)

Google popularized AJAX with applications like Gmail and Google Maps, paving the way for dynamic, realtime web applications.

#### Comet
Comet enables web servers to push updates to the client using long-lived HTTP connections. Techniques like long polling and HTTP streaming facilitated this model, allowing servers to push updates as soon as they were available.

#### Long Polling
Long polling is a technique where the server holds a client's connection open until data becomes available or a timeout is reached. Upon receiving a response, the client immediately issues another request. This approach reduces the frequency of requests compared to regular polling, but it still involves significant server overhead to handle many simultaneous long polling connections.

![](https://websocket.org/_astro/long-polling.d7000adb_Vn4A9.webp)

#### HTTP Streaming
HTTP streaming, also known as HTTP server push, is a technique where the server continuously sends data to the client over a single, long-lived HTTP connection. The server sends updates whenever available, only closing the connection when explicitly instructed to do so.

This method leverages chunked transfer encoding in HTTP/1.1, allowing data to be sent in chunks and processed by the client as it arrives.

#### Server-Sent Events (SSE)
Server-Sent Events (SSE) is a server push technology standardized as part of HTML5 by the World Wide Web Consortium (W3C). SSE allows servers to push updates to the client using a single, long-lived HTTP connection. The client uses the EventSource API to receive these updates in real time. SSE is commonly used for message updates or continuous data streams from the server to the client.


## Limitations of HTTP for Realtime Applications
While AJAX and Comet brought significant improvements, they still had limitations due to the inherent nature of HTTP:
- **Scalability**: High polling frequencies increased network traffic and server load.
- **Unreliable Message Ordering**: Network conditions could cause message delays or reordering.
- **Latency**: Establishing new HTTP connections involved significant overhead.
- **Lack of Bidirectional Streaming**: HTTP did not support continuous, bidirectional communication.

These limitations highlighted the need for a more efficient protocol for realtime web communication.

## Enter WebSockets

### The Birth of WebSockets
In 2008, developers Michael Carter and Ian Hickson proposed WebSockets as a solution to the limitations of Comet and HTTP. WebSockets enable bidirectional, full-duplex communication over a single, persistent connection. The WebSocket protocol starts with an HTTP handshake but then switches to a more efficient communication model.

### WebSockets vs. HTTP
| Feature                      | WebSockets              | HTTP/1.1                |
|------------------------------|-------------------------|-------------------------|
| Communication                | Full-duplex             | Half-duplex             |
| Message Exchange Pattern     | Bidirectional           | Request-response        |
| Server Push                  | Core feature            | Not natively supported  |
| Overhead                     | Minimal per message     | Moderate per request    |
| State                        | Stateful                | Stateless               |

![](https://websocket.org/_astro/websocket-vs-http.be03ced1_sWP4f.webp)

### Use Cases and Benefits
WebSockets are ideal for:
- **Realtime Updates**: Streaming low-latency updates to clients (e.g., live sports updates, dashboards).
- **Bidirectional Communication**: Enabling chat applications, virtual events, and multi-user collaboration.

#### Benefits of WebSockets
- **Improved Performance**: Reduced overhead and bandwidth usage.
- **Extensibility**: Support for subprotocols and extensions.
- **Fast Reaction Times**: Event-driven communication for immediate data transfer.

## Adoption and Standardization
Initially included in the HTML5 specification in 2008, the WebSocket protocol was standardized in 2011 via RFC 6455. Google Chrome 4 was the first browser to support WebSockets, followed by other major browsers. Today, WebSockets are widely used across various platforms, including mobile apps.

## Conclusion
WebSockets have transformed the landscape of web development, enabling the creation of scalable, low-latency realtime applications. Their adoption continues to grow, supported by a thriving community and a variety of tools and implementations.

## What Next

### Related Topics
- **HTTP/2 and HTTP/3**: Evolution of HTTP protocols for improved performance.
- **Server-Sent Events (SSE)**: Another method for server-to-client streaming.
- **WebRTC**: Real-time communication for audio, video, and data sharing.

### Topics for Deeper Understanding
- **WebSocket Subprotocols and Extensions**: Advanced customization for specific use cases.
- **Scaling WebSocket Applications**: Strategies for handling high traffic and concurrency.
- **Security in WebSocket Communication**: Ensuring secure and reliable data transfer.

# Resources
https://websocket.org/guides/road-to-websockets/
