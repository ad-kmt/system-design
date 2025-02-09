# Resources
[Rate Limiting system design | TOKEN BUCKET, Leaky Bucket, Sliding Logs](https://www.youtube.com/watch?v=mhUQe4BKZXs&t=1019s)

# Concepts
- Rate limiting algorithms
- Load balancer
- Load balancing algorithms
- In memory databases (Redis etc.)
- Distributed System
- API Gateway

## Why Do We Need Rate Limiting?
Rate limiting prevents overuse or abuse of APIs by controlling how often a user or system can make requests. It is essential for:

#### Major
- **Prevents Denial of Service (DoS) Attacks**: intentional (bots or abusive users) or unintenional, by blocking excess calls.
- **Security**: Prevents brute-force attacks on login endpoints or promo code abuse.

#### Additional
- **Quality of Service or UX**: Ensures fair resource distribution among users.
- **Monetization**: Allows free-tier users limited API access and encourages them to upgrade.
- **Operational Cost Control**: Avoids unnecessary auto-scaling or excessive Pay-As-You-Go charges.

## Requirements Clarification Questions

### Basic Functionality
Should we apply rate limits per user, IP, API key, or service?

Should we support global rate limits (across multiple services) or just per service?

Should we enforce rate limits per second, per minute, per hour, or per day?

### Allowed vs. Blocked Behavior

What should happen when a request exceeds the limit? (Throttle, reject, or queue it?)

### Where to Apply Rate Limiting?

Should rate limiting be enforced at the API Gateway, Load Balancer, or Backend Service?

Should it work in distributed systems with multiple replicas of services? Should the rate limiter work across microservices or only for a single service?

### Users & Traffic Pattern

What are the expected QPS (queries per second) and peak traffic?

How many unique users or IPs do we expect per second/minute/hour?

Should we handle authenticated vs. unauthenticated users differently?

### Rate Limiting Strategy

Do we need fixed window, sliding window, token bucket, or leaky bucket?

Should we allow grace periods or provide a quota-based system?

### Handling Failures

What should happen if the rate limiter backend (e.g., Redis, DB) goes down?

Should we fail-open (allow traffic) or fail-closed (block traffic)?

Do we need circuit breakers or fallback mechanisms?

## Types of Rate Limiting
Rate limiting can be applied at different levels:
- **User-based Rate Limiting**: Limits API requests per user in a given time frame.
- **Concurrent Rate Limiting**: Restricts the number of parallel requests a user can make (mitigates DDoS attacks).
- **IP-based Rate Limiting**: Limits requests based on the originating IP address.
- **Location-based Rate Limiting**: Restricts access based on geography (e.g., prioritizing a specific location for an event).
- **Server-based Rate Limiting** : Limits API usage for specific servers providing different services

## Rate Limiting Algorithms
- Token bucket
- Leaky bucket
- Fixed window counter
- Sliding window logs
- Sliding window counter

# Next
- Distributed Denial of Service Attacks (DDoS)
- External rate limit providers
- Challenge mechanisms (CAPTCHAs, Proof-of-Work, etc.):