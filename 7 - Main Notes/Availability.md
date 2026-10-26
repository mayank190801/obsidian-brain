
2024-06-27 18:26
Status: #baby
Tags: [[4 - Tags/system design|system design]] [[distributed systems]]

# Availability

- Availability is a measure of how accessible and reliable a system is to its users.
- High availability is often measured in terms of uptime, which is the ratio of time that a system is operational to the total time it is supposed to be operational.
- It also involves guaranteeing that the system can handle increased load and traffic without compromising its performance.

###### Strategies for Achieving High Availability

- High Availability through Redundancy and Replication
- Availability through Load Balancing
- Availability through Distributed Data Storage - Distributed data storage systems replicate data across geographically diverse locations, ensuring that even if one site experiences an outage, data remains accessible from other locations. 
- Availability and Consistency Models (Strong, Weak, Eventual) - Strong consistency ensures that all replicas have the same data at all times, at the cost of reduced availability and performance. Weak consistency allows for temporary inconsistencies between replicas, with the advantage of improved availability and performance. Eventual consistency guarantees that all replicas will eventually converge to the same data, providing a balance between consistency, availability, and performance.
- Availability through Health Monitoring and Alerts
- Availability through Regular System Maintenance and Updates
- Availability through Geographic Distribution - Regardless of localized incidents or natural disasters.

In this a lot of stuff could come related to Availability (Like what are the different 9s and so on, more details can come here - learn more and put it in here)

# **References**