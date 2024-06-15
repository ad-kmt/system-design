# RESTful API Notes

### What is an API?

An Application Programming Interface (API) defines the rules for communication between software systems. Developers expose APIs so that other applications can communicate with their applications programmatically.

### Clients and Resources

- **Clients**: Users or software systems that access information from the web through the API.
- **Resources**: Information provided by applications to their clients, such as images, videos, text, or numbers.

## What is REST?

Representational State Transfer (REST) is a software architecture that imposes conditions on how an API should work. REST APIs follow the REST architectural style, making them secure, high-performing and reliable.

### Principles of REST

To make an API service RESTful, six guiding constraints must be satisfied:

1. **Uniform Interface**: The uniform interface is fundamental to the design of any RESTful webservice. It indicates that the server transfers information in a standard format. The formatted resource is called a representation in REST.
   - **Requests should identify resources**: Uses Uniform Resource Identifier (URI).
   - **Manipulation of Resources**: Clients have enough information in the resource representation to modify or delete the resource if they want to. The server meets this condition by sending metadata that describes the resource further.
   - **Self-descriptive Messages**: Clients receive information about how to process the representation further. The server achieves this by sending self-descriptive messages that contain metadata about how the client can best use them.
   - **Hypermedia as the Engine of Application State (HATEOAS)**: Clients receive information about all other related resources they need to complete a task. The server achieves this by sending hyperlinks in the representation so that clients can dynamically discover more resources.

2. **Statelessness**: Server completes every client request independently of all previous requests. Clients can request resources in any order, and every request is stateless or isolated from other requests.
3. **Layered System**: Supports a hierarchical architecture with multiple layers. You can design your RESTful web service to run on several servers with multiple layers such as security, application, and business logic, working together to fulfill client requests. These layers remain invisible to the client.
4. **RESTful resource caching**: Data within a response to a request must be labeled as cacheable or non-cacheable. RESTful web services support caching, which is the process of storing some responses on the client or on an intermediary to improve server response time
5. **Code on Demand**: In REST architectural style, servers can extend or customize client functionality by transferring software programming code to the client.

## Benefits of RESTful APIs

- **Scalability**:
	- Efficient client-server interactions
	-  Statelessness removes server load because the server does not have to retain past client request information.
	- Caching partially or completely eliminates some client-server interactions.
- **Flexibility**:
	- Total client-server separation
	-  They simplify and decouple various server components so that each part can evolve independently.
	- Platform or technology changes at the server application do not affect the client application.
- **Independence**:
	- REST APIs are independent of the technology used.
	- REST APIs can be written in various programming languages without affecting API design.

## How do RESTful APIs work?

A. Client Request
B. Server authenticates and processes request
C. Server Response

### A. Client Request

The client sends a request to the server. The client follows the API documentation to format the request in a way that the server understands.

#### What does the RESTful API client request contain?

**1. Unique Resource Identifier (URI)**:
- The server identifies each resource with unique resource identifiers.
- For REST services, the server typically performs resource identification by using a **Uniform Resource Locator (URL)**.
- The URL specifies the path to the resource.
- A URL is similar to the website address that you enter into your browser to visit any webpage.
- The URL is also called the **request endpoint** and clearly specifies to the server what the client requires.

**2. Method**: Developers implement RESTful APIs by using the Hypertext Transfer Protocol (HTTP). An HTTP method tells the server what it needs to do to the resource. The following are four common HTTP methods:

- **GET**:
	- Clients use GET to access resources that are located at the specified URL on the server.
	- Clients can send parameters in the RESTful API request to instruct the server to filter data before sending.
	- Clients can cache GET requests.

- **POST**:
	- Clients use POST to send data to the server. This includes the data representation with the request.
	- Sending the same POST request multiple times has the side effect of creating the same resource multiple times.

- **PUT**:
	- Clients use PUT to update existing resources on the server.
	- Unlike POST, sending the same PUT request multiple times in a RESTful web service gives the same result.

- **DELETE**:
	- Clients use the DELETE request to remove the resource.
	- A DELETE request can change the server state. However, if the user does not have appropriate authentication, the request fails.

**3. Headers (metadata)**:
Request headers are the metadata exchanged between the client and server.
For instance, the request header indicates the format of the request and response, provides information about request status, and so on.

**4. Data (if required)**
REST API requests might include data for the POST, PUT, and other HTTP methods to work successfully.

**5. Parameters**:
RESTful API requests can include parameters that give the server more details about what needs to be done. 

The following are some different types of parameters:

- **Path** parameters that specify URL details.
- **Query** parameters that request more information about the resource.
- **Cookie** parameters that authenticate clients quickly.

### B. Request Authentication

A RESTful web service must authenticate requests before it can send a response. Authentication is the process of verifying an identity.

#### RESTful API Authentication Methods

1. **HTTP Authentication**:
   - **Basic Authentication**: Client sends the user name and password in the request header. Client encodes them with base64
   - **Bearer Authentication**: The bearer token is typically an encrypted string of characters that the server generates in response to a login request. The client sends the token in the request headers to access resources.

