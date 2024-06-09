# Evolution of HTTP

HTTP (HyperText Transfer Protocol) is the backbone of the World Wide Web, enabling computers to exchange information effortlessly. Developed by Tim Berners-Lee and his team between 1989-1991, HTTP has evolved significantly, maintaining its simplicity while becoming more flexible. This document outlines the evolution of HTTP from its inception to the modern protocols that support high-resolution images and videos.


## Invention of the World Wide Web

In 1989, while working at CERN, Tim Berners-Lee proposed building a hypertext system over the internet, initially called the Mesh, later renamed the World Wide Web in 1990. The World Wide Web consisted of four building blocks:
- **HTML**: A textual format to represent hypertext documents.
- **HTTP**: A simple protocol to exchange these documents.
- **Web Browser**: The first client to display and edit these documents.
- **Server**: An early version of httpd to give access to the documents. httpd stands for "HTTP Daemon." It is a software program that runs in the background on a server and waits for incoming HTTP requests

## HTTP/0.9 - The One-Line Protocol

HTTP/0.9, the initial version of HTTP, had no version number and was later named 0.9 to differentiate it from subsequent versions. It was extremely simple:

- **Request nature**: single-line (method + path for requested document)
- **Response**: hypertext only
- **Methods supported**: GET only
- **Connection nature**: terminated immediately after the response

### Example
```http
GET /mypage.html
```

#### Problems
No HTTP headers (cannot transfer other content type files), No status/error codes, No URLs, No versioning

## HTTP/1.0 - Building Extensibility

HTTP/0.9's simplicity was limiting, leading to the development of HTTP/1.0, which introduced several enhancements:

- **Request**
    - **Versioning**: HTTP version information sent within each request.
    - **Methods supported**: GET , HEAD , POST
- **Response**:
    - **Status Code Line**: Sent at the beginning of a response.
    - **Content-Type Header**:not limited to hypertext (Content-Type header provided ability to transmit files other than plain HTML files — e.g. scripts, stylesheets, media)
    - **HTTP Headers**: For both requests and responses to transmit metadata.

- **Connection nature**: terminated immediately after the response


#### Request
```
GET /mypage.html HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)
```

#### Response
```
200 OK
Date: Tue, 15 Nov 1994 08:12:31 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/html

<HTML>
A page with an image
  <IMG SRC="/myimage.gif">
</HTML>
```

### Problem with **HTTP/0.9** and **HTTP/1.0**
- Establishing a new connection for each request was a major problem in both **HTTP/0.9** and **HTTP/1.0**.
- Each time a new connection establishes, a TCP three-way handshake should also occur. For better performance, it was crucial to reduce these round-trips between client and server. HTTP/1.1 solved this with persistent connections.

## HTTP/1.1 - The Standardized Protocol
Published in early 1997, HTTP/1.1 brought numerous improvements and became the standardized version:

- **Persistent Connections**: Reuse of a connection to save time.
    - allowing multiple requests and responses to be sent over the same TCP connection.
    - This reduced the overhead of establishing new TCP connections (TCP Handshake) for each request, resulting in faster data transfer and improved performance.
- **Pipelining**: Send a second request before the first response is fully transmitted.
    - This concurrent processing of requests reduced the impact of head-of-line blocking, enabling resources to be fetched more efficiently, especially when a webpage required multiple elements to load, such as images, stylesheets, and scripts.
- **Chunked Responses**: Support for chunked transfer encoding.
- **Additional Cache Control**: Enhanced cache mechanisms.
- **Content Negotiation**: Agreement on content type, language, and encoding.
- **Host Header**: Allowed hosting different domains from the same IP address.
    - This capability became essential as the number of websites on the internet grew rapidly, requiring better organization and resource allocation.
- **Methods supported**: GET , HEAD , POST , PUT , DELETE , TRACE , OPTIONS
- **Connection nature**: long-lived

