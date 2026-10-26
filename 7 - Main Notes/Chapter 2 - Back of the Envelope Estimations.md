[[Alex Xu System Design Essentials]]

- Sometimes you are asked to estimate the system capacity and other requirements 

- A byte is a sequence of 8 bits
- An ASCII character uses one byte of memory (8 bits).

![[Screenshot 2024-08-15 at 11.46.21 AM.png]]
 
 ![[Screenshot 2024-08-17 at 12.45.36 PM.png]]

- L1 cache reference == 0.5ns
- Branch mispredict == 5ns
- L2 cache reference == 7ns
- Mutex lock/unlock == 100ns
- Main memory reference == 100ns
- Compress 1kb == 10,000ns == 10us
- Send 2kb over 1gbps network == 20,000ns == 20us
- Read 1mb sequentially from memory == 250us
- Round trip within same DC == 500us
- Disk seek == 10ms
- Read 1mb sequentially from network == 10ms
- Read 1mb sequentially from disk == 30ms
- Send packet CA->Netherlands->CA == 150ms

- ns = nanosecond, µs = microsecond, ms = millisecond 
- 1 ns = 10^-9 seconds 
- 1 µs= 10^-6 seconds = 1,000 ns 
- 1 ms = 10^-3 seconds = 1,000 µs = 1,000,000 ns

Some conclusions from the above numbers:

- Memory is fast, disk is slow
- Avoid disk seeks if possible
- Compression is usually fast
- Compress data before sending over the network if possible
- Data centers round trips are expensive

### Availability Numbers 

- A service level agreement (SLA) is a commonly used term for service providers. This is an agreement between you (the service provider) and your customer, and this agreement formally defines the level of uptime your service will deliver.
- Cloud providers Amazon [4], Google [5] and Microsoft [6] set their SLAs at 99.9% or above
![[Screenshot 2024-08-15 at 12.12.18 PM.png]]

Example: 
**Estimate Twitter QPS and storage requirements** 

Assumptions: 
300 million monthly active users. 
50% of users use Twitter daily. 
Users post 2 tweets per day on average. 
10% of tweets contain media. 
Data is stored for 5 years. 

Estimations: 
Query per second (QPS) estimate: 
Daily active users (DAU) = 300 million * 50% = 150 million 
Tweets QPS = 150 million * 2 tweets / 24 hour / 3600 seconds = ~3500 
Peek QPS = 2 * QPS = ~7000 

We will only estimate media storage here. 
Average tweet size: 
• tweet_id 64 bytes 
• text 140 bytes 
• media 1 MB 
Media storage: 150 million * 2 * 10% * 1 MB = 30 TB per day 
5-year media storage: 30 TB * 365 * 5 = ~55 PB

Tips 
- Rounding and approximation is the way to go 
- Write down assumptions 
- Label them correctly 
- Also practise - QPS, peak QPS, storage, cache, numbers of servers etc.


### Extra

The Open Systems Interconnection model (OSI model) has 7 layers [16]: Layer 1: Physical layer, Layer 2: Data link layer, Layer 3: Network layer, Layer 4: Transport layer, Layer 5: Session layer, Layer 6: Presentation layer, Layer 7: Application layer.