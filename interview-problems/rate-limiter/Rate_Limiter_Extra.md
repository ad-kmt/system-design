# Rate limiting at different layers of the OSI Model 30%

## Application Layer (Layer 7) – API & Web Server Rate Limiting

**Where?** API gateways, web servers (Nginx, Apache), WAF (Web Application Firewall)
**How?** Request-based limiting (e.g., limit 1000 requests per hour per user)

**Techniques:**
- API Key-based limits (e.g., Stripe, AWS APIs)
- User Session or JWT-based limiting
- URL/Endpoint-specific rate limiting
- Rate limiting plugins in Nginx, Apache, or Cloudflare

✅ **Use case**: Prevent API overuse, bot traffic, and web scraping.

##  Transport Layer (Layer 4) – TCP & UDP Rate Limiting
**Where?** Load balancers, firewalls, proxies (e.g., HAProxy, iptables)
**How?** Limit TCP connections per IP or regulate UDP packet rate.

**Techniques:**
TCP SYN flood protection (e.g., Linux sysctl settings)
WebSocket connection limits
UDP request throttling (used in gaming & VoIP)

✅ **Use case:** Prevent too many concurrent TCP connections or UDP packet floods.

##  Network Layer (Layer 3) – IP-Based Rate Limiting
**Where?** Firewalls, routers, cloud network security (AWS Security Groups, Google Cloud Firewall)
**How?** Drop packets or throttle based on source IP.

**Techniques:**
- IP-based rate limiting (e.g., allow only 100 requests/sec per IP)
- DDoS mitigation using edge firewalls (Cloudflare, AWS Shield)
- Ingress/Egress bandwidth throttling

✅ **Use case:** Block abusive IPs, mitigate volumetric DDoS attacks.

## Data Link Layer (Layer 2) – Switch-Level Rate Limiting
**Where?** Network switches, ISP throttling, MAC filtering
**How?** Restrict packet rate per MAC address or enforce bandwidth limits.

**Techniques:**

- Switch port rate limiting (e.g., Cisco QoS settings)
- MAC address filtering (control excessive packet rates)
- ISP traffic shaping (e.g., limit torrent speeds)

✅ **Use case:** Prevent local network congestion, ISP throttling heavy users.

# Strategies to Handle Exceeding Rate Limits

## 1. Reject the Request
The request is immediately denied with an `HTTP 429 Too Many Requests` response.
The client gets a "Retry-After" header indicating when they can retry.

**Example**

    HTTP/1.1 429 Too Many Requests
    Retry-After: 30  # Wait 30 seconds before retrying

### ✅ Pros:
- Simple and fast.
- Prevents backend overload.
- Encourages proper API usage.

### ❌ Cons:
- Users may experience service disruptions.
- Clients may retry aggressively, causing unnecessary load.

### Use Case
Best for stateless APIs where exceeding the limit should result in an error (e.g., public APIs, payment APIs).

## 2. Throttle the Request
Instead of rejecting the request, response time is artificially delayed to slow down the client.
Can be implemented using exponential backoff (delaying responses progressively).

**Example:**
First request exceeded → Wait 500ms
Next request → Wait 1000ms
Next request → Wait 2000ms

### ✅ Pros:
- Helps manage bursty traffic without outright rejection.
- Improves user experience by still allowing some requests.
- Useful when clients expect eventual responses.

### ❌ Cons:
- Can introduce latency.
- May not work well for real-time services.

### Use Case:
Best for analytics APIs, or background jobs where some delays are acceptable.

### 3. Queue the Request
Instead of rejecting or delaying, requests are queued for later processing.
The system processes them when capacity is available.
Works well with message queues like Kafka, RabbitMQ, or SQS.

**Example:**
A request enters the queue and is processed after X seconds.
The client may receive a `202 Accepted` response instead of a 429.

    HTTP/1.1 202 Accepted
    Location: /check-status/12345  # Client can poll for results

### ✅ Pros:
- Ensures all requests eventually get processed.
- Avoids overwhelming the backend while still serving users.

