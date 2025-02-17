# Rate Limiting Algorithms

Rate limiting can be implemented using different algorithms, and each of them has distinct
pros and cons. Understanding them at high-level helps to choose the right algorithm or combination of algorithms to fit our use
cases.

Here is a list of popular algorithms:
- Token bucket
- Leaking bucket
- Fixed window counter
- Sliding window log
- Sliding window counter

## Token bucket algorithm
The token bucket algorithm is widely used for rate limiting. It is simple, well understood and
commonly used by internet companies.

**Example**: Both [Amazon](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-request-throttling.html "Amazon") and [Stripe](https://stripe.com/blog/rate-limiters "Stripe") use this algorithm to throttle their API requests.

### How it works

**Step 1**: A token bucket is set to a pre-defined capacity. Tokens are put in the bucket
at preset rates periodically. Once the bucket is full, no more tokens are added. 

As shown in below figure, the token bucket capacity is 4. The refiller puts 2 tokens into the bucket every second. Once the bucket is full, extra tokens will overflow.

![image](https://github.com/user-attachments/assets/db2461a2-c26d-4061-8896-05a677765985)

**Step 2**: Each request consumes one token. When a request arrives, we check if there are enough
tokens in the bucket.  Below Figure explains how it works.
- If there are enough tokens, we take one token out for each request, and the request
goes through.
- If there are not enough tokens, the request is dropped.

![image](https://github.com/user-attachments/assets/8191da4f-ca1c-4540-aeb2-cca09b89a81f)

**Example:** Below figure illustrates how token consumption, refill, and rate limiting logic work. In this example, the token bucket size is 4, and the refill rate is 4 per 1 minute.

![image](https://github.com/user-attachments/assets/5d4d2af9-7bcb-40b0-85d5-3e0f79cd6a1f)

#### Parameters
The token bucket algorithm takes two parameters:
- **Bucket size**: the maximum number of tokens allowed in the bucket
- **Refill rate**: number of tokens put into the bucket every second

#### How many buckets do we need? 
This varies, and it depends on the rate-limiting rules. Here are a few examples.
- It is usually necessary to have different buckets for different API endpoints. For instance, if a user is allowed to make 1 post per second, add 150 friends per day, and like 5 posts per second, 3 buckets are required for each user.
- If we need to throttle requests based on IP addresses, each IP address requires a bucket.
- If the system allows a maximum of 10,000 requests per second, it makes sense to have a global bucket shared by all requests.

### Pros and Cons

#### Pros:
- Simple and easy to implement.
- Uses minimal memory.
- The token bucket allows short bursts of traffic, as requests are processed if tokens are available.

#### Cons:
- Requires careful tuning of two key parameters: bucket size and token refill rate, which can be challenging.


## Leaking Bucket Algorithm

The **Leaking Bucket Algorithm** is similar to the **Token Bucket Algorithm**, but instead of allowing bursts, it processes requests at a **fixed rate**. It is typically implemented using a **First-In-First-Out (FIFO) queue**.

### How It Works
1. When a request arrives, the system checks if the queue has space:
   - **If the queue is not full**, the request is added.
   - **If the queue is full**, the request is dropped.
2. Requests are processed from the queue at **regular intervals**, maintaining a steady outflow.

### Parameters
- **Bucket Size**: The maximum number of requests the queue can hold.
- **Outflow Rate**: The number of requests processed per second.

**Example Usage**
- Shopify, an e-commerce company, uses the **Leaky Bucket Algorithm** for **rate-limiting**.

### Pros and Cons

#### Pros
✅ **Memory Efficient** – The queue has a fixed size, preventing excessive memory use.  
✅ **Stable Processing Rate** – Ensures a steady outflow, making it suitable for cases requiring **consistent request processing**.

#### Cons
❌ **Traffic Bursts Issue** – A sudden spike in requests fills up the queue with old requests, potentially dropping newer ones.
❌ **Parameter Tuning Complexity** – Finding the optimal **bucket size** and **outflow rate** can be challenging.

## Fixed Window Counter Algorithm
The **Fixed Window Counter** algorithm is a simple rate-limiting technique that divides time into fixed-sized windows and tracks request counts within each window.

### How It Works
1. The timeline is divided into fixed-sized time windows.
2. Each window has a counter initialized to zero.
3. Every incoming request increments the counter by 1.
4. If the counter reaches a predefined threshold, additional requests are **dropped** until the next time window begins.

### Example
- Suppose the system allows **3 requests per second**.
- If more than 3 requests arrive within the same second, the excess requests are **discarded**.
- A visualization of this behavior is shown in **Figure 4-8**.

### Edge Case: Traffic Burst at Window Boundaries
A limitation of this approach is that traffic spikes **at the edges of time windows** can allow **more requests than the quota**.  
For instance:
- A system allows **5 requests per minute**.
- The quota resets at each full minute (e.g., 2:00:00, 2:01:00).
- If **5 requests are made at 2:00:59 and another 5 at 2:01:01**, a total of **10 requests** go through in a span of one minute, **exceeding the allowed limit**.

### Pros & Cons

#### ✅ Pros:
- **Memory efficient** – Only a single counter per window is needed.
- **Simple and easy to understand**.
- **Works well when resetting quota at fixed time intervals**.

#### ❌ Cons:
- **Traffic spikes near window edges** can lead to exceeding the allowed request limit.