#### Request
```
GET /en-US/docs/Glossary/CORS-safelisted_request_header HTTP/1.1
Host: developer.mozilla.org
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://developer.mozilla.org/en-US/docs/Glossary/CORS-safelisted_request_header
```

#### Response
```
200 OK
Connection: Keep-Alive
Content-Encoding: gzip
Content-Type: text/html; charset=utf-8
Date: Wed, 20 Jul 2016 10:55:30 GMT
Etag: "547fa7e369ef56031dd3bff2ace9fc0832eb251a"
Keep-Alive: timeout=5, max=1000
Last-Modified: Tue, 19 Jul 2016 00:59:33 GMT
Server: Apache
Transfer-Encoding: chunked
```

### Problems with HTTP/1.1
**Head-of-Line Blocking:**
- HTTP/1.1 operates over a single TCP connection for each request-response pair. This causes head-of-line blocking, where a single slow request can delay all subsequent requests in the queue.
- Even with pipelining, responses must be returned in the same order as the requests were sent. If one request takes longer to process, subsequent requests still have to wait, causing head-of-line blocking.

**Inefficient Use of Connections:**
Although HTTP/1.1 introduced persistent connections to reduce the overhead of establishing new connections, multiple parallel connections were often needed to achieve better performance. This led to inefficient use of network resources.

**Redundant Headers:**

HTTP/1.1 required headers to be sent with every request and response. Many of these headers were identical across requests, leading to significant overhead.

**Lack of Multiplexing:**

HTTP/1.1 could not handle multiple requests and responses simultaneously over a single connection. This limitation meant that each resource required a separate request-response cycle, increasing latency and reducing performance.

**Security Concerns:**

While not a direct limitation of HTTP/1.1 itself, the lack of default encryption and the need for separate handling of HTTPS added complexity and potential security risks.

#### Multiplexing vs Pipelining

Multiplexing and pipelining are both techniques to improve data transfer efficiency, but they differ in their approach:

- **Pipelining**: Allows multiple HTTP requests to be sent out in sequence without waiting for the corresponding responses. However, responses must still be received in order, which can lead to head-of-line blocking if one request takes longer to process.

- **Multiplexing**: Enables multiple requests and responses to be sent and received independently over a single connection. This means that delays in one request do not block others, reducing latency and improving overall performance.

## HTTP/2 - Revolutionizing Web Communication
Introduced to address the limitations of HTTP/1.1, HTTP/2 brought major advancements. The primary motivation behind its development was to enhance the performance and efficiency of data transfer on the web.

- **Binary Protocol**: Improved optimization techniques.
- **Multiplexing**: Parallel requests over the same TCP connection.
    - This means that the client can request multiple resources from the server simultaneously, eliminating the need for multiple connections and reducing latency.
- **Header Compression**: Reduced duplication and overhead.
    - reduces the overhead of sending redundant header data with each request and response.
    - This optimization saves bandwidth and speeds up the communication process.
- **Server Push**: Server can push data into client cache.
    - server can proactively send resources to the client before the client explicitly requests them.
    - eliminates the need for the client to make additional requests for critical resources, further reducing page load times.
    - A real-world example would be a web server pushing CSS and JavaScript files to the client along with the HTML, so the client has everything it needs to render the page without waiting for individual requests.

#### Request
```
GET / HTTP/2
Host: www.example.com
```

#### Response
```
:status: 200
content-type: text/html
content-length: 1234
```

## HTTP/3 - HTTP over QUIC - The Future of Web Communication
Based on QUIC (Quick UDP Internet Connections), HTTP/3 uses UDP for the transport layer, offering lower latency and improved performance:

**QUIC**: a transport layer protocol that provides reliable and secure communication over the internet. QUIC is a multiplexed protocol.

**vs HTTP/2**
HTTP/2 runs over a single TCP connection, so packet loss detection and retransmission handled at the TCP layer can block all streams. QUIC runs multiple streams over UDP and implements packet loss detection and retransmission independently for each stream, so that if an error occurs, only the stream with data in that packet is blocked.

