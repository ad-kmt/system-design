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

#### Minor
- **Quality of Service or UX**: Ensures fair resource distribution among users.
- **Monetization**: Allows free-tier users limited API access and encourages them to upgrade.
- **Operational Cost Control**: Avoids unnecessary auto-scaling or excessive Pay-As-You-Go charges.

## Requirements Clarification Questions



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