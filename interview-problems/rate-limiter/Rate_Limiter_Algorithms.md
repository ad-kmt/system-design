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
