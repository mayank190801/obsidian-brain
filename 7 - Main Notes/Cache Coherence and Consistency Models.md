
2024-07-17 09:40
Status: 
Tags:

# Cache Coherence and Consistency Models


These models ensure that data remains accurate and up-to-date across multiple caches or processing units.

#### Cache Coherence (write in your own language)

It is a property of multi-core processors or distributed systems that ensures all processors or nodes see the same view of shared data.

 In a system with multiple caches, each cache may store a local copy of the shared data. When one cache modifies its copy, it is essential that all other caches are aware of the change to maintain a consistent view of the data.
 
To achieve cache coherence : 

- **Write-invalidate:** When a cache writes to its copy of the shared data, it broadcasts a message to other caches, invalidating their copies. When another cache requires the updated data, it fetches the new data from the memory or the cache that made the change.

- **Write-update (or write-broadcast):** When a cache writes to its copy of the shared data, it broadcasts the updated data to all other caches, which update their local copies accordingly.

#### Cache Consistency Models

- **Strict Consistency:** In this model, any write to a data item is instantly visible to all caches. This model provides the highest level of consistency but is difficult to achieve in practice, as it may require significant synchronization overhead and negatively impact performance.

- **Sequential Consistency:** In this model, all operations on data items appear to occur in a specific sequential order across all caches. While this model allows for better performance than strict consistency, it still requires considerable synchronization and may not be practical in many distributed systems.

- **Causal Consistency:** In this model, operations that are causally related (i.e., one operation depends on the outcome of another) are guaranteed to appear in order across all caches. Operations that are not causally related can occur in any order. This model provides better performance than sequential consistency while still ensuring a reasonable level of data accuracy.

- **Eventual Consistency:** In this model, all updates to a data item will eventually propagate to all caches, **but there is no guarantee about the order or timing of the updates**. This model offers the best performance among the consistency models but provides the weakest consistency guarantees. Eventual consistency is often used in distributed systems where performance and scalability are prioritized over strict data accuracy.










# **References**