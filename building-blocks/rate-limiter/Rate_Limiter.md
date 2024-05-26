# Rate Limiter

## What is a Rate Limiter?

A rate limiter, as the name suggests, puts a limit on the number of requests a service fulfills. It throttles requests that cross the predefined limit. For example, a client using a particular service’s API that is configured to allow 500 requests per minute would block further incoming requests for the client if the number of requests the client makes exceeds that limit.

![](https://user-images.githubusercontent.com/23625821/132120396-f3dd7e42-df2d-4c44-bf7b-3bdbfde5cbdf.png)

## Why Do We Need a Rate Limiter?

A rate limiter is generally used as a defensive layer for services to avoid their excessive usage, whether intended or unintended. It also protects services against abusive behaviors that target the application layer, such as denial-of-service (DOS) attacks and brute-force password attempts.

### Scenarios Where Rate Limiters Can Be Used

1. **Preventing Resource Starvation:**
   Some denial of service incidents are caused by errors in software or configurations in the system, which causes resource starvation. Such attacks are referred to as friendly-fire denial of service. One of the common use cases of rate limiters is to avoid resource starvation caused by such denial of service attacks, whether intentional or unintentional.

2. **Managing Policies and Quotas:**
   There is also a need for rate limiters to provide a fair and reasonable use of resources’ capacity when they are shared among many users. The policy refers to applying limits on the time duration or quantity allocated (quota).

3. **Controlling Data Flow:**
   Rate limiters could also be used in systems where there is a need to process a large amount of data. Rate limiters control the flow of data to distribute the work evenly among different machines, avoiding the burden on a single machine.

4. **Avoiding Excess Costs:**
   Rate limiting can also be used to control the cost of operations. For example, organizations can use rate limiting to prevent experiments from running out of control and avoid large bills. Some cloud service providers also use this concept by providing freemium services to certain limits, which can be increased on request by charging from users.

## Related Topics

- **Load Balancing:** Understanding how rate limiting can work in conjunction with load balancing to distribute requests efficiently.
- **API Gateway:** Exploring how API gateways implement rate limiting to manage traffic.
- **Denial-of-Service (DoS) Protection:** Methods and strategies to protect against DoS attacks.
- **Quota Management:** Techniques for managing and enforcing usage quotas in software applications.

## Deeper Understanding

- **Rate Limiting Algorithms:** An in-depth look at various algorithms used for rate limiting such as token bucket, leaky bucket, fixed window, and sliding window log.
- **Implementing Rate Limiting in Different Environments:** Practical examples of how to implement rate limiting in different programming environments and cloud services.
- **Monitoring and Logging:** Best practices for monitoring and logging rate-limited requests to ensure optimal performance and security.
