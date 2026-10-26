
### What to estimate? 

- Find the crux of the questions 
- Almost all designs need to know approximate quantities for:
	- Read and write throughput of the bottleneck service (often the DB or the API layer).
	- Total storage quantity of the system (spread across memory and disk).


### Data Size

- **1 KB = 1,000 bytes**
- **1 MB = 1,000 KB**
- **1 GB = 1,000 MB**

```java
10^0   → 1              → Unit
10^3   → 1,000          → Kilo (KB)
10^6   → 1,000,000      → Mega (MB)
10^9   → 1,000,000,000  → Giga (GB)
10^12  → Trillion       → Tera (TB)
10^15  → Quadrillion    → Peta (PB)
```

- **1 million × 1 KB = 1 GB**
- **1 billion × 1 byte = 1 GB**
- **1 million × 1 MB = 1 TB**
- **1 billion × 1 KB = 1 TB**

```java
int        → 4 bytes
long       → 8 bytes
boolean    → 1 byte
char       → 1 byte
varchar(n) → n bytes
timestamp  → 8 bytes
UUID       → 16 bytes
```

### Latency

| Reading 1mb sequentially from memory         | 0.25ms |           |
| -------------------------------------------- | ------ | --------- |
| Reading 1mb sequentially from SSD            | 1ms    | 4x memory |
| Reading 1mb sequentially from spinning disk  | 20ms   | 20x SSD   |
| Round trip network latency CA to Netherlands | 150ms  |           |

Historically we introduced sharding, caching, and replication to fight hardware limits. With modern hardware, we can often start simple and add these only when scale demands it.

### Storage 

| Item                                                 | Size  |
| ---------------------------------------------------- | ----- |
| A two-hour movie                                     | 1gb   |
| A small book of plain text                           | 1mb   |
| A high-resolution photo                              | 1mb   |
| A medium-resolution image (or a site layout graphic) | 100kb |

Expect to size up a record or struct during your interview (hint: add up all the fields!). Don't forget to round the final result, you don't need to carry a 323 byte calculation all the way through your interview so rounding to 500 bytes or even 1kb is probably ok.


### Business
|Metric| Order of Magnitude |
|---|---|
|Daily active users of major social networks| O(1b)              |
|Hours of video streamed on Netflix per day| O(100m)            |
|Google searches per second| O(100k)            |
|Size of Wikipedia| O(100gb)           |


### Common Mistakes 
- Will probably takes 2-3 minutes of your time
- Don't estimate something that doesn't matter 
- Getting stuck in the math 
- Getting quantities outrageously wrong 


### BUILD YOUR ESTIMATION MUSCLE 
- estimate and check random stats 














