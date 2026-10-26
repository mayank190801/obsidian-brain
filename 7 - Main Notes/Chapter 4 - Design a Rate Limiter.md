[[Alex Xu System Design Essentials]]

- Basically limit the number of requests allowed over a specific period of time 
- All the excess calls are blocked 

Benefits? 
- Prevent resource starvation caused by DOS attacks 
- Reduce cost (if you use third party APIs then even more)
- Prevent servers from being overloaded (due to bots or user misbehaviour)


### Step - 1 Understand the problem and establish design scope 

- Candidate: What kind of rate limiter are we going to design? Is it a client-side rate limiter or server-side API rate limiter? Interviewer: Great question. We focus on the server-side API rate limiter. 
- Candidate: Does the rate limiter throttle API requests based on IP, the user ID, or other properties? Interviewer: The rate limiter should be flexible enough to support different sets of throttle rules. 
- Candidate: What is the scale of the system? Is it built for a startup or a big company with a large user base? Interviewer: The system must be able to handle a large number of requests.
- Candidate: Will the system work in a distributed environment? Interviewer: Yes.
- Candidate: Is the rate limiter a separate service or should it be implemented in application code? Interviewer: It is a design decision up to you. 
- Candidate: Do we need to inform users who are throttled? Interviewer: Yes.

Requirements 
- Accurately limit excessive requests
- Low Latency - should not slow down HTTP response time 
- As little memory as possible 
- Distributed rate limiting
- Exception handling - (user should be notified)
- High fault tolerance - any problem with rate limitier should not affect

### Step - 2 Propose high level design and get a buy in

Where to put the rate limiter??? 
- Client Side - unrealiable as it can be easily bypassed 
- Server Side - We have two options, into the server code or somewhere in between (like API gateway)

