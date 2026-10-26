[[Alex Xu System Design Essentials]]

### Single Server Setup 
- Pretty evidently clear 
- We have domain names and DNS (3rd party)
- Then using IP Adress and HTTP we send and recieve request/response

### Databases 
- Now different servers for web traffic and databases (helps in scaling them independently)
- Web tier and data tier basically 
- Relational databases - MySQL, Oracle database, PostgreSQL, etc.
- Non Relational databases - CouchDB, Neo4j, Cassandra, HBase, Amazon DynamoDB, etc.
- Four categories - key-value stores, graph stores, column stores, and document stores

When to choose NoSQL
• Your application requires super-low latency.
• Your data are unstructured, or you do not have any relational data.
• You only need to serialize and deserialize data (JSON, XML, YAML, etc.).
• You need to store a massive amount of data.

### Load Balancer
- Pretty dope, they distribute the requests among different servers (Public IP and Private IP concepts)

![[Screenshot 2024-08-15 at 8.40.30 AM.png]]

### Database replication
- Usually a master slave relationship among different database servers
- Master handles write, slaves handles read
- Read:Write ratio exist because of which slaves are usually more 
![[Screenshot 2024-08-15 at 8.42.42 AM.png]]

- Better Performance - Master DB handles are writes, read operations are distributed across Slave DB, hence more queries in parallel can take place 
- Reliability - Since DB is present at more than one location 
- Highly Available - For read operations atleast 

What happens in case of failures? 
- If only one slave database is available and it goes offline, read operations will be directed to the master database temporarily. As soon as the issue is found, a new slave database will replace the old one. In case multiple slave databases are available, read operations are redirected to other healthy slave databases. A new database server will replace the old one. 

- If the master database goes offline, a slave database will be promoted to be the new master. All the database operations will be temporarily executed on the new master database. A new slave database will replace the old one for data replication immediately. In production systems, promoting a new master is more complicated as the data in a slave database might not be up to date. The missing data needs to be updated by running data recovery scripts. Although some other replication methods like multi-masters and circular replication could help, those setups are more complicated.

![[Screenshot 2024-08-15 at 8.50.52 AM.png]]

### Cache 
![[Screenshot 2024-08-15 at 8.51.52 AM.png]]
- The cache tier is a temporary data store layer, much faster than the database.
- After receiving a request, a web server first checks if the cache has the available response. If it has, it sends data back to the client. If not, it queries the database, stores the response in cache, and sends it back to the client. This caching strategy is called a **read-through cache.**
- Multiple other cache techniques are there (figure those out in depth with time)

When to use these? 
- When read is more frequent than writes 
- Not used for persisting data, used for keeping it volatile etc. 
- Expiration policy is important for cache data (not too long, not too short)
- Maintain consistency if possible (Ready facebook articles on it)
- Have more than one cache server available (we can see different ways to implement in real world projects)
- Cache eviction policies are important (like LRU, LFU, etc)

### Content Delivery Network (CDN)
- a network of geographically dispersed servers used to deliver static content
- images, videos, CSS, JavaScript files, etc
- Dynamic content caching is a relatively new concept and beyond the scope of this book. It enables the caching of HTML pages that are based on request path, query strings, cookies, and request headers (relatively newer concept, pls ping it later)

![[Screenshot 2024-08-15 at 9.19.59 AM.png]]
![[Screenshot 2024-08-15 at 9.20.31 AM.png]]
- Basically different URL for CDN images
- HIt CDN, it not found, it will hit S3 (get TTL), then back to user, if present, then return back (simple)

Consideration to make 
- Cost (if not necessary you can save money here)
- Appropriate TTL 
- CDN fallback (what if it fails? then client should have some planned solution for that as well)
- Invalidate file before TTL (you are given few APIs by CDN vendors to invalidate the files) - suppose you update some image, then you should invalidate the CDN (could be entire reset or file reset maybe
- You can also use object versioining to serve different version of that object, by making changes in the URL - Example -: image.png?v=2.

![[Screenshot 2024-08-15 at 9.26.45 AM.png]]
-  Static assets (JS, CSS, images, etc.,) are no longer served by web servers. They are fetched from the CDN for better performance (insane performance boost)
- Database load is lightened by caching data (invalidate it as well according to requirements)

### Stateless web tier

Stateful Architecture
![[Screenshot 2024-08-15 at 10.48.52 AM.png]]
- User A session data and profile image are stored in the server 1 only, hence we would have to route the request to the same server everytime 
- Can be done with sticky session in load balancer (but increase complexity)

Stateless Architecture
![[Screenshot 2024-08-15 at 10.50.17 AM.png]]
- HTTP requests can be sent to any web server, and they can fetch data from shared storage 
- Easy to implement, scalable and robust solution 

Hence the latest design looks something like this!!!! 

![[Screenshot 2024-08-15 at 10.51.52 AM.png]]
Pretty neat no? (get more deeper baby)

#### Data Centers
-  geoDNS is a DNS service that allows domain names to be resolved to IP addresses based on the location of a user.
![[Screenshot 2024-08-15 at 10.53.12 AM.png]]

Technical challenges faced with this type of architecture? 
- Traffic redirection - Use geoDNS to redirect traffic based on the location of the user 
- Data Synchronization - Replicate data across multiple data center (Learn how netflix does this approach)
- Test and deployment - Automated setups to test everything (isn't this true for everything)
- Netflix uses Apache Cassandra for data storage, which supports multi-region replication to ensure data is accessible across all regions.

### Message Queue
![[Screenshot 2024-08-15 at 11.27.10 AM.png]]
- Decoupling makes the message queue a preferred architecture for building a scalable and reliable application. With the message queue, the producer can post a message to the queue when the consumer is unavailable to process it. The consumer can read messages from the queue even when the producer is unavailable.
- Example - Batch processing for image suppose (increase producer or consumer workers independently based on the size of message queue)

### Logging Metrics and Automation 
- These become important as the scale of the system grows 
- Always have an idea for implementing them

**EVEN MORE UPDATED LAYOUT** 
![[Screenshot 2024-08-15 at 11.30.27 AM.png]]

### Database Scaling 
- Vertical Scaling / Horizontal Scaling 
- Amazon Relational Database service can reach upto 24TB of ram 
- stackoverflow in 2013 had 10 million monthly active users - 1 Master database only 
- **Horizontal Scaling also known as sharding** (practise of adding more servers)
- Each shard shares the same schema, though the actual data on each shard is unique to the shard.
- Example 
![[Screenshot 2024-08-15 at 11.34.14 AM.png]]

- Most important factor is selecting the sharding key (partition key)
- A key that can evenly distribute data (v.imp)
- Great technique but far from perfect solution 

Issues with Data Sharding 
- Resharding data - if data in one shard exceed, or we have to add or remove shards in that case (we can use consistent Hashing to solve these sort of issues)
- Celebrity Problem - hotspot key problem - Imagine having data of ceveral big celebs in one shard, this will cause more requests and hence overwhelm it with read operations 
- Join and de-normalization - join operations are harder to perform, solution is to simply denormalize the most used joins 

Peak software engineering 
![[Screenshot 2024-08-15 at 11.41.42 AM.png]]

Summary for this chapter 

- Keep web tier stateless 
- Build redundancy at every tier 
- Cache data as much as you can 
- Support multiple data centers 
- Host static assets in CDN 
- Scale your data tier by sharding  
- Split tiers into individual services 
- Monitor your system and use automation tools

