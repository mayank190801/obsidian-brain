
2024-07-17 10:05
Status: 
Tags:

# Distributed File Systems

#### What is a Distributed File System?
- file system that manage the storage and retrieval of data across multiple servers and locations, making the distributed nature of the storage transparent to the user
- Files are stored across multiple physical servers
- Complexities are abstracted away from the user 
- Handle large amounts of data, large number of clients (horizontal scaling)
- Gracefully handles failures, data is replicated among multiple nodes for availability and durability 
- Some provide strong consistency and some eventual consistency 
### Common Use Cases
- Cloud Storage Services (Google Cloud Storage)
- Big Data Application (Hadoop)
- Content Delivery Networks 
- High Performance Computing (large datasets to be accessed by multiple systems)\
### Examples
1. **Hadoop Distributed File System (HDFS)**: Designed to store large data sets reliably and stream them at high bandwidth to user applications.
2. **Google File System (GFS)**: Optimized for Google's own large-scale data processing needs.
3. **Microsoft Distributed File System (DFS)**: Used in Windows Server environments, allowing files distributed across multiple servers to appear as if they are in one place.
4. **Amazon Elastic File System (EFS)**: A cloud-based file storage service for use with Amazon EC2.
5. **Ceph File System (CephFS)**: A POSIX-compliant file system that uses the Ceph storage architecture to store data across a network.
### Challenges 
- Data Synchronisation (under heavy load or network partition)
- Security and Performance (slower than local file system ofc)

### Architecture of a Distributed File System

![[Screenshot 2024-06-24 at 6.14.12 AM.png]]
 - Client Interface (to access and manipulate files)
 - Metadata Servers (metadata about files, such as location information, directory structures, permissions, and file attributes.)
 - Data Nodes (Store the actual file data)
 - Replication and Redundancy Mechanism (ensures data is replicated)
 - Load Balancer (work distributed across nodes)
 - Network Infrastructure (connects all the components and facilitates the communication)
 - Synchronisation (ensures all copy are consistent)
 - Fault Tolerance (data loss or significant downtime)
 - Security (encryptions and stuff)
### Key Components of a DFS
##### Replication 
- By creating multiple copies of data across different nodes, DFS protects against data loss due to node failures.
- **Data Blocks**: Files are often divided into blocks, and each block is replicated across multiple nodes.
- **Replication Factor**: DFS usually allows configuring the replication factor, i.e., the number of replicas for each block.
- **Placement Strategy**: Intelligent placement of replicas across different nodes or racks to ensure high availability and fault tolerance.
- **Network Bandwidth**: Replication consumes network bandwidth, especially during the initial copying of data.
- **Storage Overhead**: Requires additional storage capacity for replicas.
##### Scalability 
- ensures that the DFS can grow in capacity and performance as the amount of data or the number of users increases.
- **Horizontal Scaling**: DFS scales out by adding more nodes to the system. This can be done without disrupting the service.
- **Load Distribution**: Distributes file blocks evenly across all nodes to balance the load.
- **Decentralized Design**: Avoids single points of failure and bottlenecks, allowing for seamless scaling.
- **Metadata Management**: Scaling up involves efficiently managing metadata so that it doesn't become a bottleneck.
##### Consistency 
- In DFS is about ensuring that all clients see the same data at any given time, despite data replication and concurrent modifications.
- **Consistency Models**: Different DFS implementations use different consistency models, from strict consistency to eventual consistency.
- **Versioning and Timestamps**: Used to manage updates to replicated data.
- **Locking and Synchronisation Mechanisms**: Ensuring that write operations are properly synchronised across replicas.
- **Trade-off with Performance**: Strong consistency can impact system performance and latency.
- **Handling Concurrency**: Ensuring data integrity in the presence of concurrent accesses and updates.








# **References**