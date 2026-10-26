
2024-06-27 08:35
Status: #child
Tags: [[4 - Tags/system design|system design]] [[load balancer]]

# What is Load Balancer?

- It helps distribute incoming requests and traffic evenly across multiple servers.
- It ensure high availability, reliability, and performance by avoiding overloading a single server and avoiding downtime.
- It prevent the system from becoming a single point of failure

![[Screenshot 2024-06-12 at 4.37.58 PM.png]]

**Session Persistence:** A technique used to ensure that subsequent requests from the same client are directed to the same backend server, maintaining session state and providing a consistent user experience.

**SSL/TLS Termination:** The process of decrypting SSL/TLS-encrypted traffic at the load balancer level, offloading the decryption burden from backend servers and allowing for centralized SSL/TLS management.





# **References**

[[Grokking System Design Fundamentals]]