![[Screenshot 2024-08-17 at 11.27.34 AM.png]]
![[Screenshot 2024-08-17 at 11.27.50 AM.png]]![[Screenshot 2024-08-17 at 11.28.25 AM.png]]
- It sends back 429 status code (used when too many requests are being sent
- API gateway. API gateway is a fully managed service that supports rate limiting, SSL termination, authentication, IP whitelisting, servicing static content, etc.

Important points to keep in consideration 
- Company tech stack (current language is efficient enough)
- Server side (mostly full control) but if using third party API gateway (then not much)
- Already have self implemented API gateway then easier to go forward with it
- Usually difficult to implement, preffered to use commercial API gateway. 

###### Algorithms 

- Token Bucket 
- Leaking Bucket 
- Fixed Window Counter 
- Sliding Window Log 
- Sliding Window Counter 

**Token Bucket Algorithm** 

![[Screenshot 2024-08-17 at 11.38.12 AM.png]]
- There is one bucket concept, which refills at every minute/seconds. 
- If the bucket is full, the tokens will be overflowed. 
- If a request comes up, it sees if a token is present in the bucket, picks it up and moves forward
- If no, token is there then that request will be sent back/dropped.
- It has only two paramets - (bucket size and refill rate)

How many buckets do we need? 
- Depends, necessary to have different bucket for different API endpoints (A user can not send these many requests pr day, not these many posts etc)
- Throttling based on IP adress, then we require that many buckets (for each IP adress)
- Global buckets can be also setup, (only 10k requests per day entire software)

Pros 
- Simple to implement 
- Memory Efficient 
- Sudden bursts of requests can also be handled with this 
Cons
- Hard to tune those two parameters correctly 


**Leaking Bucket Algorithm**

![[Screenshot 2024-08-17 at 11.45.32 AM.png]]
- Similar to token bucket except requests are processed at fixed rate 
- Queue is used with FIFO 
- Just look at the diagram, pretty clear what is happening 
- Bucket Size and Outflow rate are two parameters for it. 
- Suitable for usecases which requires stable outflow rate 

Cons 
- A burst of traffic fills up the queue with old requests, and if they are not processed in time, recent requests will be rate limited.
- Parameters are hard to tune.

**Fixed window counter algorithm**

![[Screenshot 2024-08-17 at 11.52.44 AM.png]]
- It divides the timeline into fix-sized windows and assign a counter for each 
- Each request increments the counter by one, when reached threshold all other requests are rate limited 
- Above example is 3 requests every second sort of 

A major problem exists 

![[Screenshot 2024-08-17 at 11.54.49 AM.png]]
- Suppose 5 requests per minutes are allowed 
- But in span of 2 minutes, 10 requests happened and that too close to the edge of the window. 
- This caused 10 requests in 1 minutes time window (DOUBLE THE EXPECTED)

Pros 
- Memory Efficient 
- Easy to understand 
- Resetting quota in fixed time periods (fits certain use cases)

Cons 
- Discussed above 

**Sliding window log algorithm**

![[Screenshot 2024-08-17 at 12.06.42 PM.png]]
- One flaw with the above diagram, if the request at 1:00:50 is rejected, then it should not be logged (think logically)
- Becase now if 1:01:40 is entered, it will see the log count to be 2 (1:00:40 - 1:01:40) where as it should be 1 only! (since that previous request was rejected brother)

How it works 

**Log of Timestamps**:
• For each client, the algorithm maintains a log of timestamps corresponding to the requests made by that client.
• Each time a new request is received, the current timestamp is added to the log.

**Prune Old Timestamps**:
• The algorithm removes timestamps from the log that fall outside the defined time window. For example, if the window is set to 1 minute, it will remove any timestamps older than 1 minute.

**Check Log Size**:
• After pruning, the algorithm checks the size of the log.
• If the log contains fewer entries than the allowed limit, the request is allowed.
• If the log has reached or exceeded the allowed limit, the request is rejected.

Pros 
- Very accurate 

Cons 
- Consumes a lot of memory 
- Performance wise can take hits 

**Sliding window counter algorithm**

![[Screenshot 2024-08-17 at 12.12.12 PM.png]]
- Simpler and more memory efficient compared to sliding window log algorithm (it sacrifices some precision)
- But acc to a study only 0.003% request were wrongly with this approach 

How it works ? 
- Basically the time is divided into time windows (shorter the better normally)
- Each window has a counter that tracks the number of requests made during that interval 
- We use current window and previous window for our criteria 
- When a new request arrives, the algorithm checks the count of requests in the current window and a weighted count from the previous window to account for the overlap between the two windows. 
  (Example - Requests in current window + requests in the previous window * overlap percentage of the rolling window and previous window)
- The proportion are based on the time overlap between current and previous windows. 
- If weighted sum exceed the current limit, then nope 

Example

- Assume the rate limiter allows a maximum of 7 requests per minute, and there are 5 requests in the previous minute and 3 in the current minute.
- For a new request that arrives at a 30% position in the current minute, the number of requests in the rolling window is calculated using the following formula: 
		• Requests in current window + requests in the previous window * overlap percentage of the rolling window and previous window 
		• Using this formula, we get 3 + 5 * 0.7% = 6.5 request.
- Depending on the use case, the number can either be rounded up or down. In our example, it is rounded down to 6.

Pros 
- Use less memory compared to sliding window log algorithms 
- Easier to implement 

Cons 
- Slightly less accurate than sliding window log algo
- Can be used for not so accurate request scenarions 

###### High-level architecture

![[Screenshot 2024-08-17 at 12.27.11 PM.png]]

- Basic idea is clear and simple, if the request based on IP address we need to keep a counter and throttle it on based of that 
- Database is slow, hence use Cache (most famous in market - Redis - Provides (INCR and EXPR))
- Cache are fast and supports time based 

### Step 3 - Design deep dive

**Rate Limiting Rules** 

 - Let's look at how lyft implemented these rules 
```
domain: messaging 
descriptors: 
	- key: message_type 
	- Value: marketing 
	- rate_limit: 
		- unit: day 
		- requests_per_unit: 5
```
- The system is configured to allow a maximum of 5 marketing messages per day. 

**Rate Limit Headers**

- How does a client know if it is throttled, or after how many request it will be throtlled????
- The answer lies in response headers (simple as that)
- X-Ratelimit-Remaining: The remaining number of allowed requests within the window. 
- X-Ratelimit-Limit: It indicates how many calls the client can make per time window. 
- X-Ratelimit-Retry-After: The number of seconds to wait until you can make a request again without being throttled.
- When a user has sent too many requests, a 429 too many requests error and X-Ratelimit- Retry-After header are returned to the client.

**Detailed Design**

![[Screenshot 2024-08-17 at 12.43.19 PM.png]]
- Rules are stored on the disk. Workers frequently pull rules from the disk and store them in the cache.
- Everything else is pretty clear from the design (option 1 and option 2 depends on the usecase)

### Rate limiter in a distributed environment
- Scaling the system to support multiple servers and concurrent threads is a different story
- Two issues - Race Condition and Synchronisation Issues

Race Condition 
- When two threads, try to update one value in redis, in that case it can take place 
- Two strategies are commonly used to solve the problem: Lua script [13] and sorted sets data structure in Redis [8].
- [Better rate limiting with Redis sorted sets | Building ClassDojo](https://engineering.classdojo.com/blog/2015/02/06/rolling-rate-limiter/)

Synchronisation 
- When multiple servers of rate limiters are there in that how would we synchronise the data?? 
- If no synchronisation, then server 1 would not know about the data of client 2 and vice versa 
![[Screenshot 2024-08-17 at 2.43.23 PM.png]]
![[Screenshot 2024-08-17 at 2.43.45 PM.png]]
- You can use sticky session or a centralized data store like in above image (sticky sessions are not scalable)

**Performance Optimization**
- Have edge servers throughout the world (many cloud providers provide that). Traffic is automatically routed to the closest edge server 
- Synchronize data with an eventual consistency model. If you are unclear about the eventual consistency model

**Monitoring** 
- Important aspect 
- Make sure - The rate limiting algorithm is effective. • The rate limiting rules are effective.
- For example, if rate limiting rules are too strict, many valid requests are dropped. In this case, we want to relax the rules a little bit. In another example, we notice our rate limiter becomes ineffective when there is a sudden increase in traffic like flash sales. In this scenario, we may replace the algorithm to support burst traffic. Token bucket is a good fit here

### Step 4 - Wrap up

We discussed a bunch of rate-limiting algorithms:

- Token bucket - good for supporting traffic bursts.
- Leaking bucket - good for ensuring consistent inbound request flow to downstream services
- Fixed window - good for specific use-cases where you want time divided in explicit windows
- Sliding window log - good when you want high rate-limiting accuracy at the expense of memory footprint.
- Sliding window counter - good when you don't want 100% accuracy with a very low memory footprint.

Additional talking points if time permits:

- Hard vs. soft rate limiting
    - Hard - requests cannot exceed the specified threshold
    - Soft - requests can exceed threshold for some limited time
- Rate limiting at different layers - L7 (application) vs L3 (network)
- Client-side measures to avoid being rate limited:
    - Client-side cache to avoid excessive calls
    - Understand limit and avoid sending too many requests in a small time frame
    - Gracefully handle exceptions due to being rate limited
    - Add sufficient back-off and retry logic