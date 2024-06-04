# Content Delivery Network (CDN)

## What is a CDN?

A Content Delivery Network (CDN) is a globally distributed network of proxy servers designed to serve content from locations closer to the user.

CDNs typically deliver static files such as HTML, CSS, JavaScript, images, and videos. Some CDNs, like Amazon CloudFront, also support dynamic content delivery.

The site's DNS resolution informs clients about which CDN server to contact.

## Why Use a CDN?

Serving content from CDNs can significantly improve performance by:

1. **Reduced Latency**: Delivering content from data centers closer to users.
2. **Improved performance**: Reducing the load on your servers, as the CDN handles many requests. Application server can better allocate resources to process more complex, dynamic requests.
3. **Reliability**:  CDNs often have multiple data centers distributed globally. If one data center experiences issues, traffic can be rerouted to another nearby data center.
4. **Scalability**: During traffic spikes, the CDN can handle the increased number of requests by distributing the load across multiple CDN servers, without overloading the origin server, ensuring consistent performance.

## Types of CDNs

### Push CDNs

#### What is a Push CDN?
Push CDNs receive new content whenever changes occur on your server. You are responsible for uploading content directly to the CDN and updating URLs to point to the CDN. 

#### When to Use Push CDNs?
Push CDNs are ideal for:
- Sites with a small amount of traffic.
- Sites with content that doesn't change frequently.

#### Advantages of Push CDNs
- Content is uploaded only when it is new or changed, minimizing traffic.
- Maximizes storage by keeping content until it expires or is updated.

### Pull CDNs

#### What is a Pull CDN?
Pull CDNs retrieve new content from your server when the first user requests it. The content remains on your server, and URLs are rewritten to point to the CDN. The initial request may be slower until the content is cached on the CDN.

#### When to Use Pull CDNs?
Pull CDNs are suitable for:
- Sites with heavy traffic.
- Scenarios where only recently-requested content remains cached on the CDN.

#### Advantages of Pull CDNs
- Minimizes storage space on the CDN.
- Distributes traffic evenly across servers.

## Disadvantages of CDNs

- **Cost**: CDN costs can be significant depending on traffic, but these should be weighed against the costs of not using a CDN.
- **Stale Content**: Content might be stale if it is updated before the TTL (time-to-live) expires.
- **URL Changes**: CDNs require changing URLs for static content to point to the CDN.

## Conclusion

Using a CDN can greatly enhance the performance and scalability of your website by distributing content delivery and reducing server load. However, it's important to choose the right type of CDN and consider potential drawbacks such as cost and content staleness.

## What Next?

### Related Topics
- **Edge Computing**: Understanding how edge computing complements CDNs.
- **Load Balancing**: Techniques to distribute traffic across servers effectively.

### Topics for Deeper Understanding
- **Dynamic Content Delivery with CDNs**: Exploring how CDNs handle dynamic content.
- **Security in CDNs**: Measures CDNs take to secure content delivery.
- **CDN Configuration Best Practices**: Tips for optimizing CDN performance and management.
