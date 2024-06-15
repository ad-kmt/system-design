# TODO

1. Requires streamlining of content.
2. Removal of duplicate content

# gRPC: An Introduction and In-depth Exploration

## What is gRPC and Why Was It Introduced?

- gRPC is a framework for implementing RPC APIs via HTTP/2.
- gRPC facilitates service-to-service communication in distributed environments. (e.g. microservices)
- gRPC is language-agnostic
- gRPC supports multiple streaming modes through HTTP/2 and strongly typed service contracts using Protocol Buffers (Protobuf).

## Who developed gRPC

It was developed and open-sourced by Google in 2015 as the next generation of their existing RPC infrastructure, called “Stubby.”

## History of gRPC

Traditionally, there have been two distinct ways to build APIs: **RPC and REST**. There’s also **SOAP**, an ancient protocol that is mostly used in strictly standardized operations like banking and aviation. You will also hear about **GraphQL**, gRPC’s peer in terms of age. Let’s go through them one by one.

#### RPC:

The “RPC” in gRPC stands for “Remote Procedure Call.” RPC was first introduced in the late 1970s and 1980s, and it allows clients and servers to interact with one another as if they were both on the same machine.

It uses procedure calls to request a service from a remote server the same way you would request a local system -- via direct actions to the server (like `SendUserMessages`, `LocateVehicle`, `addEntry`). 

RPC is an efficient way to build APIs.

RPC messages are lightweight and the interactions are straightforward.

**Problem with RPC**

- Interoperability: Different RPC implementations written in different programming languages may not interoperate well
- Tight Coupling: RPC APIs are tightly coupled with the underlying systems.
- Complexity in Integration: requires specific client libraries

#### REST:
REST (Representational State Transfer) was introduced in 2000,  it was meant to solve these problem and make APIs more accessible.

- Uniform Interface: REST provided a uniform way to access data indirectly, via resources, using generic HTTP methods such as GET, POST, PUT, DELETE, and so on.
- REST APIs are basically self-descriptive

This was the main difference between RPC and REST

**Problems with REST**

- High Latency and Performance overhead
	- Lot of Metadata
	- JSON for data interchange, which is text-based and larger in size
	- Under-fetching and over-fetching
- Only request/response architecture. Lack of Efficient Streaming Support

These are the reasons two new approaches emerged later: Facebook’s GraphQL and gRPC from Google.

#### gRPC

gRPC offers a refreshed take on the old RPC design method by making it interoperable, modern, and efficient using technologies such as Protocol Buffers and HTTP/2.

gRPC owes its success to the employment of two techniques: using HTTP/2 instead of HTTP/1.1 and protocol buffers as an alternative to XML and JSON. Most of the gRPC benefits stem from using these technologies.

The following benefits make it a solid candidate for replacing REST in some operations.

- Low Latency and High Performance
	- Lightweight messages: gRPC uses Protocol Buffers (Protobuf), a binary format that is smaller and faster to parse ( 30 percent smaller in size than JSON messages.)
	- High performance: gRPC is 5, 7, and even 8 times faster than REST+JSON communication.
	- Built-in code generation: gRPC has automated code generation in different programming languages
- More connection options:
	- server-side streaming, client-side streaming, and bidirectional streaming.


## gRPC Main Concepts

### Protocol Buffers

gRPC uses Protocol Buffers (Protobuf) as its interface definition language (IDL), which is one of its primary enhancements of RPC. Protobuf is a flexible and efficient method for serializing structured data into a binary format. Data that is encoded in a binary form is more space-efficient and faster to serialize and deserialize than text-based formats like JSON or XML.

#### Benefits of Protobuf

- **Efficient Parsing**: Less CPU-intensive and faster message exchange (serialization and deserialization) due to binary format.
- **Reduced Development overhead**:  its ability to generate code reduces development overhead and makes it easier to work with serialized data in various programming languages.
- **Schema Enforcement**: promotes strong typing, which ensures data consistency and reduces the risk of error.

### HTTP/2 as the Transport Protocol

gRPC introduces many upgrades to the old RPC structure by using HTTP/2.

#### Benefits of HTTP/2

- **Binary Framing Layer**: HTTP/2 communication is divided into smaller messages and framed in binary format. Unlike text-based HTTP/1.1, it makes sending and receiving messages compact and efficient.
- **Multiple Parallel Requests**: While HTTP/1.1 allows for processing just one request at a time, HTTP/2 supports multiple calls via the same channel. More than that, communication is bidirectional -- a single connection can send both requests and responses at the same time.
- **Streaming**: Real-time communication is not only possible with HTTP/2, but also has high performance thanks to binary framing -- each stream is divided into frames that can be prioritized and run via a single TCP connection, thus reducing the network utilization and processing load.

#### Challenges with HTTP/2

