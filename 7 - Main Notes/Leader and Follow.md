
2024-07-17 10:07
Status: 
Tags:

# Leader and Follow

Leader and Follower
- Distributed systems keep multiple copies of data
- quorum to ensure data consistency between replicas
- quorum can lead to another problem, that is, lower availability; at any time, the system needs to ensure that at least a majority of replicas are up and available, otherwise the operation will fail

#### Solution
- Allow only a single server (called leader) to be responsible for data replication and to coordinate work.
 ![[Screenshot 2024-06-18 at 7.24.14 PM.png]]

- In case the leader fails, one of the followers can become the leader. In some cases, the follower can serve read requests for load balancing.








# **References**