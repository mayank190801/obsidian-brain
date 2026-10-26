
2024-06-27 09:02
Status:  #child
Tags: [[4 - Tags/system design|system design]] [[load balancer]]

# Challenges/Remedies for Load Balancer

######  1. Single Point of Failure
- Implement high availability and failover mechanisms
###### 2. Configuration Complexity
- Regularly review and update configurations, and consider using automated configuration tools
###### 3. Scalability Limitations
- Plan for horizontal or vertical scaling of the load balancer
###### 4. Latency
- Optimise load balancer performance through efficient routing algorithms and by placing the load balancer geographically close to the majority of users.
- request-response path adds an additional network hop, which can result in increased latency
- **Geographical distribution** : Deploying load balancers and backend servers in geographically distributed locations
- **Connection reuse:** It can support connection reuse or keep-alive connections, which reduce the overhead of establishing new connections between the load balancer and backend servers for each request.
- **Protocol optimisations:** support protocol optimisations, such as HTTP/2 or QUIC - reduce latency and increase throughput
###### 5. Sticky Sessions
- Employ advanced load balancing techniques that balance the need for session persistence with even traffic distribution, or redesign the application to reduce dependence on session state.
###### 6. Cost
- open-source software or cloud-based services that offer pay-as-you-go pricing models.
###### 7. Health Checks and Monitoring
- Implement comprehensive and regular health checks for backend servers




# **References**