- Being fairly new, it’s currently supported only by 50.5 percent of all the websites. This is one of the reasons why gRPC is mostly featured on the backend,

![](https://www.altexsoft.com/static/blog-post/2023/11/e9c78edf-7a19-4159-8361-2329d56409fb.webp)

## How Does gRPC Work?
gRPC enables distributed, polyglot services to communicate efficiently over a network.

![](https://blog.postman.com/wp-content/uploads/2023/11/What-is-gRPC.png)


### Step 1: Defining Service Contracts and Data Structures

A service contract in gRPC defines the methods and message types for communication between clients and servers using Protocol Buffers (Protobuf) in a .proto file.

1. **Protobuf (.proto) Files**: In a .proto text file, a programmer defines a schema -- how they want data to be structured. They define service methods, message types, and API structure in Protobuf files.
2. **Protocol Buffers Compiler (protoc)**: This compiler generates client and server code in multiple programming languages.
3. **Generated Code**: The code that is generated by protoc includes classes or modules that abstract away much of the complexity of making gRPC calls
   - **Client Side**:  the generated code typically includes method stubs that correspond to the RPC methods that are defined in the .proto file. These stubs handle serializing data, making the gRPC call over the network, and deserializing the response.
   - **Server side**: the generated code provides a base class that developers can implement to define the service’s behavior. Developers can also override these methods to create custom server logic.

### Communication Patterns

1. **Unary RPC**: Client sends a single request and waits for a single response.
2. **Server Streaming RPC**: Client sends a single request and receives a stream of responses.
3. **Client Streaming RPC**: Client sends a stream of requests and waits for a single response.
4. **Bidirectional Streaming RPC**: Both client and server send streams of messages concurrently.

## Benefits of gRPC

### Lightweight Messages

- gRPC messages can be up to 30% smaller than JSON messages, making data transfer more efficient.

### High Performance

- Evaluations show gRPC to be 5 to 8 times faster than REST+JSON communication.

### Built-in Code Generation

- Supports multiple languages including Java, C++, Python, Go, Dart, Objective-C, and Ruby.

### More Connection Options

- Supports server-side streaming, client-side streaming, and bidirectional streaming, unlike REST’s request-response architecture.



## Weaknesses of gRPC

### Lack of Maturity

- Fewer resources and developer support compared to older technologies like REST and GraphQL.

### Limited Browser Support

- Modern browsers cannot access HTTP/2 frames directly, requiring a gRPC proxy.

![](https://www.altexsoft.com/media/2021/03/grpc-web-991x1024.png)

### Non-Human-Readable Format

- Protobuf Binary format requires extra tools for debugging and analysis.

### Steeper Learning Curve

- Requires understanding Protobuf, HTTP/2, strong typing, and code generation.

## When to Use gRPC

- **Real-Time Communication Services**: Suitable for streaming calls.
- **Efficient Communication**: When performance is a critical factor.
- **Multi-Language Environments**: Supports various programming languages.
- **Internal APIs**: Avoids forcing technology choices on clients.

## gRPC in Microservices

gRPC is ideal for microservice architectures due to its performance and polyglot nature.

It allows different technologies for each service, ensuring interoperability through binary service contracts.

It supports multiple concurrent messages, making it suitable for internal microservice-to-microservice communication.

![](https://www.altexsoft.com/static/blog-post/2023/11/bc9ad786-7b04-4617-9200-bd84e26b89d1.webp)

## gRPC vs. REST

### gRPC

- **Communication Model**: Calls functions on the server as if they were local.
- **Data Format**: Uses Protobuf for binary serialization.
- **Use Case**: High-performance microservices with real-time, bidirectional data transfer.

### REST

- **Communication Model**: Uses HTTP methods to request resources.
- **Data Format**: Typically uses JSON.
- **Use Case**: Web applications with standardized interfaces.

## Challenges of gRPC

- **Complex Protobuf Definitions**: More challenging than JSON.
- **Steep Learning Curve**: Requires understanding multiple new concepts.
- **Difficult Debugging**: Binary serialization is not human-readable.
- **Less Mature Ecosystem**: Fewer libraries and tools compared to older technologies.

## Tools and Resources

- **Official Guides**: gRPC guide and Protocol Buffers guide.
- **Community**: Gitter chat, subreddit, Google Group, StackOverflow, and Quora.
- **Tools**: gRPC Ecosystem on GitHub.
- **Online Classes**: Microservices with gRPC and gRPC Master Class on Udemy.

# Resources

https://www.altexsoft.com/blog/what-is-grpc/
https://blog.postman.com/what-is-grpc/

## What Next?

### Related Topics

- REST API Design
- SOAP vs. REST vs. gRPC

### Deeper Understanding

- Advanced Protobuf Techniques
- HTTP/2 Detailed Study
- Real-World gRPC Use Cases
- gRPC Security Best Practices

