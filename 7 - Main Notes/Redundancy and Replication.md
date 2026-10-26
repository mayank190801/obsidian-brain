
2024-07-17 09:48
Status: 
Tags:

# Redundancy and Replication

##### What is Redundancy?
- Refers to the duplication of critical components or functions to increase the reliability, availability, and fault tolerance of a system
- For example, if we have two instances of a service running in production and one fails, the system can failover to the other one.

![[Screenshot 2024-06-14 at 10.35.31 AM.png]]

##### Benefits
- Improved reliability
- Enhanced fault tolerance
- Increased availability
- Simplified maintenance (update one system while the other is accepting use requests)
- Disaster recovery (having more geographical copies of the same data)

##### What is Replication?
- It is the process of copying and synchronizing data from one database to one or more additional databases.
- primary-replica relationship between the original and the copies
- The primary server gets all the updates, which then ripple through to the replica servers.

##### Redundancy vs. Replication
- Redundancy is passive (only in case of failures), replication is active (all are used in some way or another)
- Reliability and availability, availability and integrity 
- Involed identical backup systems, synchronizing and distributing data 
- Redundancy is more about having backup resources at the ready, and replication is about keeping multiple active copies of data 

##### Replication Strategies
![[Screenshot 2024-06-14 at 12.07.32 PM.png]]
###### 1. Synchronous replication
- Immediately replicated to the replica databases before the write operation is considered complete
- reduces the risk of data loss or inconsistency
###### 2. Asynchronous replication
- the changes are queued and replicated to the replicas at a later time
- delay can result in temporary inconsistencies between the primary and replica databases
- write operations can be completed quickly
###### 3. Semi-synchronous replication
- combines elements of both synchronous and asynchronous replication
- immediately replicated to at least one replica database
- some level of strong consistency between the primary and replica databases


### Replication Methods
###### 1. Primary-Replica (Master-Slave) Replication
- one primary (master) database and one or more replica (slave) databases
- **Data Redundancy**
- Allows for load balancing by distributing read queries across multiple replicas.
- Simple to implement 
- Primary database can become bottleneck for write operations
- Replication Lag: it takes time for data to propogate to replicas
###### 2. Primary-Primary (Master-Master) Replication
- Two or more database nodes act as primary nodes
- Each node can handle both read and write operations
- Data written to one node is replicated to the other node(s), allowing each node to have an up-to-date copy of the database.
- Enhances availability, Load Distribution, No Single Point of Failure
- Conflict Resolution, Complexity, and overhead of synchronising data 
###### 3. Multi-Master Replication
- but involves more than two nodes, all capable of handling write operations.
- Similar to primary-primary 
- Complexity increase significantly, synchronisation overhead can impact performance
###### 4. Read-Replica Replication
- A variation of primary-replica replication where the replicas are specifically used for read-only operations.
- READ MORE ABOUT IT - how it different from primary-replica strategy 
###### 5. Snapshot Replication
- Involves replicating data as it appeared at a specific moment in time.
- used for replicating databases to a data warehouse for reporting.
- Useful for offloading complex queries from the operational database.
- Not suitable for applications requiring up-to-date, real-time data.
- Can be resource-intensive, depending on the size of the snapshot.
###### 6. Hybrid Replication
- Combines different replication methods to meet specific requirements.
- For example, using multi-master replication between two data centers and read-replica replication within each data center.
- Complexity increases








# **References**