# Client-Server Architecture in System Design

[![](https://www.interviewbit.com/blog/wp-content/uploads/2022/06/Client-and-Server-768x321.png)](https://www.interviewbit.com/blog/client-server-architecture/)

## Understanding Client and Server

### What is a Client?
A client is any computer that requests something from the server. For example, when visiting a website, the browser requests the webpage from the server hosting the domain. In this scenario, the browser acts as a client.

### What is a Server?
A server is a computer designed to serve requests from clients. Continuing with the same example, the server responds to the client's request by sending the webpage.

## What is Client-Server Architecture?

The client-server architecture, or model, is a network architecture that separates tasks between clients and servers. These tasks can be within the same system or across a network. To access the services provided by the server, a client sends a request to the server, which then processes the request and shares the resources.

Client-server communication follows a request-response pattern and adheres to standard communication protocols like TCP. The TCP protocol manages the distribution of data in packets, which are then transferred over networks, ensuring flow control and retransmission of lost packets.

## How Does Client-Server Architecture Work?

In a client-server architecture:
1. The client requests the server's IP address from the DNS (Domain Name System).
2. The DNS responds with the IP address.
3. The client sends a request to the server at this IP address, specifying the port number for the required application.
4. The server processes the request and responds.
5. The client receives the response, and the relevant application processes the response based on the port number.

![](https://www.interviewbit.com/blog/wp-content/uploads/2022/06/Client-Server-Architecture-working-768x600.png)

## Types of Client-Server Architecture

### 1-Tier Architecture
In a 1-tier architecture, everything related to the application (user interface, business logic, database logic, and database) is grouped and used as a single package. This architecture offers reliability but is complex to manage due to data variance and duplicated work. It typically stores data within local systems or on shared drives.

### 2-Tier Architecture
In a 2-tier architecture, the application logic is divided into two layers:
- The database, which acts as a separate entity.
- The main application, which contains the user interface, business logic, and database logic.

This architecture offers a better environment than the 1-tier architecture and is faster since there is no intermediary between the client and the server. An example of this architecture is an online reservation system.

![](https://www.interviewbit.com/blog/wp-content/uploads/2022/06/2-Tier-Architecture-1-768x417.png)

### 3-Tier Architecture
In a 3-tier architecture, there is middleware between the client and the server. When a client requests information, the request is first received by the middleware, which then sends it to the server. The server's response follows the same path back to the client.

This architecture consists of three layers:
- Presentation layer: Controlled by client devices.
- Application layer: Managed by middleware.
- Database layer: Handled by the server.

The additional layer enhances security, ensures data integrity, and provides invisible database structures.

![](https://www.interviewbit.com/blog/wp-content/uploads/2022/06/3-Tier-Architecture-1-768x207.png)

## Advantages of Client-Server Architecture

- **Management**: Easy to manage since files are stored on one server.
- **Accessibility**: Clients can access the system from any location or platform.
- **Scalability**: The architecture is highly scalable, allowing the addition of more clients and servers.
- **Centralized Control**: Centralized management and administration facilitate easy updates and troubleshooting.
- **Security**: Centralized architecture enhances data protection and simplifies backup processes.

## Disadvantages of Client-Server Architecture

- **Less Robust**: Centralized nature means network interruptions if the main server fails.
- **Maintenance**: Requires regular maintenance and prompt fixing of issues.
- **Cost**: High setup and maintenance costs due to powerful network operations.
- **Network Congestion**: Overloaded servers can lead to crashes or slow connectivity.

## Conclusion
Client-server architecture facilitates the updating of shared databases by multiple users through a graphical user interface. This architecture is widely used by businesses to grow, digitalize, market products, and stay updated with industry news and events.

## What Next?

### Related Topics
- **Peer-to-Peer Architecture**
- **Microservices Architecture**

### Topics for Deeper Understanding
- **Network Protocols**
- **Middleware in System Design**
- **Security Measures in Client-Server Architecture**

# Resources

https://www.interviewbit.com/blog/client-server-architecture/