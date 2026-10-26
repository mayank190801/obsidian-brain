
2024-07-17 09:41
Status: 
Tags:

# Cache Challenges

##### 1. Thundering Herd
- The thundering herd problem occurs when a popular piece of data expires from the cache, leading to a sudden surge in requests to the origin server to fetch the missing data.
- Solved using staggered expiration times, implementing a cache lock, or using background updates to refresh the cache before the data expires.
##### 2. Cache Penetration
- Cache penetration refers to the situation where requests for data bypass the cache and directly access the origin server, reducing the benefits of caching. 
- This typically happens when requests are made for non-existent or rarely accessed data. 
- To mitigate cache penetration, negative caching (caching negative responses) or using a bloom filter to check for the existence of data before querying the cache can be employed.
##### 3. Big Key
- A big key is a large piece of data that consumes a significant portion of the cache's capacity. Storing big keys can lead to cache evictions, reducing the overall effectiveness of the caching system. 
- Solutions for handling big keys include compressing the data before caching, breaking the data into smaller chunks, or using a separate caching strategy specifically designed for large objects.
##### 4. Hot Key
- A hot key refers to a piece of data that is frequently accessed, causing contention and performance issues in the caching system. 
- Solutions are using consistent hashing to distribute the load more evenly, replicating the hot key across multiple cache nodes, or implementing a load balancing strategy to distribute requests across multiple instances of the hot key.

##### 5. Cache Stampede (or Dogpile)
- Cache stampede occurs when multiple requests for the same data are made simultaneously, causing excessive load on the cache and the origin server. 
- Solved by combining multiple requests for the same data into a single request or implementing a read-through cache, where the cache itself fetches the missing data from the origin server.
##### 6. Cache Pollution
- Cache pollution occurs when less frequently accessed data displaces more frequently accessed data in the cache, leading to a reduced cache hit rate. 
- Use LRU or LFU 
##### 7. Cache Drift
- Cache drift refers to the inconsistency between cached data and the data on the origin server, typically caused by updates or changes in the data. 
- Use proper cache invalidation strategies 









# **References**