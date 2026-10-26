
2024-06-27 08:57
Status: #baby 
Tags: [[4 - Tags/system design|system design]] [[load balancer]]

# Scalability and Performance in Load balancer

**Horizontal scaling**
- active-active configurations,
- achieved using DNS load balancing or by implementing an additional load balancer layer

**Vertical Scaling**
- increasing the resources
- limited by the maximum capacity of a single instance

###### Connection and request rate limits
- Load balancers can enforce rate limits based on various criteria, such as IP addresses, client domains, or URL patterns. 
- Implementing these limits can also help mitigate the impact of Denial of Service (DoS) attacks and prevent individual clients from monopolizing resources.

###### Caching and content optimisation
- cache static content
- compression or magnification, which can further improve performance and reduce bandwidth consumption.




# **References**