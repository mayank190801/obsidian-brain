
2024-07-17 09:38
Status: 
Tags:

# Cache Invalidation

 If the data is modified in the database, it should be invalidated in the cache; if not, this can cause inconsistent application behavior.

###### 1. Write-through cache
- Under this scheme, Data is written into the cache and the corresponding database simultaneously. 
- The cached data allows for fast retrieval 
- Complete data consistency between the cache and the storage
- Nothing will get lost in case of a crash, power failure, or other system disruptions. 
- Every write operation must be done twice before returning success to the client
- higher latency for write operations.

###### 2. Write-around cache
- Data is written directly to permanent storage, bypassing the cache.
- Reduce the cache being flooded with write operations that will not subsequently be re-read
- Disadvantage that a read request for recently written data will create a “cache miss”

###### 3. Write-back cache
- Data is written to cache alone, and completion is immediately confirmed to the client.
- Write to the permanent storage is done when the system needs some free space
- Low-latency and high-throughput for write-intensive applications
- Risk of data loss

###### 4. Write-behind cache
- Data is written to the cache and acknowledged to the application immediately, but it is not immediately written to the permanent storage.
- Eventually written to the permanent storage at specified intervals.








# **References**