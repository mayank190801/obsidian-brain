
2024-07-17 09:50
Status: 
Tags:

# CAP Theorem

### Introduction to CAP Theorem

- also known as Brewer's theorem
- consistency, availability, and partition tolerance.
- A distributed system can only guarantee two out of these three properties at any given time

#### 1. **Consistency:** 
- A system is considered consistent if all nodes see the same data at the same time. This means that any read operation should return the most recent write operation's result, ensuring that the system maintains a single, up-to-date version of the data. (same data everywhere!!!!!)
- Strong Consistency - Any read operation, returns the most recent write operation
- Eventual Consistency - Eventually have the same data

#### 2. **Availability:** 
- A system is considered highly available if it continues to operate and respond to requests despite failures, ensuring that every request receives a response, either a success or an error. (always available!!!!)
- Represented in terms of 99.999 and so on (use of multiple nodes)

#### 3. **Partition Tolerance:** 
- A system is considered partition-tolerant if it can continue to operate and maintain its guarantees despite network partitions, which are situations where communication between nodes in the system is interrupted or lost. 
- **Trade-offs**:
    - If a system chooses **Consistency and Partition Tolerance (CP)**, it may sacrifice availability, meaning that if a network partition happens, some users might not be able to access the data until the partition is resolved.
    - If a system chooses **Availability and Partition Tolerance (AP)**, it can lead to temporary inconsistencies in the system, where not all nodes have the same data at the same time.

 ![[Screenshot 2024-06-14 at 12.48.33 PM.png]]

 
 ## **Examples of CAP Theorem in Practice**
##### a. Consistency and Partition Tolerance (CP) Systems
- The focus is on ensuring that all nodes have the same data at the same time, even if it means sacrificing some availability during network partitions or node failures.
- Example - Google's Bigtable
- It is distributed storage system used by Google (structured data), 
- To achieve this, Bigtable uses a single-master architecture, where a master node coordinates all write operations. 
- During network partitions or master node failures, the system sacrifices availability to maintain consistency and partition tolerance.
##### b. Availability and Partition Tolerance (AP) Systems
- These systems are designed to remain operational and responsive to user requests even during network partitions or node failures, at the cost of potentially serving stale or inconsistent data.
- Example - Amazon's DynamoDB
- It is a managed NoSQL database service provided by Amazon Web Services (AWS).
- multi-master architecture and allowing eventual consistency
- It can accept write operations independently, even during network partitions
##### c. Consistency and Availability (CA) Systems
- CAP theorem implies that a distributed system must sacrifice either consistency or availability in the presence of network partitions
- some systems prioritize consistency and availability in environments where network partitions are rare or can be quickly resolved.
- Examples - Tradition Relation Database( MySQL / PostreQL )
- These systems use transactions and ACID (Atomicity, Consistency, Isolation, Durability) properties to ensure data consistency.
- Not built to handle network partitions gracefully and may experience reduced availability or performance during such events.

Then my question is how, they are supporting consistency and availability ?  We are just expecting that network partitioning will be rare?? That's it??? 

### Beyond CAP Theorem

##### a. Extended CAP (ECAP) Model
- consistency, availability, partition tolerance, and latency
-  impossible to optimize for all four properties
##### b. PACELC Theorem
- Partition (P), Availability (A), Consistency (C), Else (E), Latency (L), Consistency (C).
- theorem states that in case of a network partition, a system must choose between availability and consistency (similar to CAP), but when the system is operating normally (no partitions), it must choose between latency and consistency.
##### c. CRDTs and Hybrid Systems
- Convergent Replicated Data Types (CRDTs) are data structures designed to allow multiple replicas to be updated independently and converge to a consistent state without requiring coordination.
- achieve both strong eventual consistency and high availability










# **References**