- **Multiplexing**: Multiple streams over UDP.
- **Packet Loss Detection**: Independent retransmission for each stream.
    - HTTP/2 runs over a single TCP connection, so packet loss detection and retransmission handled at the TCP layer can block all streams.
    - QUIC runs multiple streams over UDP and implements packet loss detection and retransmission independently for each stream, so that if an error occurs, only the stream with data in that packet is blocked.
- **Built-in TLS**: Encrypted communication by default.

Example
#### Request
```
GET / HTTP/3
Host: www.example.com
```

#### Response
```
:status: 200
content-type: text/html
content-length: 1234
```
## Web Context: Impact on User Experience
HTTP versions significantly impact user experience:

- **HTTP/1.0**: Single requests causing delays.
- **HTTP/2**: Simultaneous resource requests, reducing load times.
- **HTTP/3**: Enhanced reliability and speed, especially in mobile environments.

#### Example Scenario
**HTTP/1.0**: Separate requests for each element causing slow load times.
**HTTP/2**: Multiple requests over a single connection speeding up load times.
**HTTP/3**: Improved performance and reduced latency on mobile devices.

## Mobile Web and HTTP Versions
HTTP/2 and HTTP/3 optimized for mobile networks, reducing latency and improving performance:

**HTTP/2**: Multiple requests over a single connection.
**HTTP/3**: Faster data transmission with QUIC.

#### Example
A social media platform switching from HTTP/1.1 to HTTP/2 improves loading times and user engagement. Further switching to HTTP/3 enhances performance even in areas with poor network coverage.

## Web Security and HTTP
Older HTTP versions had security vulnerabilities, leading to the adoption of HTTPS and TLS encryption:

**HTTP/1.0 and HTTP/1.1**: Lack of built-in encryption.
**HTTPS and TLS**: Secure communication.
**HTTP/2 and HTTP/3**: Enhanced security features like header compression and built-in TLS.

#### Real-World Examples
- A healthcare platform saw a decrease in XSS attacks after adopting HTTP/2.
- An online banking website reported a decline in CSRF incidents after implementing HTTP/3.

## Search Engine Ranking and HTTP Versions
The performance of your website and the version of HTTP it uses influence search engine rankings:

- **HTTP/1.0 and HTTP/1.1**: Slower performance can lead to lower rankings.
- **HTTP/2 and HTTP/3**: Faster performance improves rankings and user engagement.

#### Example
A travel blog switching to HTTP/2 sees improved loading times and higher search engine rankings.

## CDNs and HTTP/3 Adoption
CDNs improve website speed and reliability by delivering content from the nearest server:

- **HTTP/2 and HTTP/3**: CDNs use new features to deliver content more efficiently.

## Challenges in HTTP/3 Implementation
Implementing HTTP/3 involves overcoming technical challenges and ensuring compatibility:

- **Technical Challenges**: Learning the new protocol and debugging issues.
- **Best Practices**: Thorough testing and open communication with CDN providers.

## The Future of Web Protocols
Continuous advancements in web protocols promise faster and more secure communication:

- **HTTP/4**: Potential for further improvements in content delivery.
- **WebRTC and QUIC**: Emerging technologies enhancing real-time communication.

## Conclusion
The evolution of HTTP from HTTP/0.9 to HTTP/3 has significantly impacted web performance and user experience. Continuous improvement in web protocols is vital for a faster, more secure, and enjoyable internet. Embracing these advancements ensures a smooth online experience for users worldwide.

# Resources

https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Evolution_of_HTTP#http3_-_http_over_quic

https://medium.com/@nirajranasinghe/the-evolution-of-http-from-version-1-0-to-3-0-and-the-impact-on-modern-web-communication-cb233b17e118

https://medium.com/platform-engineer/evolution-of-http-69cfe6531ba0