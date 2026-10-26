
2024-07-17 09:43
Status: 
Tags:

# Data Partitioning

### Introduction to Data Partitioning

 - It is a technique used in distributed systems and databases to divide a large dataset into smaller, more manageable parts, referred to as partitions. 
 - Each partition is independent and contains a subset of the overall data.
 - Each partition is then assigned to a separate processing node, which can perform operations on its assigned data subset independently of the others.
 - The system can handle more requests and process data more efficiently.

### Partitioning Methods

##### A. Horizontal Partitioning (based on rows)
- Horizontal data partitioning involves dividing a database table into multiple partitions or shards, with each partition containing a subset of rows.
- It allows for parallel processing and faster query execution times.
- Example - Consider a social media platform that stores user data in a database table. The platform might partition the user table horizontally based on the geographic location of the users
- The key problem with this approach is that if the value whose range is used for partitioning isn’t chosen carefully, then the partitioning scheme will lead to unbalanced servers. For ex- you can take the above example only. Not all locations will be equally populated
- Range based sharding and Hash based sharding are there
##### B. Vertical Partitioning (based on columns)
- Vertical data partitioning involves splitting a database table into multiple partitions or shards, with each partition containing a subset of columns
- For example - In an ecommerce platform the name and address are stored in one shard, while order history and payment information are stored in another shard for a user 

##### C. Hybrid Partitioning
- Hybrid data partitioning combines both horizontal and vertical partitioning techniques to partition data into multiple shards.
- For example - ecommerce platform - horizontally based on the geographic location and vertically based on the type of data.
- Also each shard can be stored on a different database server


### Data Sharding Techniques

- Data sharding, a type of horizontal partitioning
- It is a technique used to distribute large datasets across multiple storage resources, often referred to as shards.
##### 1. Range-based Sharding
- Data is divided into shards based on a specific range of values for a given partitioning key.
- Example -  An e-commerce platform stores order data and decides to shard it based on order dates. Shards can be created for specific date ranges, such as monthly or yearly intervals.

##### 2. Hash-based Sharding
- It involves applying a consistent hash function to the partitioning key, which generates a hash value that determines the destination shard for each data entry
- Useful when partition key has large number of distinct values or is not easily divided into ranges.
- For example - social media website basis of  user ID
##### 3. Directory-Based Sharding 
- It uses a lookup table, often referred to as a directory, to map each data entry to a specific shard.
- It offers greater flexibility, as shards can be added, removed, or reorganized without the need to rehash or reorganize the entire dataset.
- Directory must be maintained and kept consistent. (added complexity)
##### 4. Geographical Sharding
- Geographical sharding involves partitioning data based on geographical locations
- Example - based on user country
##### 5. Dynamic Sharding
- It is an adaptive approach that automatically adjusts the number of shards based on the data’s size and access patterns.
- merging or splitting them as the data grows or shrinks.
##### 6. Hybrid Sharding: The Best of Many Worlds
- blend of multiple sharding strategies to optimize performance.
- It can achieve unprecedented efficiency levels.
- Cloud service provider - It's their secret sauce to ensure consistent, high-speed services across the board.

### Benefits of Data Partitioning
- Improved Query Performance (reduce amount of data that needs to be processed)
- Enhanced Scalability (new partitions can be added, without negatively impacting performance)
- Load Balancing (helps distribute the workload evenly across multiple storage nodes)
- Data Isolation (failure or corruption of one partition, doesn't affect other)
- Parallel Processing (multiple partitions can be accessed simultaneously)
- Storage Efficiency (more frequent used, more expensive storage resources, vice versa)
- Simplified Data Management (backup, archiving, and maintenance, manageable & efficient.)
- Better Resource Utilization (appropriate storage and processing resources (geographical))
- Improved Data Security (partitioning data based on sensitivity - patient medical record vs demographic data)
- Faster Data Recovery (focusing on one partition at a time would be faster)

### Common Problems
###### 1. Complexity
- It adds complexity to system architecture, design, and management
- Increased development and maintenance efforts, as well as a steeper learning curve for team members.
###### 2. Data Skew
- uneven data distribution across partitions
- some partitions being larger or more heavily accessed than others
- negative results - Ex - (geographical based)
###### 3. Partitioning Key Selection
- Selecting the right key requires a deep understanding of the data and its access patterns
- Otherwise data skew could happen 
###### 4. Cross-Partition Queries
- performance can suffer, as the system must search through and aggregate data from several partitions.
- reduced overall performance (compared to non-partitioned system)
###### 5. Data Migration
- Requires extra efforts while changing partitioning schemes or adding new partitions
- time-consuming and resource-intensive,
###### 6. Partition Maintenance
- Managing and maintaining partitions can be a challenging and resource-intensive task.
- repartitioning, merging, or splitting partitions (are just nightmare maybe)
- **Backup Challenges:** Performing backups isn't straightforward anymore. You need to ensure data consistency across all shards.
- **Patch Management:** When a security update rolls out, it needs to be applied across all shards, sometimes simultaneously, to maintain compatibility and security.
- **Monitoring Woes:** Instead of one set of metrics, DB administrators now need to monitor multiple, making anomaly detection a more daunting task.
###### 7. Cost
- may require additional hardware, software, or infrastructure
- added complexity of managing a partitioned system may result in higher operational expenses.







# **References**