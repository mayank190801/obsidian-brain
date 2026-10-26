
2024-06-27 08:37
Status: #child 
Tags: [[4 - Tags/system design|system design]] [[load balancer]] [[algorithm]]

# Load Balancer Algorithms

These below are the algorithms which are used to divide the incoming load - 

In short 
- Round Robin
- Least Connections 
- Weighted Round Robin
- Weighted Least Connections  (combines above two)
- IP Hash
- Least Response time (and fewest active connections as well)
- Random
- Least Bandwidth 
- Custom

###### 1. Round Robin
-  Distributes incoming requests to servers in a cyclic order.
-  Works well when servers have similar capacities.
- May not perform optimally when servers have different capacities or varying workloads.
- No consideration for server health or response time.
- Potentially be exploited by attackers who can observe traffic patterns

###### 2. Least Connections
- Directs incoming requests to the server with the lowest number of active connections.
- Balances load more effectively when dealing with requests that take a variable amount of time to process.
- Requires tracking the number of active connections for each server, which can increase complexity.
- May not factor in server response time or health.

###### 3. Weighted Round Robin
- Assigns different weights to servers based on their capacities. The load balancer distributes requests proportionally to these weights.
- Weights must be assigned and maintained manually.
- No consideration for server health or response time.

###### 4. Weighted Least Connections 
- It combines the Least Connections and Weighted Round Robin algorithms.
- Requires tracking active connections and maintaining server weights.
- May not factor in server response time or health.

###### 5. IP Hash
- Determines the server to which a request should be sent based on the source and/or destination IP address
- Maintains session persistence
- Can distribute load evenly when using a well-designed hash function.
- No consideration for server health, response time, or varying capacities.

###### 6. Least Response Time
- Directs incoming requests to the server with the lowest response time and the fewest active connections.
- Requires monitoring and tracking server response times and active connections
- No considerations for server health or varying capacities.

###### 7. Random
- Directs incoming requests to a randomly selected server from the available pool.
- No consideration for server health, response times, or varying capacities, session persistence.
- It dilutes the visibility of attack patterns. (DDos Attacks)

###### 8. Least Bandwidth
- Directs incoming requests to the server currently utilizing the least amount of bandwidth.
- Considers network bandwidth usage, which can be helpful in managing network resources.
- May not factor in server health, response times, or active connections.

###### 9. Custom Load
- It allows administrators to create their own load balancing algorithm based on specific requirements or conditions.
- time-consuming and complex.
- May require extensive testing to ensure optimal performance.



# **References**

[[Grokking System Design Fundamentals]]