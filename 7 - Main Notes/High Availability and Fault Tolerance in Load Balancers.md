
2024-06-27 08:53
Status: #baby 
Tags: [[[4 - Tags/system design|system design]] [[load balancer]]

# High Availability and Fault Tolerance in Load Balancers

**Active-passive configuration:**
- one load balancer (the active instance) handles all incoming traffic while the other (the passive instance) remains on standby.
- does not utilize the resources of the passive instance during normal operation.

**Active-active configuration:**
- multiple load balancer instances actively process incoming traffic simultaneously.
- If one instance fails, the others continue to process traffic with minimal disruption.

**Health checks and monitoring**
 - have health checks, for load balancer to remove unused servers 
 - Monitor stats so that the issues can be seen beforehand 
 - Alerting should be there, incase anything goes wrong 

**Synchronization and State Sharing** (Requires deep understanding of how this works)
 - crucial to ensure that the load balancer instances maintain a consistent view of the system's state, including the status of backend servers, session data, and other configuration settings.
 - **Centralized configuration management:**  centralized configuration store (e.g., etcd, Consul, or ZooKeeper) to maintain and distribute configuration data
 - **State sharing and replication:** database replication, distributed caching systems (e.g., Redis or Memcached), or built-in state-sharing mechanisms



# **References**