### ❌ Cons:
- Not suitable for real-time requests (e.g., authentication, payments).
- Requires extra infrastructure (message queues, job workers).

### Use Case:
Best for batch processing, data ingestion pipelines, and async APIs (e.g., background tasks, reporting jobs).

# Stackoverflow Questions
[Sequence in which rate limiter, load balancer, api gateway and reverse proxy should be placed](https://stackoverflow.com/questions/78440167/sequence-in-which-rate-limiter-load-balancer-api-gateway-and-reverse-proxy-sho "Sequence in which rate limiter, load balancer, api gateway and reverse proxy should be placed")

# Where to Enforce Rate Limiting? (API Gateway, Load Balancer, or Backend Service)
Rate limiting can be enforced at different levels of a system’s architecture:

- API Gateway
- Load Balancer
- Backend Service

Each has its own advantages, disadvantages, and trade-offs. Let's break them down.

## 1️⃣ API Gateway Level Rate Limiting
✅ Best for: Global API limits across multiple backend services

Enforced at the reverse proxy or API Gateway (e.g., Nginx, Envoy, Kong, AWS API Gateway) before reaching backend services.
Uses a distributed store (like Redis) to maintain counters across instances.

### ⚙️ How it Works
1. A client sends a request → API Gateway checks the rate limit.
2. If the request exceeds the limit, it is rejected with HTTP 429 (Too Many Requests).
3. If within the limit, it is forwarded to the backend.
4. API Gateway updates rate limit counters in Redis or a distributed store.

### ✅ Pros
✔ Global Rate Limiting → Limits requests across all backend services.

✔ Prevents Backend Overload → Blocks excessive requests before reaching backend.

✔ Centralized Control → All services follow the same rate limiting rules.

✔ Scalable → Can be distributed using Redis or a cloud-based service.

✔ Supports Multiple Rate Limit Policies → Per user, API key, IP, region, etc.

### ❌ Cons
✘ Latency Overhead → API Gateway must check Redis (adds ~1-5ms delay).

✘ Single Point of Failure → If Redis is down, rate limiting fails (use circuit breakers).

✘ Less Granular Control → Cannot enforce per-service rate limits efficiently.

### 🚀 Best Use Cases
✅ Public APIs (Google Maps, Stripe, AWS APIs).

✅ Microservices where global rate limits are required.

✅ Protecting against API scraping & abuse.

## 2️⃣ Load Balancer Level Rate Limiting
✅ Best for: IP-based rate limiting, DDoS protection

Enforced at Layer 4 (Transport Layer) via load balancers (e.g., Nginx, HAProxy, AWS ALB, GCP Load Balancer).
Limits connections per IP, port, or TCP session.

### ⚙️ How it Works
1. A client sends too many requests in a short period.
2. The load balancer drops excessive connections based on its policy.
3. Requests that pass the limit are forwarded to the API Gateway or backend.

### ✅ Pros
✔ Defends Against DDoS Attacks → Prevents floods of connections.

✔ Low Latency → Works at the transport level (faster than API Gateway).

✔ Prevents Server Overload → Stops TCP/UDP request floods before hitting services.

### ❌ Cons
✘ No Application Awareness → Cannot limit by user, API key, or endpoint.

✘ IP-Based Limits Can Fail → Attackers can rotate IPs (use Cloudflare/WAF).

✘ Limited Flexibility → Cannot enforce complex rules like user-based limits.

🚀 Best Use Cases

✅ DDoS mitigation (limit connections per IP).

✅ Rate limiting WebSockets or UDP requests.

✅ Preventing TCP SYN flood attacks.

## 3️⃣ Backend Service Level Rate Limiting
✅ Best for: Granular, per-user or per-function rate limiting

Implemented in backend application code (e.g., in Python, Java, or Go).
Uses in-memory cache (local) or Redis (distributed).

### ⚙️ How it Works
1. A request reaches the backend.
2. The application checks the rate limit before processing it.
3. If the request exceeds the limit, return HTTP 429; otherwise, process it.

### ✅ Pros
✔ Full control of the rate limiting algorithm

✔ Per-user or API key limits → More granular than API Gateway or Load Balancer.

✔ Dynamic Limits → Can adjust limits based on user type (e.g., free vs. premium users).

✔ Custom Handling → Can log violations, return custom responses, or queue requests.

### ❌ Cons
✘ High Latency → Requests reach the backend before being rejected.

✘ No Global Awareness → Cannot enforce limits across multiple servers easily.

✘ Backend Overload Risk → Requests still consume resources before being limited.

## More points to note

- If you have already used microservice architecture and included an API gateway in the
design to perform authentication, IP whitelisting, etc., you may add a rate limiter to the
API gateway.
- Building your own rate limiting service takes time. If you do not have enough
engineering resources to implement a rate limiter, a commercial API gateway is a better
option.


# Tradeoff Between Low Memory Usage and High Accuracy in Rate Limiting

When designing a rate limiter, there's a tradeoff between memory efficiency and accuracy in tracking request limits. The choice depends on factors like:
- traffic volume
- performance requirements
- rate limit enforcement strictness.

### Key Factors Affecting the Decision

| Factor  | Favor Low Memory Usage  | Favor High Accuracy  |
| ------------ | ------------ | ------------ |
| User Traffic | Millions of users, global APIs | Small-scale API with strict enforcement |
| Burst Handling | Allow short bursts | Strict real-time control |
| Latency Constraints | Must be ultra-fast | Can tolerate minor delays |
| Storage Cost | Using Redis with limited RAM | Large storage budget available |
| DDoS Protection | Best-effort filtering | Strict security required |


### Examples of Tradeoff in Different Rate Limiting Strategies

| Rate Limiting Algorithm  |  Memory Usage | Accuracy  | Use Case  |
| ------------ | ------------ | ------------ | ------------ |
| Fixed Window Counter | Low | Low | Simple API rate limiting (e.g., 100 req/min) |
| Sliding Window Counter | High | High | Real-time, strict rate enforcement |
| Token Bucket |  Medium | Medium | Best balance for burst-friendly APIs |
| Approximate Counting (e.g., HyperLogLog, Bloom Filters) | Very Low | Low | Large-scale, memory-efficient rate limiting |


# Circuit Breakers in Rate Limiters

## What is a Circuit Breaker?
A circuit breaker is a fault-tolerance mechanism that prevents repeated calls to a failing service. If a component (like a rate limiter using Redis) fails or slows down, the circuit breaker trips and blocks requests temporarily instead of overwhelming the failing system.

## Why is it Needed in Rate Limiting?
If Redis (or any storage backend) used for rate limiting becomes unavailable, checking the rate limit might take too long or fail.
Without a circuit breaker, the system would continuously retry Redis, causing worse performance.
The circuit breaker detects failures and temporarily bypasses rate limiting or applies a default behavior.

##  Circuit Breaker States
| State  | Meaning  | Action Taken  |
| ------------ | ------------ | ------------ |
| Closed | Everything is normal | Requests are processed as usual |
| Open | Too many failures detected | Requests bypass rate limiter (fail-safe) |
| Half-Open | Recovering, testing the system | Allow limited requests to check if Redis is back |

# Fallback Mechanisms

## What is a Fallback Mechanism?
A fallback mechanism is an alternative action taken when the primary system fails. Instead of completely stopping requests, the system switches to a backup strategy.

## Why is it Needed in Rate Limiting?
If Redis fails, the system still needs a way to enforce some default rate limits.
Instead of blocking all requests, the system can apply an emergency fallback (e.g., assume all users are within limits).
Prevents false positives (blocking legitimate requests due to a temporary failure).

## Common Fallback Strategies
| Strategy | When to Use | How It Works |
| --------------- | ---- | ----- |
| Allow all requests (fail-open) | When uptime is critical | If Redis is down, assume no limits apply | 
| Apply a default limit | When some control is needed | Use a fixed in-memory rate limit for all users |
| Local cache fallback | When Redis is temporarily slow | Store recent limits in local cache |

**Best Practice:** Use both together for fault tolerance