2. **API Keys**:
	- The server assigns a unique generated value to a first-time client. Whenever the client tries to access resources, it uses the unique API key to verify itself.
	- API keys are less secure because the client has to transmit the key, which makes it vulnerable to network theft.

3. **OAuth**:
	- OAuth combines passwords and tokens for highly secure login access to any system.
	- The server first requests a password and then asks for an additional token to complete the authorization process.
	- It can check the token at any time and also over time with a specific scope and longevity.

### C. Server Response
The server returns a response to the client. The response contains information that tells the client whether the request was successful. The response also includes any information that the client requested.

#### What does the RESTful API server response contain?

1. **Status Line**: The status line contains a three-digit status code that communicates request success or failure. For instance, 2XX codes indicate success, but 4XX and 5XX codes indicate errors. 3XX codes indicate URL redirection.
	- **200**: Generic success response.
	- **201**: POST method success response
	- **400**: Incorrect request that the server cannot process
	- **404**: Resource not found

2. **Message Body**: The response body contains the resource representation.
	- The server selects an appropriate representation format based on what the request headers contain.
	- Clients can request information in XML or JSON formats, which define how the data is written in plain text.
	- For example, if the client requests the name and age of a person named John, the server returns a JSON representation as follows: '{"name":"John", "age":30}'

3. **Headers**: The response also contains headers or metadata about the response. 
	- They give more context about the response and include information such as the server, encoding, date, and content type.


## History of REST APIs

Before the advent of REST, developers commonly used SOAP (Simple Object Access Protocol) for API integration.

**SOAP Working**: To make a call, developers handwrote an **XML document** with a **Remote Procedure Call** in the body. They then specified the endpoint and would POST their SOAP envelope to the endpoint.

**Problem with SOAP:** SOAP was complex to build, use, and debug.

**Inception of REST**: In response to these challenges, Roy Fielding and a group of developers created REST in 2000, setting the stage for a simpler and more efficient API architecture. REST's universal rules make it easier for developers to integrate software.

### Timeline of REST API Development

- **Before 2000**: Developers used SOAP, requiring handwritten XML documents with Remote Procedure Calls (RPC) in the body. Integration involved specifying endpoints and posting SOAP envelopes.
- **2000**: Roy Fielding and his team introduced REST, defining constraints for a standard that allowed any server to communicate with any other server.
- **2002**: eBay launched its REST API, allowing broader market access via its API, inspiring other e-commerce giants like Amazon to follow suit.
- **2004-2006**: Flickr introduced its RESTful API in 2004, facilitating easy embedding of images into blogs and social media. Facebook and Twitter released their APIs in 2006, responding to developer demand for data scraping and integration.
- **2006-Present**: RESTful APIs have become the norm, enabling enhanced functionality in websites and applications. Tools like Postman have simplified API building and collaboration, further popularizing REST APIs.

REST APIs have revolutionized how developers integrate systems, providing a flexible, scalable, and efficient framework for building modern applications.


## REST vs. SOAP APIs

- **SOAP**: Protocol with strict message formats using XML.
- **REST**: Architectural style using HTTP, URLs, and flexible data formats like JSON/XML etc.

## Uses of REST APIs

- **Cloud Applications**: Stateless calls for smooth redeployment and scaling.
- **Web Use**: Accessible from various client-side technologies.
- **Flexibility**: Can be used in different environments without worrying about the client-side stack.

## Challenges of Using REST APIs

- **Endpoint Consensus**: Consistency in URL formatting is crucial.
- **API Versioning**: Managing multiple API versions to prevent compatibility issues.
- **Authentication**: Varies depending on the context and can be complex.
- **Security**: Implementing proper security measures to protect APIs.

## REST API Best Practices

- **Use HTTP Status Codes Correctly**: Align status codes with request outcomes.
- **Provide Informative Error Messages**: Help consumers understand and fix issues.
- **Secure Your API**: Implement measures like input sanitization and role-based access control.
- **Version Your API**: Manage changes and maintain compatibility.
- **Document Your API**: Provide comprehensive documentation.
- **Allow Filtering, Sorting, and Pagination**: Improve performance and prevent system overload.
- **Use Nouns Instead of Verbs in Endpoints**: Keep endpoint paths concise and meaningful.

# Resources
https://aws.amazon.com/what-is/restful-api/
https://blog.postman.com/rest-api-examples/

## Related Topics

- **GraphQL APIs**: Understanding how GraphQL differs from REST.
- **SOAP APIs**: Deep dive into SOAP and its use cases.
- **API Security**: Best practices for securing APIs.

## Topics for Deeper Understanding

- **Advanced RESTful API Design**: Best practices and advanced concepts.
- **API Versioning Strategies**: Techniques for managing API versions.
- **OAuth in Depth**: Detailed explanation and implementation of OAuth.
- **Rate Limiting and Throttling**: Protecting APIs from abuse.
- **Hypermedia in REST APIs**: Implementing HATEOAS effectively.
