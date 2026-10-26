 [Course Link](https://www.designgurus.io/course/grokking-system-design-fundamentals)

## System Design Fundamentals 
 
 Requires Deep Understanding of **Load Balancing**, **Caching**, **Partitioning**, **Replication**, **Databases**, and **Proxies**.

#### Load balancing

It helps distribute incoming requests and traffic evenly across multiple servers.
It ensure high availability, reliability, and performance by avoiding overloading a single server and avoiding downtime.
It prevent the system from becoming a single point of failure

![[Screenshot 2024-06-12 at 4.37.58 PM.png]]

**Session Persistence:** A technique used to ensure that subsequent requests from the same client are directed to the same backend server, maintaining session state and providing a consistent user experience.

**SSL/TLS Termination:** The process of decrypting SSL/TLS-encrypted traffic at the load balancer level, offloading the decryption burden from backend servers and allowing for centralized SSL/TLS management.

##### Load Balancing Algorithms:

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

##### Uses of Load Balancing 
 - Improving website performance
 - Ensuring high availability and reliability
 - Scalability
 - Redundancy 
 - Network Optimization 
 - Geographic Distribution 
 - Application Performance (less request on each server then before since caching and lot of stuff it can handle)
 - Security (Against DDos Attacks, by distributing traffic among multiple servers)
 - Cost Savings
 - Content Caching 


##### Load Balancer Types (later figure it out) 
- [[Hardware Load Balancing]]
- [[Software Load Balancing]]
- [[Cloud-Based Load Balancing]] 
- DNS Load Balancing 
- Global Server Load Balancing 
- Hybrid Load Balancing 
- Layer 4 Load Balancing 
- Layer 7 Load Balancing 


#####  Stateless vs. Stateful Load Balancing (pretty simple)

Stateless
- It operate without maintaining any information about the clients' session or connection state.
- They make routing decisions based solely on the incoming request data, such as the client's IP address, request URL, or other headers.
- quickly and efficiently

Ex -  A stateless load balancer can allocate requests to servers based on the user's geographic location, without retaining any session data.

Stateful 
- It preserves session information between requests.
- It assigns a client to a specific server and ensures that all subsequent requests from the same client are directed to that serve
- Two types - Source IP Affinity and Session Affinity

1. Source IP Affinitiy 
	- It assigns a client to a specific server based on the client's IP address.
	- Issues if the client's IP address frequently changes, such as in mobile networks.

2. Session Affinity
	- It allocates a client to a specific server based on a session identifier, such as a cookie or URL parameter.
	- No issues even if client's IP address changes in future 

##### High Availability and Fault Tolerance

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

**Synchronization and State Sharing** (might have to come later to this)
 - crucial to ensure that the load balancer instances maintain a consistent view of the system's state, including the status of backend servers, session data, and other configuration settings.
 - **Centralized configuration management:**  centralized configuration store (e.g., etcd, Consul, or ZooKeeper) to maintain and distribute configuration data
 - **State sharing and replication:** database replication, distributed caching systems (e.g., Redis or Memcached), or built-in state-sharing mechanisms

#####  Scalability and Performance

**Horizontal scaling:**
- active-active configurations,
- achieved using DNS load balancing or by implementing an additional load balancer layer

Vertical Scaling: 
- increasing the resources
- limited by the maximum capacity of a single instance

###### Connection and request rate limits
- Load balancers can enforce rate limits based on various criteria, such as IP addresses, client domains, or URL patterns. Implementing these limits can also help mitigate the impact of Denial of Service (DoS) attacks and prevent individual clients from monopolizing resources.

###### Caching and content optimization
- cache static content
-  compression or minification, which can further improve performance and reduce bandwidth consumption.

###### Impact of load balancers on latency

- request-response path adds an additional network hop, which can result in increased latency
- **Geographical distribution** : Deploying load balancers and backend servers in geographically distributed locations
- **Connection reuse:** It can support connection reuse or keep-alive connections, which reduce the overhead of establishing new connections between the load balancer and backend servers for each request.
- **Protocol optimizations:** support protocol optimizations, such as HTTP/2 or QUIC - reduce latency and increase throughput


#####  Challenges of Load Balancers (direct points and their remedies are good enough)

######  1. Single Point of Failure
- Implement high availability and failover mechanisms
###### 2. Configuration Complexity
- Regularly review and update configurations, and consider using automated configuration tools
###### 3. Scalability Limitations
- Plan for horizontal or vertical scaling of the load balancer
###### 4. Latency
- Optimize load balancer performance through efficient routing algorithms and by placing the load balancer geographically close to the majority of users.
###### 5. Sticky Sessions
- Employ advanced load balancing techniques that balance the need for session persistence with even traffic distribution, or redesign the application to reduce dependence on session state.
###### 6. Cost
- open-source software or cloud-based services that offer pay-as-you-go pricing models.
###### 7. Health Checks and Monitoring
- Implement comprehensive and regular health checks for backend servers



#### Introduction to API Gateway

An API Gateway is a server-side architectural component in a software system that acts as an intermediary between clients (such as web browsers, mobile apps, or other services) and backend services, microservices, or APIs.

- single entry point for external consumers to access the services
- responsible for tasks such as routing, authentication, and rate limiting
- enables microservices to focus on their individual tasks


![[Screenshot 2024-06-13 at 9.35.21 AM.png]]

##### Main difference betwen API Gateway and Load Balancer 

- An API gateway is focused on **routing** requests to the appropriate microservice, while a load balancer is focused on **distributing** requests evenly across a group of backend servers.
- These requests specific URL that identifies the API that the client is trying to access, and the API gateway routes the request to the appropriate microservice based on this URL. 
- A load balancer used to handle requests that are sent to a single, well-known IP address, and then routes them to one of many possible backend servers based on factors such as server performance and availability.

##### Usage of API gateway (tons of usages)
- Routing (help in simplying the overall system design) - remember that always!
- Rate limiting and throttling
- Caching
- Authentication and Authorization
- Load balancing
- Monitoring
- Transformation
- Request and response validation
- Circuit breaker (circuit breaker pattern, prevents single failed microservice from bring down the entire system) - (can more in depth)
- Service discovery (Gateway have to know the location of microservice, not clients)
- API Versioning
- Error Handling
- Service Aggregation (can combine responses from multiple backend services into a single response )
- Web Application Firewall (WAF) (prevents backend services from SQL injection, cross-site scripting (XSS), or distributed denial-of-service (DDoS) attacks.)
- API Documentation

Pros are same as above, and cons are similar to load balancer - Single point of failure, latency, vendor lockin, cost, maintenance overhead and complexity to setup

#### Key Characteristics of Distributed Systems 

##### 1. Scalability 

Scalability is the ability of a system to handle an increasing workload, either by adding more resources (scaling out) or by upgrading the capacity of existing resources (scaling up).

Horizontal  (ex -  Cassandra and MongoDB)
Vertical       (ex - MySQL)

##### 2. Availability

Availability is a measure of how accessible and reliable a system is to its users.

High availability is often measured in terms of uptime, which is the ratio of time that a system is operational to the total time it is supposed to be operational.

 It also involves guaranteeing that the system can handle increased load and traffic without compromising its performance.

###### Strategies for Achieving High Availability

- High Availability through Redundancy and Replication
- Availability through Load Balancing
- Availability through Distributed Data Storage - Distributed data storage systems replicate data across geographically diverse locations, ensuring that even if one site experiences an outage, data remains accessible from other locations. 
- Availability and Consistency Models (Strong, Weak, Eventual) - Strong consistency ensures that all replicas have the same data at all times, at the cost of reduced availability and performance. Weak consistency allows for temporary inconsistencies between replicas, with the advantage of improved availability and performance. Eventual consistency guarantees that all replicas will eventually converge to the same data, providing a balance between consistency, availability, and performance.
- Availability through Health Monitoring and Alerts
- Availability through Regular System Maintenance and Updates
- Availability through Geographic Distribution - Regardless of localized incidents or natural disasters.

##### 3. Latency and Performance

A. Data Locality
- Minimize the amount of data that needs to be transferred between nodes
- Storing related data close together
- Techniques to achieve data locality include data partitioning, sharding, and data replication.

B. Load Balancing
- helps to optimize resource utilization, minimize response times, and prevent system overloads.

C. Caching Strategies
- Common caching strategies include in-memory caching, distributed caching, and content delivery networks (CDNs).

##### 4. Concurrency and Coordination

A. Concurrency Control

Primary Goal : Manage access to shared resources (like data or hardware resources) in an environment where multiple processes or threads are executing simultaneously.

Focus : It is concerned with how to handle situations where multiple processes need to access or modify shared data at the same time.

- **Locking:** Locks are used to restrict access to shared resources or data, ensuring that only one process can access them at a time.
- **Optimistic concurrency control:** This approach assumes that conflicts are rare and allows multiple processes to work simultaneously. Conflicts are detected and resolved later, usually through a validation and rollback mechanism.
- **Transactional memory:** This technique uses transactions to group together multiple operations that should be executed atomically, ensuring data consistency and isolation.

 B. Synchronization

Primary Goal: It is to coordinate the timing of multiple concurrent processes or threads. It's about managing the execution order and timing of processes to ensure correct operation.

Focus : It ensures that concurrent processes execute in a way that respects certain timing constraints, like making sure certain operations happen before others or that operations do not interfere destructively with one another.

(go deeper into all these once - useChatGPT)
- **Barriers:** Barriers are used to synchronize the execution of multiple processes or threads, ensuring that they all reach a specific point before proceeding.
- **Semaphores:** Semaphores are signaling mechanisms that control access to shared resources and maintain synchronization among multiple processes or threads.
- **Condition variables:** Condition variables allow processes or threads to wait for specific conditions to be met before proceeding with their execution.

C. Coordination Services

- specialized components or tools that help manage distributed systems' complexity by providing a set of abstractions and primitives
- for tasks like configuration management, service discovery, leader election, and distributed locking
- Ex - Apache ZooKeeper, etcd, and Consul.

D. Consistency Models

Consistency models are fundamental in distributed systems, defining the rules for how and when changes made by one operation (like a write) become visible to other operations (like reads).

1. Strong Consistency
- **Definition**: After a write operation completes, any subsequent read operation will immediately see the new value.
- **Example**: Traditional relational databases (RDBMS) like MySQL or PostgreSQL typically offer strong consistency. If a record is updated in one transaction, any subsequent transaction will see that update.

2. Eventual Consistency
- **Definition**: Over time, all accesses to a particular data item will eventually return the last updated value. The time it takes to achieve consistency after a write is not guaranteed.
- **Example**: Amazon's DynamoDB uses eventual consistency. If you update a data item, the change might not be immediately visible to all users, but it will eventually propagate to all nodes.

3. Causal Consistency ( not  much clarity on this one )
- **Definition**: Operations that are causally related are seen by all processes in the same order. Concurrent operations might be seen in a different order on different nodes.
- **Example**: In a social media app, if a user posts a message and then comments on that post, any user who sees the comment must also see the original post.

4. Read-Your-Writes Consistency 
- **Definition**: Guarantees that once a write operation completes, any subsequent reads (by the same client) will see that write or its effects.
- **Example**: A user profile update in a web application. Once the user updates their profile, they immediately see the updated profile data.

5. Session Consistency
- **Definition**: A stronger version of read-your-writes consistency. It extends this guarantee to a session of interactions, ensuring consistency within the context of a single user session.
- **Example**: In an e-commerce site's shopping cart, items added to the cart in a session will be consistently visible throughout that session.

6. Sequential Consistency
- **Definition**: Operations from all nodes or processes are seen in the same order. There is a global order of operations, but it doesn't have to be real-time.
- **Example**: A distributed logging system where logs from different servers are merged into a single, sequentially consistent log.

 7. Monotonic Read Consistency
- **Definition**: Ensures that if a read operation reads a value of a data item, any subsequent read operations will never see an older value.
- **Example**: A user checking a flight status on an airline app will not see a departure time that goes back in time; it will only move forward.

8. Linearizability (Strong Consistency)
- **Definition**: A stronger version of sequential consistency, it ensures that all operations are atomic and instantly visible to all nodes.
- **Example**: In a distributed key-value store, once a new value is written to a key, any read operation on any node immediately reflects this change.


##### 5. Monitoring and Observability

###### A. Metrics Collection
- Collecting and analyzing metrics, such as latency, throughput, error rates, and resource utilization, can help identify performance bottlenecks, potential issues, and areas for improvement.
- Tools - Prometheus, Graphite, or InfluxDB

###### B. Distributed Tracing
- technique for tracking and analyzing requests as they flow through a distributed system
- allow you to understand the end-to-end performance and identify issues in specific components or services.
- Tools - Jaeger, Zipkin, or OpenTelemetry

###### C. Logging
-  Collecting, centralizing, and analyzing logs from all services and nodes in a distributed system can provide valuable insights into system behavior
- Tools - Elasticsearch, Logstash, and Kibana (ELK Stack) or Graylog

###### D. Alerting and Anomaly Detection
- Tools like Grafana, PagerDuty, or Sensu can help you set up alerting and anomaly detection for your distributed system.

###### E. Visualization and Dashboards
- make data-driven decisions
- Tools like Grafana, Kibana, or Datadog for customizable dashboards


#### 6. Resilience and Error Handling

 It help minimize the impact of failures and ensure that the system can recover gracefully from unexpected events.

###### A. Fault Tolerance
- It is the ability of a system to continue functioning correctly in the presence of faults or failures.
- incorporating redundancy at various levels (data, services, nodes) and implementing strategies like replication, sharding, and load balancing 
###### B. Graceful Degradation
- It is the ability of a system to continue providing limited functionality when certain components or services fail.
- Techniques like circuit breakers, timeouts, and fallbacks can be employed
###### C. Retry and Backoff Strategies
- In distributed systems, transient failures like network issues, timeouts, or service unavailability are common.
- Automatically reattempting failed operations with an increasing delay between retries
###### D. Error Handling and Reporting
- By consistently handling and logging errors, categorizing them, and generating alerts when necessary, you can quickly identify and diagnose problems in the system.
###### E. Chaos Engineering
- Disney + Hotstar uses this technique a lot 
- It is the practice of intentionally injecting failures into a distributed system to test its resilience and identify weaknesses.
- Tools - Chaos Monkey or Gremlin


##### 7. Fault Tolerance vs. High Availability

Fault tolerance is about uninterrupted operation even in the face of component failures, while high availability is about keeping the overall system operational as much as possible.

Approach 
- It involves redundancy and. automatic failover mechanisms
- It focuses on preventing downtime through redundant resources and rapid recovery strategies 

Downtime 
- No downtime even when failure 
- Minimal downtime, but some interruptions are acceptable (based on the 99.99 selected)

Cost 
- More expensive, and more complex due to the need for exact replicas and seemless failover
- More cost effective, depends on the level of availability 

Data Integrity 
- Maintains data integrity 
- Prioritizes system uptime, with potential for minimal data loss in certain failure conditions 


### Network Essentials

#### HTTP vs. HTTPS

HTTP
1. **No Encryption**: HTTP does not encrypt the data being transmitted. This means that the data can be intercepted and read by others.
2. **Default Port**: It typically operates over port 80.
3. **Vulnerabilities**: More vulnerable to man-in-the-middle attacks and eavesdropping.

HTTPS
1. **Encryption**: HTTPS encrypts the data being transmitted using protocols like SSL (Secure Sockets Layer) or TLS (Transport Layer Security). This encryption ensures that even if the data is intercepted, it cannot be easily read by attackers.
2. **Default Port**: It operates over port 443.
3. **Trustworthiness**: Websites with HTTPS are generally trusted more by users. Browsers often mark HTTP sites as 'Not Secure'.

###### Key Differences:

1. **Security**: The most significant difference is security. HTTPS provides a secure layer through encryption, while HTTP does not.
2. **Performance**: HTTPS may cause slightly more server load due to the encryption and decryption process.
3. **SEO Ranking**: Search engines like Google give preference to HTTPS websites, considering them more secure.
4. **Certificate Requirement**: To implement HTTPS, a website must obtain an SSL/TLS certificate from a Certificate Authority (CA).

#### TCP vs. UDP

- **TCP** is a connection-oriented protocol that ensures reliable, ordered, and error-checked delivery of a stream of bytes between applications.
- **UDP** is a connectionless protocol that sends messages, called datagrams, without establishing a prior connection and without guaranteeing reliability or order.

TCP (Transmission Control Protocol)
- **Reliability**: TCP ensures that data is delivered accurately and in order, retransmitting lost or corrupted packets.
- **Connection-Oriented**: Establishes a connection between sender and receiver before transmitting data.
- **Flow Control**: Manages data transmission rate to prevent network congestion.
- **Congestion Control**: Adjusts the transmission rate based on network traffic conditions.
- **Acknowledgements and Retransmissions**: Uses acknowledgments to confirm receipt of data and retransmits if necessary.
- Applications where reliability and order are critical, like web browsing (HTTP/HTTPS), email (SMTP, POP3, IMAP), and file transfers (FTP).

UDP (User Datagram Protocol)
- **Low Overhead**: Does not establish a connection, leading to lower overhead and latency.
- **Unreliable Delivery**: Does not guarantee message delivery, order, or error checking.
- **Speed**: Faster than TCP due to its simplicity and lack of retransmission mechanisms.
- **No Congestion Control**: Does not reduce transmission rates under network congestion.
- Applications that require speed and can tolerate some loss of data, like streaming video or audio, online gaming, or VoIP (Voice over Internet Protocol).

###### Key Differences
- Reliability - (accurately and in order, maybe lost or arrive out of order)
- Connection - (establishes a connection, without establishing a connection)
- Speed - (slower due to handshake, retransmission and congestion control, no overhead just fast)
- Data Integrity - (high data integrity, lower data integrity)
- Use case - (data accuracy, speed is more critical)

#### URL vs. URI vs. URN

URL - (Uniform Resource Locator)
URI - (Uniform Resource Identifier)
URN - (Uniform Resource Name)

- **URL**: Specifies both the identity and the location of a resource (How and Where).
- **URI**: A more comprehensive term covering both URLs (identifying and locating) and URNs (just identifying).
- **URN**: Focuses only on uniquely identifying a resource, not on where it is located or how to access it.

### Introduction to DNS

- Domain Name System, is a system used to translate human-readable domain names (e.g., [www.designgurus.com](http://www.designgurus.com/)) into IP addresses (e.g., 198.47.25.1) that computers can understand.
- In simple terms, DNS acts like a phonebook for the internet, allowing users to access websites using easy-to-remember domain names instead of having to memorize numeric IP addresses.

##### Purpose and Importance

- **User-friendliness** 
- **Scalability:** DNS is a distributed and hierarchical system, allowing it to handle the ever-growing number of domain names and IP addresses on the internet.
- **Flexibility:** DNS allows websites to change their IP addresses without affecting users. When a website's IP address changes, the DNS records are updated, and users can continue accessing the site using the same domain name.
- **Load balancing:** DNS can distribute user requests across multiple servers, improving the performance and reliability of websites.

##### Components and Terminology

1. Domain names, TLDs (Top-Level Domains), and subdomains

A domain name is a human-readable address used to access a website or other resources on the internet. Ex- www.example.com

A top-level domain (TLD) is the rightmost part of a domain name, such as ".com" in [www.example.com](http://www.example.com/).
- generic TLDs (.com, .org, .net)
- country-code TLDs (.in, .uk)

A subdomain is a subdivision of a domain name, allowing the creation of separate sections or areas within a website. Ex -  blog.example.com, where "blog" is the subdomain of example.com.

 2. DNS servers: Root, TLD, and Authoritative Name Servers

Root servers are the highest level of DNS servers and are responsible for directing queries to the appropriate TLD servers. There are 13 root server clusters worldwide, managed by various organizations, each having multiple servers for redundancy and reliability.

TLD servers store information about domain names within their specific TLD. When they receive a query, they direct it to the appropriate authoritative name server responsible for that domain.

These servers hold the actual DNS records for a domain, including its IP address and other information. They provide the final answer to DNS queries, allowing users to access the desired website or resource.

3. DNS resolvers (caching and forwarding)

**DNS resolvers:** Also known as recursive resolvers, DNS resolvers are usually provided by internet service providers (ISPs) or other organizations. They act as intermediaries between users and DNS servers, receiving DNS queries from users and sending them to the appropriate DNS servers to be resolved. Once the resolver receives the answer, it caches the information and returns it to the user.

**Caching resolver:** A caching resolver stores previously resolved queries in its cache, speeding up the resolution process for future requests. If the requested information is available in the cache, the caching resolver returns the answer directly without contacting other DNS servers.

**Forwarding resolver:** A forwarding resolver forwards DNS queries to another resolver, which is typically a caching resolver, instead of contacting DNS servers directly. This setup allows for better control, security, and performance.


### DNS Resolution Process

![[Screenshot 2024-06-13 at 1.54.46 PM.png]]

 
 The DNS resolution process involves a series of recursive and iterative queries, utilizing a distributed and hierarchical infrastructure of DNS servers, resolvers, and caching mechanisms

- **Recursive query:** In a recursive query, the DNS resolver asks for the complete answer to a query from the DNS server. If the server has the answer, it responds with the required information. If not, the server takes responsibility for contacting other DNS servers to find the answer and then returns it to the resolver. Recursive queries put more responsibility on the DNS server to find the requested information.

- **Iterative query:** In an iterative query, the DNS resolver asks the DNS server for the best answer it has at the moment. If the server doesn't have the complete answer, it responds with a referral to another server that might have more information. The resolver then contacts that server with a new iterative query, repeating the process until it finds the complete answer. In iterative queries, the resolver takes on more responsibility for finding the requested information.

- Resolvers and servers cache the results of previous queries to speed up the resolution process, with TTL values determining how long the records are stored. 

- Negative caching helps improve performance by caching the non-existence of DNS records.

#### DNS Load Balancing and High Availability

###### 1. Round-robin DNS
- It is a simple load balancing technique in which multiple IP addresses are associated with a single domain name.
- It can lead to uneven load distribution or increased latency in some cases.

###### 2. Geographically distributed DNS servers
- Distributing DNS servers across different regions, they can provide faster and more reliable DNS resolution for users located closer to a server.
- It also offer increased redundancy, if one become unreachable, user can still access the service.

###### 3. Anycast routing
- It is a networking technique that allows multiple servers to share the same IP address
- The network routes the query to the nearest server, based on factors like network latency and server availability.
- **Load balancing:** Anycast distributes DNS queries among multiple servers, preventing any single server from becoming a bottleneck.
- **Reduced latency:** By directing users to the nearest server, anycast can significantly reduce the time it takes for DNS resolution.
- **High availability:** If a server fails or becomes unreachable, anycast automatically redirects queries to the next closest server, ensuring uninterrupted service.

###### 4. Content Delivery Networks (CDNs) and their relation to DNS

DNS plays a crucial role in the functioning of CDNs. When a user requests content from a website using a CDN, the CDN's DNS server determines the best server to deliver the content based on the user's location and other factors. The DNS server then responds with the IP address of the chosen server, allowing the user to access the content quickly and efficiently.

## Caching 

### Introduction to Caching 

#### What is Caching?

- The cache is a high-speed storage layer that sits between the application and the original source of the data
- Used for various types of data, such as web pages, database queries, API responses, images, and videos.
- Implemented in various ways, including in-memory caching, disk caching, database caching, and CDN caching.

**1. Cache:** A temporary storage location for data or computation results, typically designed for fast access and retrieval.
**2. Cache eviction:** The process of removing data from the cache, typically to make room for new data or based on a predefined cache eviction policy.
**3. Cache staleness:** When the data in the cache is outdated compared to the original data source.

#### Why is Caching Important?
- Reduced Latency 
- Improved System Performance 
- Reducing Network Load 
- Increased Scalability 
- Better User Experience 

#### Types of Caching

![[Screenshot 2024-06-13 at 1.42.42 PM.png]]

###### 1. In-memory caching
- In-memory caching stores data in the main memory of the computer, which is faster to access than disk storage. This type of caching is commonly used for caching API responses, session data, and web page fragments. 
- Tools - Memcached or Redis or implementing custom caching logic within the application code.
###### 2. Disk caching
- Disk caching stores data on the hard disk, which is slower than main memory but faster than retrieving data from a remote source. Disk caching is useful for data that is too large to fit in memory or for 
- data that needs to persist between application restarts. 
- This type of caching is commonly used for caching database queries and file system data.
###### 3. Database caching
- Database caching stores frequently accessed data in the database itself, reducing the need to access external storage. 
- This type of caching is useful for data that is stored in a database and frequently accessed by multiple users. 
- Database caching can be implemented using a variety of techniques, including database query caching and result set caching.

###### 4. Client-side caching

This type of caching occurs on the client device, such as a web browser or mobile app. Client-side caching stores frequently accessed data, such as images, CSS, or JavaScript files, to reduce the need for repeated requests to the server. Examples of client-side caching include browser caching and local storage.

###### 5. Server-side caching

This type of caching occurs on the server, typically in web applications or other backend systems. Server-side caching can be used to store frequently accessed data, precomputed results, or intermediate processing results to improve the performance of the server. Examples of server-side caching include full-page caching, fragment caching, and object caching.

###### 6. CDN caching

CDN caching stores data on a distributed network of servers, reducing the latency of accessing data from remote locations. This type of caching is useful for data that is accessed from multiple locations around the world, such as images, videos, and other static assets. CDN caching is commonly used for content delivery networks and large-scale web applications.

###### 7. DNS caching

DNS caching improves the performance of the DNS system by reducing the number of requests made to DNS servers. When a DNS server receives a request for a domain name, it checks its local cache to see if it has the IP address for that domain name. If the IP address is in the cache, the DNS server can immediately respond with the IP address without having to query other servers. 


![[Screenshot 2024-06-13 at 1.58.23 PM.png]]

### Cache Replacement Policies

###### 1. Least Recently Used (LRU)
###### 2. Least Frequently Used (LFU)
###### 3. First In, First Out (FIFO)
###### 4. Random Replacement  (when patterns are unpredictable)

Trade-off between performance and complexity.
- As LRU and LFU performs better, but requires additional data structures
- Where as FIFO and random performs less effective, but are easier to implement

### Cache Invalidation

 If the data is modified in the database, it should be invalidated in the cache; if not, this can cause inconsistent application behavior.

###### 1. Write-through cache
- Under this scheme, Data is written into the cache and the corresponding database simultaneously. 
- The cached data allows for fast retrieval 
- Complete data consistency between the cache and the storage
- Nothing will get lost in case of a crash, power failure, or other system disruptions. 
- Every write operation must be done twice before returning success to the client
- higher latency for write operations.

###### 2. Write-around cache
- Data is written directly to permanent storage, bypassing the cache.
- Reduce the cache being flooded with write operations that will not subsequently be re-read
- Disadvantage that a read request for recently written data will create a “cache miss”

###### 3. Write-back cache
- Data is written to cache alone, and completion is immediately confirmed to the client.
- Write to the permanent storage is done when the system needs some free space
- Low-latency and high-throughput for write-intensive applications
- Risk of data loss

###### 4. Write-behind cache
- Data is written to the cache and acknowledged to the application immediately, but it is not immediately written to the permanent storage.
- Eventually written to the permanent storage at specified intervals.

#### Cache Invalidations Methods

###### Purge
- The purge method removes cached content for a specific object, URL, or a set of URLs. It’s typically used when there is an update or change to the content and the cached version is no longer valid.
- When a purge request is received, the cached content is immediately removed, and the next request for the content will be served directly from the origin server.

###### Refresh
- Fetches requested content from the origin server, even if cached content is available. When a refresh request is received, the cached content is updated with the latest version from the origin server, ensuring that the content is up-to-date. 
- Unlike a purge, a refresh request doesn’t remove the existing cached content; instead, it updates it with the latest version.

###### Ban
- The ban method invalidates cached content based on specific criteria, such as a URL pattern or header. 
- When a ban request is received, any cached content that matches the specified criteria is immediately removed, and subsequent requests for the content will be served directly from the origin server.

(What is the difference between Ban and Purge in that case???)
###### Time-to-live (TTL) expiration
- This method involves setting a time-to-live value for cached content, after which the content is considered stale and must be refreshed. 
- When a request is received for the content, the cache checks the time-to-live value and serves the cached content only if the value hasn’t expired. 
- If the value has expired, the cache fetches the latest version of the content from the origin server and caches it.

###### Stale-while-revalidate
- This method is used in web browsers and CDNs to serve stale content from the cache while the content is being updated in the background. 
- When a request is received for a piece of content, the cached version is immediately served to the user, and an asynchronous request is made to the origin server to fetch the latest version of the content. 
- Once the latest version is available, the cached version is updated. 
- This method ensures that the user is always served content quickly, even if the cached version is slightly outdated.

### Cache Read Strategies

![[Screenshot 2024-06-13 at 2.47.00 PM.png]]

### Cache Coherence and Consistency Models

These models ensure that data remains accurate and up-to-date across multiple caches or processing units.

#### Cache Coherence (write in your own language)

It is a property of multi-core processors or distributed systems that ensures all processors or nodes see the same view of shared data.

 In a system with multiple caches, each cache may store a local copy of the shared data. When one cache modifies its copy, it is essential that all other caches are aware of the change to maintain a consistent view of the data.
 
To achieve cache coherence : 

- **Write-invalidate:** When a cache writes to its copy of the shared data, it broadcasts a message to other caches, invalidating their copies. When another cache requires the updated data, it fetches the new data from the memory or the cache that made the change.

- **Write-update (or write-broadcast):** When a cache writes to its copy of the shared data, it broadcasts the updated data to all other caches, which update their local copies accordingly.

#### Cache Consistency Models

- **Strict Consistency:** In this model, any write to a data item is instantly visible to all caches. This model provides the highest level of consistency but is difficult to achieve in practice, as it may require significant synchronization overhead and negatively impact performance.

- **Sequential Consistency:** In this model, all operations on data items appear to occur in a specific sequential order across all caches. While this model allows for better performance than strict consistency, it still requires considerable synchronization and may not be practical in many distributed systems.

- **Causal Consistency:** In this model, operations that are causally related (i.e., one operation depends on the outcome of another) are guaranteed to appear in order across all caches. Operations that are not causally related can occur in any order. This model provides better performance than sequential consistency while still ensuring a reasonable level of data accuracy.

- **Eventual Consistency:** In this model, all updates to a data item will eventually propagate to all caches, **but there is no guarantee about the order or timing of the updates**. This model offers the best performance among the consistency models but provides the weakest consistency guarantees. Eventual consistency is often used in distributed systems where performance and scalability are prioritized over strict data accuracy.

### Caching Challenges

##### 1. Thundering Herd
- The thundering herd problem occurs when a popular piece of data expires from the cache, leading to a sudden surge in requests to the origin server to fetch the missing data.
- Solved using staggered expiration times, implementing a cache lock, or using background updates to refresh the cache before the data expires.
##### 2. Cache Penetration
- Cache penetration refers to the situation where requests for data bypass the cache and directly access the origin server, reducing the benefits of caching. 
- This typically happens when requests are made for non-existent or rarely accessed data. 
- To mitigate cache penetration, negative caching (caching negative responses) or using a bloom filter to check for the existence of data before querying the cache can be employed.
##### 3. Big Key
- A big key is a large piece of data that consumes a significant portion of the cache's capacity. Storing big keys can lead to cache evictions, reducing the overall effectiveness of the caching system. 
- Solutions for handling big keys include compressing the data before caching, breaking the data into smaller chunks, or using a separate caching strategy specifically designed for large objects.
##### 4. Hot Key
- A hot key refers to a piece of data that is frequently accessed, causing contention and performance issues in the caching system. 
- Solutions are using consistent hashing to distribute the load more evenly, replicating the hot key across multiple cache nodes, or implementing a load balancing strategy to distribute requests across multiple instances of the hot key.

##### 5. Cache Stampede (or Dogpile)
- Cache stampede occurs when multiple requests for the same data are made simultaneously, causing excessive load on the cache and the origin server. 
- Solved by combining multiple requests for the same data into a single request or implementing a read-through cache, where the cache itself fetches the missing data from the origin server.
##### 6. Cache Pollution
- Cache pollution occurs when less frequently accessed data displaces more frequently accessed data in the cache, leading to a reduced cache hit rate. 
- Use LRU or LFU 
##### 7. Cache Drift
- Cache drift refers to the inconsistency between cached data and the data on the origin server, typically caused by updates or changes in the data. 
- Use proper cache invalidation strategies 

#### Cache Performance Metrics

- Hit rate
- Miss rate
- Cache size
- Cache latency


## CDN 
#### What is CDN?

A Content Delivery Network (CDN) is a **distributed network of servers** strategically located across various geographical locations to deliver web content, such as images, videos, and other static assets, more efficiently to users.

#### How CDN Works??

- The request is routed to the nearest CDN server (also known as an edge server) based on factors such as network latency and server load.
- If cached, then well and good, otherwise edge server fetches the content from origin server
- Helps in offloading traffic from origin server 

![[Screenshot 2024-06-13 at 3.23.13 PM 1.png]]

#### Key terminology and concepts

**1. Point of Presence (PoP):** A PoP is a physical location where CDN servers are deployed, typically in data centers distributed across various geographical locations. PoPs are strategically placed close to end-users to minimize latency and improve content delivery performance.

**2. Cache Warming:** Cache warming is the process of preloading content into the edge server's cache before it is requested by users, ensuring that the content is available for fast delivery when it is needed.

**3. Anycast:** Anycast is a network routing technique used by CDNs to direct user requests to the 
nearest available edge server, based on the lowest latency or the shortest network path.

#### Benefits of using a CDN

**1. Reduced latency:** 
**2. Improved performance:**
**3. Enhanced reliability and availability:**
**4. Scalability:** 
**5. Security:** 

While the origin server is the source of the original content, edge servers play a crucial role in optimizing content delivery to end-users by caching content closer to where users are located. This architecture significantly improves website performance, reduces latency, and enhances user experience, especially for websites with a global audience.

#### CDN Routing and Request Handling

- **Anycast Routing:** In anycast routing, multiple edge servers share a single IP address. When a user sends a request to that IP address, the network's routing system directs the request to the nearest edge server based on network latency or the number of hops. This approach helps ensure that requests are automatically routed to the most appropriate server.

- **DNS-based Routing:** With DNS-based routing, when a user requests content, the CDN's DNS server responds with the IP address of the most suitable edge server. This approach can take into account factors such as geographical proximity and server load to select the best edge server for handling the request.

- **GeoIP-based Routing:** In this approach, the user's geographical location is determined based on their IP address. The request is then directed to the nearest edge server in terms of geographical distance, which often corresponds to lower network latency.

##### CDN Network Topologies

- **Flat Topology:** In a flat topology, all edge servers in the CDN are directly connected to the origin server. This approach can be effective for smaller CDNs, but may not scale well as the network grows.    
- **Hierarchical Topology:** In a hierarchical topology, edge servers are organized into multiple tiers, with each tier being responsible for serving content to the tier below it. This approach can improve scalability by distributing the load among multiple levels of servers and reducing the number of direct connections to the origin server.
- **Mesh Topology:** In a mesh topology, edge servers are interconnected, allowing them to share content and load with each other. This approach can enhance the redundancy and fault tolerance of the CDN, as well as improve content delivery performance by reducing the need to fetch content from the origin server.
- **Hybrid Topology:** A hybrid topology combines elements from various topologies to create an optimized CDN architecture tailored to specific needs. For example, a CDN could use a hierarchical structure for serving static content, while employing a mesh topology for dynamic content delivery.

#### Push CDN vs. Pull CDN

Pull CDN 
- In a Pull CDN, the content is not stored on the CDN's servers by default. Instead, the CDN "pulls" the content from the origin server when a user requests it for the first time.
- When the cached content expires or reaches its Time-to-Live (TTL), the CDN will fetch the content again from the origin server
- Easy setup 
- origin server only accessed when CDN does not have the content - (less load)
- edge server handles the cache management and expiration 
- Requires origin server to be active all the damn time 
- First request is slower 
- Examples - Cloudflare, Fastly, and Amazon CloudFront.

Push CDN 
- In a Push CDN, the content is "pushed" to the CDN's servers by the content provider, usually through manual uploads or automated processes. 
- The content is proactively distributed across the CDN's edge servers, making it readily available for user requests.
- Push CDNs are typically used for large files or less frequently accessed content, as they allow for better control over content distribution and caching.
- More complex to setup 
- Increase storage costs 
- cache management and expiration lies withing content provider - origin server
- Examples -  Rackspace Cloud Files and Akamai NetStorage.


## Data Partitioning
### Introduction to Data Partitioning

 - It is a technique used in distributed systems and databases to divide a large dataset into smaller, more manageable parts, referred to as partitions. 
 - Each partition is independent and contains a subset of the overall data.
 - Each partition is then assigned to a separate processing node, which can perform operations on its assigned data subset independently of the others.
 - The system can handle more requests and process data more efficiently.

### Partitioning Methods

##### A. Horizontal Partitioning (based on rows)
- Horizontal data partitioning involves dividing a database table into multiple partitions or shards, with each partition containing a subset of rows.
- It allows for parallel processing and faster query execution times.
- Example - Consider a social media platform that stores user data in a database table. The platform might partition the user table horizontally based on the geographic location of the users
- The key problem with this approach is that if the value whose range is used for partitioning isn’t chosen carefully, then the partitioning scheme will lead to unbalanced servers. For ex- you can take the above example only. Not all locations will be equally populated
- Range based sharding and Hash based sharding are there
##### B. Vertical Partitioning (based on columns)
- Vertical data partitioning involves splitting a database table into multiple partitions or shards, with each partition containing a subset of columns
- For example - In an ecommerce platform the name and address are stored in one shard, while order history and payment information are stored in another shard for a user 

##### C. Hybrid Partitioning
- Hybrid data partitioning combines both horizontal and vertical partitioning techniques to partition data into multiple shards.
- For example - ecommerce platform - horizontally based on the geographic location and vertically based on the type of data.
- Also each shard can be stored on a different database server


### Data Sharding Techniques

- Data sharding, a type of horizontal partitioning
- It is a technique used to distribute large datasets across multiple storage resources, often referred to as shards.
##### 1. Range-based Sharding
- Data is divided into shards based on a specific range of values for a given partitioning key.
- Example -  An e-commerce platform stores order data and decides to shard it based on order dates. Shards can be created for specific date ranges, such as monthly or yearly intervals.

##### 2. Hash-based Sharding
- It involves applying a consistent hash function to the partitioning key, which generates a hash value that determines the destination shard for each data entry
- Useful when partition key has large number of distinct values or is not easily divided into ranges.
- For example - social media website basis of  user ID
##### 3. Directory-Based Sharding 
- It uses a lookup table, often referred to as a directory, to map each data entry to a specific shard.
- It offers greater flexibility, as shards can be added, removed, or reorganized without the need to rehash or reorganize the entire dataset.
- Directory must be maintained and kept consistent. (added complexity)
##### 4. Geographical Sharding
- Geographical sharding involves partitioning data based on geographical locations
- Example - based on user country
##### 5. Dynamic Sharding
- It is an adaptive approach that automatically adjusts the number of shards based on the data’s size and access patterns.
- merging or splitting them as the data grows or shrinks.
##### 6. Hybrid Sharding: The Best of Many Worlds
- blend of multiple sharding strategies to optimize performance.
- It can achieve unprecedented efficiency levels.
- Cloud service provider - It's their secret sauce to ensure consistent, high-speed services across the board.

### Benefits of Data Partitioning
- Improved Query Performance (reduce amount of data that needs to be processed)
- Enhanced Scalability (new partitions can be added, without negatively impacting performance)
- Load Balancing (helps distribute the workload evenly across multiple storage nodes)
- Data Isolation (failure or corruption of one partition, doesn't affect other)
- Parallel Processing (multiple partitions can be accessed simultaneously)
- Storage Efficiency (more frequent used, more expensive storage resources, vice versa)
- Simplified Data Management (backup, archiving, and maintenance, manageable & efficient.)
- Better Resource Utilization (appropriate storage and processing resources (geographical))
- Improved Data Security (partitioning data based on sensitivity - patient medical record vs demographic data)
- Faster Data Recovery (focusing on one partition at a time would be faster)

### Common Problems
###### 1. Complexity
- It adds complexity to system architecture, design, and management
- Increased development and maintenance efforts, as well as a steeper learning curve for team members.
###### 2. Data Skew
- uneven data distribution across partitions
- some partitions being larger or more heavily accessed than others
- negative results - Ex - (geographical based)
###### 3. Partitioning Key Selection
- Selecting the right key requires a deep understanding of the data and its access patterns
- Otherwise data skew could happen 
###### 4. Cross-Partition Queries
- performance can suffer, as the system must search through and aggregate data from several partitions.
- reduced overall performance (compared to non-partitioned system)
###### 5. Data Migration
- Requires extra efforts while changing partitioning schemes or adding new partitions
- time-consuming and resource-intensive,
###### 6. Partition Maintenance
- Managing and maintaining partitions can be a challenging and resource-intensive task.
- repartitioning, merging, or splitting partitions (are just nightmare maybe)
- **Backup Challenges:** Performing backups isn't straightforward anymore. You need to ensure data consistency across all shards.
- **Patch Management:** When a security update rolls out, it needs to be applied across all shards, sometimes simultaneously, to maintain compatibility and security.
- **Monitoring Woes:** Instead of one set of metrics, DB administrators now need to monitor multiple, making anomaly detection a more daunting task.
###### 7. Cost
- may require additional hardware, software, or infrastructure
- added complexity of managing a partitioned system may result in higher operational expenses.

## Proxies

### What is a Proxy Server?

![[Screenshot 2024-06-13 at 8.01.40 PM.png]]

#### Forward proxy
- known as "proxy server" or simply "proxy"
- sits in front of one or more client machines and acts as an intermediary between the clients and the internet
- cache data, filter requests, log requests, or transform requests (by adding/removing headers, encrypting/decrypting, or compressing a resource).
- hide the identity of the client from the server
- Proxies can combine the same data access requests into one request and then return the result to the user; this technique is called **collapsed forwarding** (cache stamped/ dogpile)
- Ex - ProxySG
#### Reverse proxy
 - sits in front of one or more web servers and acts as an intermediary between the web servers and the Internet
 - request is first sent to the reverse proxy
 - hides the server's identity.
 - caching, load balancing, or routing requests to the appropriate servers.
 - Ex - NGINX, HAProxy

### Uses of Proxies
- Performance enhancement  (cache frequent accessed content, improve response time, reduced load on server, less bandwidth usage )
- Security enhancement (prevent unauthorized access to sensitive resources.)
- Anonymity and privacy (access content that is restricted based on geographic location or to avoid tracking and surveillance.)
- Load balancing (can distribute client requests across multiple target servers
- Centralized control and monitoring (Administrators can implement policies, filters, and other configurations)
- Content filtering and access control ( configured to block or filter specific content types like netflix does not work on our laptops )
- Content adaptation and transformation (image formats, compressing data, or adjusting content for mobile or low-bandwidth devices)
- Logging and auditing (performance issues, security vulnerabilities, or policy violations)
- SSL termination (SSL/TLS encryption and decryption)
- Application-level gateway (authentication, content filtering, or protocol translation, at the application level.)
### VPN vs. Proxy Server

VPN
- A **VPN** creates a secure, encrypted tunnel between your device and a remote server operated by the VPN service. All your internet traffic is routed through this tunnel, meaning that your data is secure from external observation.

Key Features
- **Encryption**: Offers end-to-end encryption for all data transmitted.
- **Traffic Routing**: Routes all internet traffic through the VPN server.
- **IP Masking**: Hides your IP address and makes it appear as if your traffic is coming from the VPN server’s location.
- **Security and Privacy**: Provides a high level of security and privacy.

Proxy Server 
- A **Proxy Server** acts as an intermediary between your device and the internet. It receives your requests, forwards them to the internet, and then relays the response back to you.

Key Features 
- **IP Masking**: Hides your IP address, making it appear as if the requests are coming from the proxy’s location.
- **Limited Scope**: Usually, only browser traffic or traffic from specific applications is rerouted.
- **No Encryption**: Does not inherently encrypt data (except for secure proxy servers like HTTPS proxies).
- **Caching**: Some proxies cache data, which can speed up subsequent requests to the same sites.

Key Differences
 - Encrypts all data, does not encrypt data (unless HTTPS proxies are used)
 - Reroutes and encrypts all traffic, only reroutes for specific apps and browsers
 - More privacy and security, provides IP masking (but limited security only)
 - Can be slower due to encryption, faster (could be slower if many user access the same proxy)
 - Safety is more concern like in public wifi, mostly for accessing content not allowed in your area

## Redundancy and Replication

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

### Data Backup vs. Disaster Recovery

##### Data Backup
- It refers to the process of creating copies of data to be used in case the original data is lost or damaged. The primary goal is to restore data after events like deletion, corruption, or minor hardware failures.
- Can be scheduled at regular intervals 
- Use for important files, databases etc
- Backups are on tapes, disk or cloud storage 

##### Disaster Recovery
- It is a broader strategy that includes policies, tools, and procedures for protecting and restoring an organization's IT infrastructure in the event of a major disaster, such as a natural disaster, cyberattack, or major hardware failure.
- Requires comprehensive planning - for quickly restoring everything 
- Infrastructure Recover, Business Continuity 
- Resuming business operations at an alternate location after a natural disaster damages the primary data center.

###### Key Differences
- data restorationg, resuming business operations after big events 
- duplicating data, restoring entire systems and infrastructure
- protect against data loss, business face minimum downtime in case of major disruptions 
- small scale data loss, large-scale disruptions 
- simple, more complex 

## CAP

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

## Databases 

### Introduction to Databases
- A database is an organised collection of structured data that is stored and managed electronically.
- managing, storing, and retrieving data efficiently
##### Database Management Systems (DBMS)
- A Database Management System (DBMS) is software that interacts with users, applications, and the database itself to capture, store, and manage data
- The primary goal of a DBMS is to ensure that data remains consistent, secure, and easily accessible.

Two Main Types 
- **Relational Database Management Systems (RDBMS):** These systems store data in tables with predefined schema and relationships between them. The most common query language for RDBMSs is SQL (Structured Query Language). MySQL, PostgreSQL etc. 
    
- **Non-Relational Database Management Systems (NoSQL):** These systems store data in various formats, such as key-value, document, column-family, or graph. NoSQL databases are known for their ability to scale horizontally and handle unstructured or semi-structured data. MongoDB, Redis, Apache Cassandra and Neo4j

##### High level differences between SQL and NoSQL
- Schema is fixed (if modify then modify the whole data and go offline), Schema is dynamic 
- SQL (structured query language) for defining and manipulating the data, In NoSQL the database queries are focused on a collection of documents - UnQL (Unstructured Query Language)
- SQL - Vertical Scaling, NoSQL - horizontal scaling 
- SQL - Acid compliant, NoSQL - partial ACID for availability and partition tolerance

### SQL Databases
- SQL databases follow the ACID properties (Atomicity, Consistency, Isolation, Durability) to ensure reliable data transactions.
- **Indexes:** Database indexes are data structures that help to speed up data retrieval operations. They work similarly to the index in a book, allowing for faster lookups and searches.
- SQL is a standardized language for managing and querying relational databases.
	- **Data Definition Language (DDL):** Allows for the creation, modification, and deletion of database structures, such as tables, indexes, and constraints.    
	- **Data Manipulation Language (DML):** Enables data insertion, updating, deletion, and retrieval operations on database tables.
	- **Data Control Language (DCL):** Deals with user permissions and access control for database objects.
	- **Transaction Control Language (TCL):** Manages database transactions and ensures ACID compliance. 

### NoSQL Databases
- also known as "Not Only SQL" databases
- Query languages, depending on the specific type of NoSQL database being used.
- perform well under specific workloads, such as high write loads or large-scale data storage and retrieval.
##### Types of NoSQL Databases

![[Screenshot 2024-06-14 at 4.37.09 PM.png]]
###### 1. Key-value databases
- key is a unique identifier and the value is the associated data
- Best case - high write and read performance for simple data models, such as session management and real-time analytics.
- **Examples:** Amazon DynamoDB, Azure Cosmos DB, Riak.
###### 2. In-memory key-value databases
- primarily stored in memory
- minimal response times (eliminating disk access)
- risk losing data upon a process or server failure
- It can persist data on disks by storing each operation in a log or by taking snapshots.
- **Examples:** Redis, Memcached, Amazon Elasticache.
###### 3. Document databases
- structured similarly to key-value databases
- except that keys and values are stored in documents written in a markup language like JSON, BSON, XML, or YAML.
- nested fields, arrays, and other complex data structures
- User profiles, product catalogs
- **Examples:** MongoDB, Amazon DocumentDB, CouchDB.
###### 4. Wide-column databases
- based on tables but without a strict column format
- Rows do not need a value in every column
- segments of rows and columns containing different data formats can be combined. (what does that mean??)
- **Examples:** Cassandra, Accumulo, Azure Table Storage, HBase.
###### 5. Graph databases
- map the relationships between data using nodes and edges
- Nodes are the individual data values, and edges are the relationships between those values.
- Social graphs, recommendation engines
- **Examples:** Neo4j, Amazon Neptune, Cosmos DB through Azure Gremlin.
###### 6. Time series databases
- store data in time-ordered streams
- Data is not sorted by value or id but by the time of collection, ingestion, or other timestamps included in the metadata.
- Industrial telemetry, DevOps
- **Examples:** Graphite, Prometheus, Amazon Timestream.
###### 7. Ledger databases
- based on logs that record events related to data values
- data changes that are used to verify the integrity of data.
- Banking systems, registrations
- **Examples:** Amazon Quantum Ledger Database (QLDB).

##### Pros and cons of using NoSQL databases
- schema-less design
- accommodate new data types without the need for extensive schema modifications
- built-in support for data replication, sharding, and partitioning
- superior performance under specific workloads, such as high write loads, large-scale data storage and retrieval, and complex relationships.
- NoSQL databases often prioritize Availability and Partition Tolerance over Consistency, resulting in a trade-off known as “eventual consistency.”
-  not be as expressive or versatile as SQL when it comes to complex data manipulation and analysis
- need to learn multiple query languages and paradigms when working with different types of NoSQL databases.

Things to consider 
- Deployment
- Monitoring 
- Backup and Recovery 
- Security 
- Community and Support 
- Cost 

### ACID vs BASE Properties
##### ACID Properties

![[Screenshot 2024-06-15 at 1.01.52 PM.png]]

- **Use Cases**: Ideal for systems requiring high reliability and data integrity, like banking or financial systems.
##### BASE Properties

![[Screenshot 2024-06-15 at 1.03.20 PM.png]]
- favoring availability over consistency.
- **Use Cases**: Suitable for distributed systems where availability and partition tolerance are more critical than immediate consistency, like social networks or e-commerce product catalogs.
- some level of data inconsistency.

### SQL Normalization and Denormalization
###### SQL Normalization
- Normalization in SQL is a database design technique that organizes tables in a manner that reduces redundancy and dependency. 
- It involves dividing a database into two or more tables and defining relationships between them to achieve a more efficient database structure.
- Avoids duplication of data.
- Ensures data accuracy and consistency.
- **Normalization** is about reducing redundancy and improving data integrity but can lead to more complex queries.

( Study Normalization even more achche se )***
###### Levels (Normal Forms)
- **1NF (First Normal Form)**: Data is stored in atomic form with no repeating groups.
- **2NF (Second Normal Form)**: Meets 1NF and has no partial dependency on any candidate key.
- **3NF (Third Normal Form)**: Meets 2NF and has no transitive dependency.

###### SQL Denormalization
- Denormalization, on the other hand, is the process of combining tables to reduce the complexity of database queries. 
- This can introduce redundancy but may lead to improved performance by reducing the number of joins required.
- **Improves Query Performance**: Reduces the complexity of queries by reducing the number of joins.
- In read-heavy database systems where query performance is a priority.
- **Denormalization** simplifies queries but at the cost of increased data redundancy and potential maintenance challenges.

If read heavy - then prefer denormalization, since you don't have to perform join optimisations

### In-Memory Database vs. On-Disk Database

###### In-Memory Database (IMDB)
- Primarily stores data in the main memory (RAM) of the server.
- Some can persist data on disk, but the primary data access and manipulation happen in memory.
- Offers high performance and low latency, efficient for read-heavy operations and complex, real-time computations.
- Use case : Real time analytics, Caching, Session Storage
- Limitations : Cost, Scalability and Data Volatility (unless maintained with persistance mechanism)
- Examples - Redis, Memcached, SAP HANA, Apache Ignite
###### On-Disk Database
- Stores data on persistent disk storage (HDD or SSD).
- slower due to disk I/O operations
- More suited for applications where the speed of data access is less critical.
- Use cases: Transactional Systems, Large Data sets, General Purpose Databases
- Speed and I/O Bottlenecks are limitations 
- Example - MySQL, PostgreSQL, MongoDB, Oracle Databse, Microsoft SQL server, SQLLite

### Data Replication vs. Data Mirroring

##### Data Replication
- It involves copying data from one location to another. The replication can be synchronous or asynchronous.
-  Often creates multiple copies of data, which can be stored across different servers or locations.
- Enhances data availability and accessibility, 
- used for load balancing, 
- enables data analysis without impacting the primary data source.
##### Data Mirroring
- the process of creating an exact replica of a database or storage system, usually in real-time.
- synchronous, data is always in sync in both primary and mirror locations 
- In critical applications requiring high availability and data integrity, such as financial transaction system
- Primarily for disaster recovery and high availability.

### Database Federation
- Federated databases integrate data from different sources, which can include both traditional databases and other forms of data repositories.
- data remains in its original location but is logically unified
- can combine data from different types of databases (such as SQL, NoSQL, XML databases)
-  allow queries to span across multiple databases
- Use cases : Enterprise Data Access, Business Inteligence and Analytics, Data warehousing, Mergers and Acquisitions
- Advantages - Reduced Complexity (no need to physically move/replicate data), Flexibility (easy to add and remove data), real-time access 
- Challenge - Performance, Security and Compliance, complex queries (requires advanced techniques)

## Indexes

### What are Indexes?
- The goal of creating an index on a particular table in a database is to make it faster to search through the table and find the row or rows that we want
- Example - Library Catalog

![[Screenshot 2024-06-15 at 4.36.29 PM.png]]

- Simply saying, an index is a data structure that can be perceived as a table of contents that points us to the location where actual data lives
- Finding a small payload in such a large dataset can be a real challenge, since we can’t possibly iterate over that much data in any reasonable time
##### Purpose of Database Indexes
- **Faster Data Retrieval** (reduction in disk I/O operations and CPU usage)
- **Sorting and Ordering** (quickly sort the data using indexes)
##### How Indexes Improve Query Performance
- **Reduced Table Scans** (avoid full table scans)
- **Efficient Data Access** 
- **Index Selectivity** (indexes with high selectivity, reduces the numbers of rows to be accessed)
##### How Indexes decrease write performance?
- require additional storage space
- slow down write operations (insert, update and delete) as the indexes must be updated along with the table 
- Adding unnecessary indexes on tables should be avoided and indexes that are no longer used should be removed. (since updation is required on each write operation)
- If more write, and less read (then kindly do not use it)

### Types of Indexes
##### 1. Clustered Indexes
- It determine the physical order of data storage in a table
- sorted and stored based on the columns specified in the clustered index
- only be one clustered index per table
- high efficient for range queries
- Example - In a table with a clustered index on the 'DateOfBirth' column, the rows would be stored in the order of the 'DateOfBirth' values.
##### 2. Non-Clustered Indexes
- It do not affect the physical order of data storage in a table
- maintain a separate data structure that points to the rows in the table
- Multiple non clustered indexes can created per table 
- Example - In a table with a non-clustered index on the 'LastName' column, the index would store pointers to the rows sorted by the 'LastName' values, while the actual table data remains unordered.
##### 3. Unique Indexes
- It ensures that the indexed columns do not contain duplicate values
- **Example:** In a table with a unique index on the 'Email' column, no two rows can have the same email address.
##### 4. Partial Indexes
- only a subset of rows in a table based on a specified filter condition
- large table has a relatively small number of rows that are frequently queried
- **Example:** In a table with a partial index on the 'Status' column where the condition is "Status = 'Active'", only rows with an 'Active' status would be included in the index.
##### 5. Filtered Indexes
- only a subset of rows based on a specified filter condition
- filtered indexes are specific to Microsoft SQL Server
- provide additional optimisation options for queries with specific predicates.
- **Example:** In a table with a filtered index on the 'ProductID' column where the condition is "Price > 100", only rows with a price greater than 100 would be included in the index.
##### 6. Full-Text Indexes
- designed to support complex text-based searches, such as natural language queries or pattern matching
- **Example:** In a table with a full-text index on the 'Description' column, users can search for rows containing specific words or phrases in the 'Description' field.
##### 7. Spatial Indexes
- used to optimize queries involving spatial data types, such as geometry or geography data
- **Example:** In a table containing location information, a spatial index on the 'GeoCoordinates' column would enable fast retrieval of nearby locations based on latitude and longitude coordinates.

## Bloom Filters
### Introduction to Bloom Filters

- a space-efficient and probabilistic data structure
- to quickly find if an element might be present in a set.
- It returns false positives but accurate no ie. if it returns true, then the element could be present or it could not be present. But if it return false, then it definitely does not exist 
- It is a tradeoff between spaced used vs accuracy (if we increase the space more accuracy will be there)
###### Basic Principles
- two main components: a bit array and a collection of hash functions
- The bit array is initially set to all zeroes, and the hash functions are used to map elements to positions in the bit array
- hash functions should ideally be independent and uniformly distributed to minimize the probability of false positives.
- Hash function generates three position suppose, so if we are inserting we will mark all these positions as 1, later on while checking if something exist we can use these three function and check if all three values are 1 or not (if even one bit is set to 0, we can definitely know it was never inserted)
![[Screenshot 2024-06-15 at 7.48.42 PM.png]]
##### Purpose and Use Cases
-  situations where storage space is limited, and exact membership testing is not critical
- It can be used to efficiently check if a requested web resource is present in the cache.
- Spell Checking, Network Routing, Data synchronization
- Best use case - NoSQL database, before going to search for an index in the entire database they use bloom filter to have surety whether to go searching for that index or not 
- Or earlier chrome used to use this in order to know if for a malicious url, they should be searching their entire database or not 
##### Benefits 
- Space Efficiency - uses bit array to store information about the elements in the set, (far less compared to hashset and set) 
- Time Efficiency - constant time compexity O(1) for both insertion and query
- No False Negatives
- Scalability - large number of elements with minimal increase in storage space
- Easy union and intersection of two bloom filters - Just OR ya AND on both Bit arrays 
##### Limitations 
- False positives 
- No Removal of elements - if one time a bit is set to 1, we set it back to zero (it could affect other elements)
- No extraction of exact element - if you want, require use of another data structure with it
- Dependency on Hash Function - poor hash function -> more false positives (hence proper analysis is required here)
- Tuning parameters - bit array and hash functions to achieve optimal performance

### Variants and Extensions of Bloom Filters

###### 1. Counting Bloom Filters
- Using array of counters instead of a simple bit array
- Gives ability to delete, as each counter can be incremented or decremented
- Comes at the cost of extra space and complexity
###### 2. Compressed Bloom Filters
- reduce the storage overhead by compressing the underlying bit array
- compression techniques - run-length encoding/ Golomb coding
- Additional computation overhead during insertion and query 
###### 3. Spectral Bloom Filters
- designed to estimate the frequency of elements in a dataset
- uses multiple standard Bloom filters in parallel, each representing a different frequency range
- Used in data mining or network traffic analysis.
###### 4. Scalable Bloom Filters
- issue of dynamically growing datasets by automatically adjusting the filter's size and parameters as the number of elements increases
- maintain a target false positive rate while accommodating an unpredictable number of elements.
###### 5. Cuckoo Filters
-  similar functionality with improved space efficiency and support for element removal
- combination of cuckoo hashing and a compact fingerprint representation of elements to achieve these benefits
- cuckoo filters can outperform standard Bloom filters (in multiple scenarios)

### Applications of Bloom Filters (can do deeper in this one whenever you want to)
###### 1. Database Systems
- Bloom filter as a pre-filter, unnecessary disk reads can be avoided when querying for non-existent keys
- In distributed databases, Bloom filters can also help reduce network overhead by minimizing the number of remote requests for non-existent data.
###### 2. Network Routing and Traffic Analysis
- I did not get this one
###### 3. Web Caching and Content Distribution
- By using a Bloom filter to represent the contents of a cache, a proxy server can quickly determine if a requested resource is in its cache or not, reducing unnecessary cache misses and network requests
###### 4. Spam Filtering and Malware Detection
- By querying the filter, incoming messages or files can be quickly checked against the known signatures, allowing for efficient filtering of unwanted content.
###### 5. Distributed Systems Membership Testing
- Bloom filters can be utilized to perform efficient membership testing for sets shared among multiple nodes.

## Long-Polling, WebSockets, and Server-Sent Events

- popular communication protocols between a client like a web browser and a web server.

 ![[Screenshot 2024-06-15 at 11.46.04 PM.png]]
 
 ### **Ajax Polling**
 - The basic idea is that the client repeatedly polls (or requests) a server for data. The client makes a request and waits for the server to respond with data. If no data is available, an empty response is returned.
 - The problem with Polling is that the client has to keep asking the server for any new data. As a result, a lot of responses are empty, creating HTTP overhead.

**HTTP Long-Polling**
- With Long-Polling, the client requests information from the server exactly as in normal polling, but with the expectation that the server may not respond immediately. That’s why this technique is sometimes referred to as a "Hanging GET".
- Each Long-Poll request has a timeout. The client has to reconnect periodically after the connection is closed due to timeouts.

**WebSockets**
- It provides [Full duplex](https://en.wikipedia.org/wiki/Duplex_(telecommunications)#Full_duplex) communication channels over a single TCP connection
- The client establishes a WebSocket connection through a process known as the WebSocket handshake
- This protocol enables communication between a client and a server with lower overheads, facilitating real-time data transfer from and to the server.

**Server-Sent Events (SSEs)**
- Client establishes a persistent and long-term connection with the server
- The server uses this connection to send data to a client. If the client wants to send data to the server, it would require the use of another technology/protocol to do so.
- best when we need real-time traffic from the server to the client

## Quorum
- In Distributed Systems, data is replicated across multiple servers for fault tolerance and high availability.
- A quorum is the minimum number of servers on which a distributed operation needs to be performed successfully before declaring the operation's overall success.

## Heartbeat
- Each server periodically sends a heartbeat message to a central monitoring server or other servers in the system to show that it is still alive and functioning.
- mechanisms for detecting failures in a distributed system
- If there is no heartbeat within a configured timeout period, the system can conclude that the server is not alive anymore and stop sending requests to it and start working on its replacement.
## Checksum
- In a distributed system, while moving data between components, it is possible that the data fetched from a node may arrive corrupted
- To calculate a checksum, a cryptographic hash function like MD5, SHA-1, SHA-256, or SHA-512 is used. The hash function takes the input data and produces a string (containing letters and numbers) of fixed length; this string is called the checksum.
- When a system is storing some data, it computes a checksum of the data and stores the checksum with the data.
- When a client retrieves data, it verifies that the data it received from the server matches the checksum stored. If not, then the client can opt to retrieve that data from another replica.

####  Uses of Checksum
- Data Integrity Checks - ( you wanna make sure it doesn’t get altered during transmission)
- **Error Detection** - (helping systems know when they need to try downloading it again)
- **Data Retrieval and Verification** - (download software or a file from a website, they often provide a Checksum value, help to verify that it is exactly what the creators intended, no nasty surprises hiding inside)
- **Networking** - (Checksums help detect errors in packets of data sent over a network)
- Secure Storage - (Periodically, the stored data is checked against the Checksum)
- **Password Verification** - (store only checksum, and if password entered convert to checksum and then compare)
- **Preventing Accidental Duplicates** - (If two pieces of data have the same Checksum, they might be duplicates, saving storage space and preventing redundancy!)

## Leader and Follower
- Distributed systems keep multiple copies of data
- quorum to ensure data consistency between replicas
- quorum can lead to another problem, that is, lower availability; at any time, the system needs to ensure that at least a majority of replicas are up and available, otherwise the operation will fail

#### Solution
- Allow only a single server (called leader) to be responsible for data replication and to coordinate work.
 ![[Screenshot 2024-06-18 at 7.24.14 PM.png]]

- In case the leader fails, one of the followers can become the leader. In some cases, the follower can serve read requests for load balancing.

## Security 

### What is Security and Privacy?
- Distributed systems face unique challenges related to security and privacy due to their distributed nature, which makes them more vulnerable to attacks and data breaches

##### A. Authentication and Authorization
- Authentication is the process of verifying the identity of users, services, or nodes before allowing them access to the system.
- Authorization determines what actions or resources the authenticated entity is allowed to access.
##### B. Data Encryption
-  converting data into an encoded format that can only be decrypted and read by someone with the correct decryption key.
- Techniques like symmetric and asymmetric encryption, as well as protocols such as TLS/SSL, can be used to secure data in distributed systems.
##### C. Secure Communication
- Implementing secure communication protocols, such as TLS/SSL, IPSec, or application-level encryption, can help protect the integrity and confidentiality of data exchanged between nodes.
##### D. Intrusion Detection and Prevention
- designed to monitor network traffic, detect malicious activities or policy violations, and take appropriate actions to mitigate potential threats

### What is Authentication?
- Authentication is a crucial first step in securing a software system, ensuring that access is granted only to the right individuals, much like how the right people are allowed into a club or a private event.

**Types of Authentication**:
1. **Single-Factor Authentication (SFA)**: 
2. **Two-Factor Authentication (2FA)**: 
3. **Multi-Factor Authentication (MFA)**:

### What is Authorization?
- Authorization in software systems is like getting a specific wristband at a festival that allows you access to certain areas. It's about granting or denying permissions to do something after your identity is verified

 ##### Roles and Permissions
-  **Roles**: These are like different types of wristbands or badges. For example, an 'Admin' might have access to everything, while a 'User' has limited access.
- **Permissions**: Specific actions you're allowed to perform, like viewing, editing, or deleting information. If you're at a festival, it's like being allowed to enter backstage areas, VIP sections, or just the general area.
##### Examples - 
- File System Permissions
- Database Roles
- Web Application Privileges

### OAuth vs. JWT for Authentication

### JWT
- Full form - Json Web Tokens 
- **JWT** is a token format used in authorization and information exchange. It’s a JSON object encoded as a string, which is digitally signed, and optionally encrypted.
- A JWT typically consists of three parts: Header, Payload, and Signature.
- Stateless; it contains all the necessary information within the token.

What is Encoding
- In computers, encoding is the process of putting a sequence of characters (letters, numbers, punctuation, and certain symbols) into a specialized format for efficient transmission or storage.

![[Screenshot 2024-06-18 at 8.24.24 PM.png]]

![[Screenshot 2024-06-18 at 8.25.29 PM.png]]

Pros 
- Self contained, portable, dont require server side storage 
Cons
- As payload in not encrypted, hence it should not contain highly sensitive data 
- vulnerable to theft 
- poor performance due to large payload 

### OAuth
https://www.youtube.com/watch?v=t4-416mg6iU
- Authorization between services (but whyyy?)
- **OAuth** is an open standard for access delegation, commonly used as a way for users to grant websites or applications access to their information on other websites but without giving them the passwords.
- When third parties wants some data from your Google, Facebook account and you don't want to share the passwords 
- It is not an authentication protocol but a secure delegation mechanism
- Example -  A user logs into a third-party app using their Google account. OAuth allows the app to access some of the user’s Google account data, as authorized, without the need to share Google account credentials with the third-party app.It uses access tokens for authorization.
- Typically relies on server-side storage to keep track of the issued tokens

Security 
- **OAuth**: Security depends on the specific implementation but generally relies on SSL/TLS for security during token exchange.
- **JWT**: The token itself is secured by its digital signature.

### What is Encryption?
- Encryption transforms readable data (plaintext) into a scrambled, unreadable format (ciphertext). To turn it back into readable form, you need the correct decryption key.
- Important to keep the keys safe (complex task)
- Slow downs systems 
##### **Types of Encryption**:
1. **Symmetric Encryption**: Uses the same key for encrypting and decrypting data. Think of it as a lock and key system where the same key locks and unlocks the box.
2. **Asymmetric Encryption**: Uses two different keys – a public key for encryption and a private key for decryption. It's like having a public mailbox where anyone can drop a message (public key), but only you have the key to open it (private key).
##### Uses
- Data security
- Privacy
- Integrity of data

### What are DDoS Attacks?
- malicious attempt to disrupt normal traffic of a targeted server, service, or network by overwhelming the target or its surrounding infrastructure with a flood of Internet traffic.
- **Goal**: To overload the server's capacity to handle requests, causing slow service or complete shutdown.
- **Volumetric Attacks**: The most common form, these attacks flood the network with a substantial amount of traffic.
- **Protocol Attacks**: These target network layer or transport layer protocols to consume server resources or bandwidth.
- **Application Layer Attacks**: These are more sophisticated, targeting specific aspects of an application or server.

##### Mitigation Strategies (pretty much only some of them are useful)
1. **Network Redundancy**: Having multiple pathways for network traffic can help avoid single points of failure.
2. **DDoS Protection Services**: These services can detect and mitigate DDoS attacks, often through large-scale network infrastructure capable of absorbing and diffusing attack traffic.
3. **Firewalls and Anti-DDoS Software**: Implementing advanced firewall systems and specific anti-DDoS software can help identify and block attack traffic.
4. **Traffic Analysis**: Continuously monitoring network traffic can help in identifying anomalies indicative of a DDoS attack.
5. **Responsive Plan**: Having a response plan in place, including procedures for identifying, mitigating, and recovering from an attack, is crucial for minimizing damage.
6. **Good Security Hygiene**: Regularly updating security protocols and educating users about the risks of malware can help reduce the number of devices that can be used in DDoS attacks.
7. **Scalable Infrastructure**: Utilizing cloud services with the ability to scale rapidly can absorb and disperse high traffic loads during an attack.

## Distributed Messaging System

### Introduction to Messaging System
- Issues its solves 
	- Extreme high number of messages per second
	- multiple aggregator services, how to divide work among them?
	- highly coupled 
	- What is all aggregator services fails?

![[Screenshot 2024-06-18 at 10.37.31 PM.png]]

- A **messaging system** is responsible for transferring data among services, applications, processes, or servers. Such a system helps **decouple** different parts of a distributed system by providing an **asynchronous** way of transferring messaging between the sender and the receiver.
- Mainly de-coupling and asynchronously transferring data from one place to another 
### Queue

![[Screenshot 2024-06-18 at 10.38.50 PM.png]]

- messages are stored sequentially in a queue
- A particular message can be consumed by a maximum of one consumer only.
- limits the system as multiple consumers cannot read the same message from the queue.

### Publish-subscribe messaging system

![[Screenshot 2024-06-18 at 10.40.23 PM.png]]

- messages are divided into topics
- A publisher (or a producer) sends a message to a topic that gets stored in the messaging system under that topic
- Subscribers (or the consumer) subscribe to a topic to receive every message published to that topic.
- if two consumers subscribe to the same topic, they will receive all messages published to that topic.
- The messaging system that stores and maintains the messages is commonly known as the message **broker**.
-  This **loose coupling** enables subscribers and publishers to read and write messages at different rates.
- **fault-tolerance**, so messages do not get lost between the time they are produced and the time they are consumed.

In Summary - 
- Messaging Buffering - (handling sudden peak of load)
- Guarentee of message deliver
- Provides abstraction 
- Scalability 
- Fault Tolerance
- Asynchronous Communication 
- Load Balancing 
- Messages Persistence 
- Security 
- Interoperability 

### Introduction to Kafka
- open-source **publish-subscribe**-based messaging system
- Kafka was created at LinkedIn around 2010
##### Use Cases
1. Reliably storing a huge amount of data.
2. Enabling high throughput of message transfer between different entities.
3. Streaming real-time data.

At a high level, we can call Kafka a distributed **Commit Log**. (understand more in depth)
![[Screenshot 2024-06-18 at 10.48.37 PM.png]]
 - A Commit Log (_also known as a Write-Ahead log or a Transactions log_) is an **append-only** data structure that can persistently store a sequence of records.
 - Records are always appended to the end of the log, and once added, records cannot be deleted or modified.
 - Reading from a commit log always happens from left to right (_or old to new_).
 - Kafka takes advantage of sequential disk reads (_more on this later_) .

Use cases 
- Metrics
- Log Aggregation 
- Stream Processing (pick from one topic and put in another topic)
- Commit Log (useful for recovery failed nodes)
- Website Activity Tracking (product suggestions)

### Kafka common terms
- Brokers - (A Kafka server is also called a broker. Brokers are responsible for reliably storing data provided by the producers and making it available to the consumers.)
- Records - (A record contains a key, a value, a timestamp, and optional metadata headers.)
![[Screenshot 2024-06-18 at 10.52.09 PM.png]]

##### Topics
- A topic is like a table in a database, and the messages are the rows in that table.
- Consumers can subscribe to a topic to get notified when new messages are added to that topic
- In a Kafka cluster, a topic is identified by its name and must be unique.
- Kafka retains messages for a configurable amount of time or until a storage size is exceeded
- Kafka's performance is effectively constant with respect to data size (hence storing data for a long time is no issue)

![[Screenshot 2024-06-18 at 10.54.39 PM.png]]

#### High-level architecture
###### Kafka cluster
Kafka is deployed as a cluster of one or more servers, where each server is responsible for running one Kafka broker.
###### ZooKeeper
- It is a distributed key-value store and is used for coordination among kafka brokers and storing configurations.
- Highly optimized for reads
- It maintains metadata information about the kafka cluster.
![[Screenshot 2024-06-19 at 10.21.49 AM.png]]

### Messaging patterns
##### 1. Point-to-Point (Direct Messaging):
- Single producer to Single consumer 
- Queue are often used to implement it (FIFO)
- Simple to implement, No intermediaries, Limited Scalability 

##### 2. Publish-Subscribe (Pub/Sub):
- Messages are sent from a producer (publisher) to multiple consumers (subscribers).
- Ideal where the information needs to be shared among multiple people, or the sender doesn't know who could be the reciever
- Decoupling, Scalable, Dynamic Subscription (consumers can added and removed dynamically)

##### 3. Request-Reply (Request-Response):
- a producer (requester) sends a message to a consumer (responder) and waits for a response.
- Synchronouse communication, Sender requires response before moving ahead 
- Inside payment gateways when the usern the consumer is waiting for the response 
- Tight coupling is there, also latency is also present (since user has to wait now)
##### 4. Fan-Out/Fan-In (Scatter-Gather):
- a message is sent to multiple consumers (fan-out), and the responses from these consumers are aggregated before being sent back to the original sender.
- tasks needs to distributed among multiple worker nodes 
- Parallelism, load balancing and also aggregration step would cost extra resources 
- Ex - A search engine sends query to multiple index servers, each of them return relevant results, which are then combined and return back to the user. 
##### 5. Dead Letter Queue (DLQ):
- This pattern is used to handle erroneous or invalid messages that cannot be processed by consumers.
- They are sent to an dedicated queue called the dead letter queue, where they can be monitored, analyzed and reprocessed.
- Help to not block the queue. 
- Error handling, monitoring and debugging, fault isolation and retention 
- Ex -  An email delivery system where messages that fail to be delivered (store is some another queue and figure out the issue by trying to redeliver it)

### Popular Messaging Queue Systems
##### 1. RabbitMQ
- It an open-source message broker 
- Supports - publish-subscribe, request-reply, and point-to-point communication.
- Flexible, extensible (more protocols using plugins), internal tools for monitoring, clustering and high availability possible 
##### 2. Apache Kafka
- distributed streaming platform - high throughput, fault tolerant and scalable messaging 
- stream processing, log aggregation and event driven architectures 
- Horizontal scalable (distributed architecture), Durability (messages are stores persistently on disk), low latency, kafka provides stream process API for real time processing 
##### 3.  Amazon Simple Queue Service (SQS)
- messaging queue provided by AWS 
- automatic scaling, reliable and secure, pay as you go model (might be or not be cost efficient)
##### 4. Apache ActiveMQ
- open-source, multi-protocol message broker
- Highly available, message persistence, Integration with spring (simple)

### RabbitMQ vs. Kafka vs. ActiveMQ
1. **Performance and Scalability:** Kafka is designed for high throughput and horizontal scalability, making it well-suited for handling large volumes of data. RabbitMQ and ActiveMQ both offer high performance, but Kafka generally outperforms them in terms of throughput, particularly in scenarios with high data volume.
    
2. **Message Ordering:** RabbitMQ and ActiveMQ guarantee message ordering within a single queue or topic, respectively. Kafka ensures message ordering within a partition but not across partitions within a topic.
    
3. **Message Priority:** RabbitMQ and ActiveMQ support message prioritization, allowing messages with higher priority to be processed before those with lower priority. Kafka does not have built-in message priority support.
    
4. **Message Model:** RabbitMQ uses a queue-based message model following the Advanced Message Queuing Protocol (AMQP), while Kafka utilizes a distributed log-based model. ActiveMQ is built on the Java Message Service (JMS) standard and also uses a queue-based message model.
    
5. **Durability:** All three message brokers support durable messaging, ensuring that messages are not lost in case of failures. However, the mechanisms for achieving durability differ among the three, with RabbitMQ and ActiveMQ offering configurable durability options and Kafka providing built-in durability through log replication.
    
6. **Message Routing:** RabbitMQ provides advanced message routing capabilities through exchanges and bindings, while ActiveMQ uses selectors and topics for more advanced routing. Kafka's message routing is relatively basic and relies on topic-based partitioning.
    
7. **Replication:** RabbitMQ supports replication through Mirrored Queues, while Kafka features built-in partition replication. ActiveMQ uses a Master-Slave replication mechanism.
    
8. **Stream Processing:** Kafka provides native stream processing capabilities through Kafka Streams, similarly RabbitMQ offers stream processing too, while ActiveMQ relies on third-party libraries for stream processing.
    
9. **Latency:** RabbitMQ is designed for low-latency messaging, making it suitable for use cases requiring near-real-time processing.
    
10. **License:** RabbitMQ is licensed under the Mozilla Public License, while both Kafka and ActiveMQ are licensed under the Apache 2.0 License.

### Scalability and Performance
##### 1. Partitioning
- process of dividing a data set into smaller, manageable pieces called partitions.
- helps in distribute messages evenly among multiple nodes
- Ex -  Apache Kafka uses partitions to divide a topic's messages
##### 2. Consumer Groups
- It is a way to manage multiple consumers of a messaging system that work together to process messages from one or more topics
- Each consumer group ensures that all messages in the topic are processed, and each message is processed by only one consumer within the group
##### 3. Load Balancing and Parallel Processing
- Load balancing refers to distributing incoming messages evenly among multiple consumers or processing units, while parallel processing involves processing multiple messages simultaneously
##### 4. Message Batching and Compression
- process of combining multiple messages into a single batch before processing or transmitting them
- For ex - Producers can batch messages together, and the system can compress these batches using various compression algorithms like Snappy or Gzip, reducing the amount of data transmitted and improving overall performance.

## Distributed File Systems 
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

### Misc Concepts 
### Batch Processing vs. Stream Processing

##### Batch Processing
- large chunks of data with some delay.
- higher latency due to delayed processing.
- can handle more complex processing since data is not processed in real-time.
- is designed for high volumes of data.
- can be resource-intensive, often run during off-peak hours.
- Use cases -> End-of-day reports, Data warehousing and ETL (Extract, Transform, Load) processes, Monthly billing processes.
##### Stream Processing 
- processes data immediately and continuously.
- lower latency and is suitable for time-sensitive applications.
- more about processing less complex data quickly.
-  handles lower volumes of data at any given time but continuously over a period.
-  resources to be constantly available but generally uses less resource per unit of data.
- Use cases -> Real-time monitoring and analytics (e.g., stock market analysis), Live data feeds (e.g., social media streams), IoT (Internet of Things) sensor data processing.

### XML vs. JSON
##### XML 
![[Screenshot 2024-06-24 at 6.37.01 AM.png]]
- markup language much like HTML, designed to store and transport data
- It is more verbose with a heavier structure.
- treats all data as strings and doesn’t natively support different data types.
- less readable and writable for humans but has a strong capability for defining complex structures.
- requires a parser to be read and written.
- more demanding in terms of resources 
- Use Cases - document processing systems where document format and structure are important
##### JSON
![[Screenshot 2024-06-24 at 6.38.12 AM.png]]
- lightweight data-interchange format that is easy for humans to read and write and for machines to parse and generate.
- lightweight and more compact.
- supports various data types natively.
- highly readable and writable, with a simple structure.
- easily parsed by standard JavaScript functions.
- more demanding in terms of resources due to its complexity.
- Use cases -> web applications, data bases, Rest API 

### Synchronous vs. Asynchronous Communication
##### Synchronous
- Occurs in real-time; sender and receiver must be present simultaneously.
- Can be resource-heavy as it requires active engagement from both parties.
- Offers immediate feedback and responsiveness.
- Often simpler in concept but can be complex in resource management.
- Ideal for scenarios requiring real-time data exchange and immediate decision-making.
##### Asynchronous
- Does not occur in real-time; sender and receiver do not need to be concurrently engaged.
- More efficient in resource use, as it allows for delayed responses.
- Feedback is delayed, leading to potential lag in communication.
- Can be more complex to implement but offers greater flexibility.
- Suitable for scenarios where immediate response is not critical, and flexibility is desired.


### Microservices vs. Serverless Architecture

##### Microservices
- **Microservices** architecture is a method of developing software systems that structures an application as a collection of loosely coupled services, which are fine-grained and independently deployable.
- **Language Agnostic**: Each microservice can be written in a different programming language, depending on its requirements.
- **Scalability**: Each service can be scaled independently, based on demand.
- Teams that prefer to work independently on different parts of an application.
- Costs are based on the infrastructure provisioned, regardless of usage.
- Higher operational complexity due to the need to manage multiple services and their interactions.
- Suitable for large, complex applications where each service may have different resource requirements.
##### Serverless Architecture 
- **Serverless Architecture** refers to a cloud computing model where the cloud provider dynamically manages the allocation and provisioning of servers. A serverless model allows developers to build and run applications without managing infrastructure.
- **No Server Management**, Auto Scaling, Pay as you go, Event-driven 
- Simpler from an operational standpoint, but can have limitations in terms of function execution times and resource limits.

What are service bus?
![[Screenshot 2024-06-24 at 7.00.14 AM.png]]

### Event-Driven vs. Polling Architecture
##### Event-Driven 
- Responds immediately to events as they occur.
- Generally more efficient with system resources, as it only reacts to changes.
- Can be more complex to implement, requiring robust event handling and management.
- Suitable for real-time applications.
- Scales well, especially in distributed systems with many events.
##### Polling Architecture
- Checks for changes at regular intervals.
- Can be resource-intensive, especially with frequent polling intervals.
- Simpler to implement but may not be as responsive or efficient.
- More suitable for applications where real-time response is not critical.
- Scaling can be challenging, particularly if the polling frequency is high.





Load Balancer Types

A load balancing type refers to the method or approach used to distribute incoming network traffic across multiple servers or resources to ensure efficient utilization, improve overall system performance, and maintain high availability and reliability. Different load balancing types are designed to meet various requirements and can be implemented using hardware, software, or cloud-based solutions.

Each load balancing type has its own set of advantages and disadvantages, making it suitable for specific scenarios and use cases. Some common load balancing types include hardware load balancing, software load balancing, cloud-based load balancing, DNS load balancing, and Layer 4 and Layer 7 load balancing. By understanding the different load balancing types and their characteristics, you can select the most appropriate solution for your specific needs and infrastructure.

## 1. Hardware Load Balancing

Hardware load balancers are physical devices designed specifically for load balancing tasks. They use specialized hardware components, such as Application-Specific Integrated Circuits (ASICs) or Field-Programmable Gate Arrays (FPGAs), to efficiently distribute network traffic.

**Pros:**

- High performance and throughput, as they are optimized for load balancing tasks.
- Often include built-in features for network security, monitoring, and management.
- Can handle large volumes of traffic and multiple protocols.

**Cons:**

- Can be expensive, especially for high-performance models.
- May require specialized knowledge to configure and maintain.
- Limited scalability, as adding capacity may require purchasing additional hardware.

**Example:** A large e-commerce company uses a hardware load balancer to distribute incoming web traffic among multiple web servers, ensuring fast response times and a smooth shopping experience for customers.

## 2. Software Load Balancing

Software load balancers are applications that run on general-purpose servers or virtual machines. They use software algorithms to distribute incoming traffic among multiple servers or resources.

**Pros:**

- Generally more affordable than hardware load balancers.
- Can be easily scaled by adding more resources or upgrading the underlying hardware.
- Provides flexibility, as they can be deployed on a variety of platforms and environments, including cloud-based infrastructure.

**Cons:**

- May have lower performance compared to hardware load balancers, especially under heavy loads.
- Can consume resources on the host system, potentially affecting other applications or services.
- May require ongoing software updates and maintenance.

**Example:** A startup with a growing user base deploys a software load balancer on a cloud-based virtual machine, distributing incoming requests among multiple application servers to handle increased traffic.

## 3. Cloud-based Load Balancing

Cloud-based load balancers are provided as a service by cloud providers. They offer load balancing capabilities as part of their infrastructure, allowing users to easily distribute traffic among resources within the cloud environment.

**Pros:**

- Highly scalable, as they can easily accommodate changes in traffic and resource demands.
- Simplified management, as the cloud provider takes care of maintenance, updates, and security.
- Can be more cost-effective, as users only pay for the resources they use.

**Cons:**

- Reliance on the cloud provider for performance, reliability, and security.
- May have less control over configuration and customization compared to self-managed solutions.
- Potential vendor lock-in, as switching to another cloud provider or platform may require significant changes.

**Example:** A mobile app developer uses a cloud-based load balancer provided by their cloud provider to distribute incoming API requests among multiple backend servers, ensuring smooth app performance and quick response times.

## 4. DNS Load Balancing

DNS (Domain Name System) load balancing relies on the DNS infrastructure to distribute incoming traffic among multiple servers or resources. It works by resolving a domain name to multiple IP addresses, effectively directing clients to different servers based on various policies.

**Pros:**

- Relatively simple to implement, as it doesn't require specialized hardware or software.
- Provides basic load balancing and failover capabilities.
- Can distribute traffic across geographically distributed servers, improving performance for users in different regions.

**Cons:**

- Limited to DNS resolution time, which can be slow to update when compared to other load balancing techniques.
- No consideration for server health, response time, or resource utilization.
- May not be suitable for applications requiring session persistence or fine-grained load distribution.

**Example:** A content delivery network (CDN) uses DNS load balancing to direct users to the closest edge server based on their geographical location, ensuring faster content delivery and reduced latency.

## 5. Global Server Load Balancing (GSLB)

Global Server Load Balancing (GSLB) is a technique used to distribute traffic across geographically dispersed data centers. It combines DNS load balancing with health checks and other advanced features to provide a more intelligent and efficient traffic distribution method.

**Pros:**

- Provides load balancing and failover capabilities across multiple data centers or geographic locations.
- Can improve performance and reduce latency for users by directing them to the closest or best-performing data center.
- Supports advanced features, such as server health checks, session persistence, and custom routing policies.

**Cons:**

- Can be more complex to set up and manage than other load balancing techniques.
- May require specialized hardware or software, increasing costs.
- Can be subject to the limitations of DNS, such as slow updates and caching issues.

**Example:** A multinational corporation uses GSLB to distribute incoming requests for its web applications among several data centers around the world, ensuring high availability and optimal performance for users in different regions.

## 6. Hybrid Load Balancing

Hybrid load balancing combines the features and capabilities of multiple load balancing techniques to achieve the best possible performance, scalability, and reliability. It typically involves a mix of hardware, software, and cloud-based solutions to provide the most effective and flexible load balancing strategy for a given scenario.

**Pros:**

- Offers a high degree of flexibility, as it can be tailored to specific requirements and infrastructure.
- Can provide the best combination of performance, scalability, and reliability by leveraging the strengths of different load balancing techniques.
- Allows organizations to adapt and evolve their load balancing strategy as their needs change over time.

**Cons:**

- Can be more complex to set up, configure, and manage than single-technique solutions.
- May require a higher level of expertise and understanding of multiple load balancing techniques.
- Potentially higher costs, as it may involve a combination of hardware, software, and cloud-based services.

**Example:** A large-scale online streaming platform uses a hybrid load balancing strategy, combining hardware load balancers in their data centers for high-performance traffic distribution, cloud-based load balancers for scalable content delivery, and DNS load balancing for global traffic management. This approach ensures optimal performance, scalability, and reliability for their millions of users worldwide.

## 7. Layer 4 Load Balancing

Layer 4 load balancing, also known as transport layer load balancing, operates at the transport layer of the OSI model (the fourth layer). It distributes incoming traffic based on information from the TCP or UDP header, such as source and destination IP addresses and port numbers.

**Pros:**

- Fast and efficient, as it makes decisions based on limited information from the transport layer.
- Can handle a wide variety of protocols and traffic types.
- Relatively simple to implement and manage.

**Cons:**

- Lacks awareness of application-level information, which may limit its effectiveness in some scenarios.
- No consideration for server health, response time, or resource utilization.
- May not be suitable for applications requiring session persistence or fine-grained load distribution.

**Example:** An online gaming platform uses Layer 4 load balancing to distribute game server traffic based on IP addresses and port numbers, ensuring that players are evenly distributed among available game servers for smooth gameplay.

## 8. Layer 7 Load Balancing

Layer 7 load balancing, also known as application layer load balancing, operates at the application layer of the OSI model (the seventh layer). It takes into account application-specific information, such as HTTP headers, cookies, and URL paths, to make more informed decisions about how to distribute incoming traffic.

**Pros:**

- Provides more intelligent and fine-grained load balancing, as it considers application-level information.
- Can support advanced features, such as session persistence, content-based routing, and SSL offloading.
- Can be tailored to specific application requirements and protocols.

**Cons:**

- Can be slower and more resource-intensive compared to Layer 4 load balancing, as it requires deeper inspection of incoming traffic.
- May require specialized software or hardware to handle application-level traffic inspection and processing.
- Potentially more complex to set up and manage compared to other load balancing techniques.

**Example:** A web application with multiple microservices uses Layer 7 load balancing to route incoming API requests based on the URL path, ensuring that each microservice receives only the requests it is responsible for handling.


## Background

In Distributed Systems, data is replicated across multiple servers for fault tolerance and high availability. Once a system decides to maintain multiple copies of data, another problem arises: how to make sure that all replicas are consistent, i.e., if they all have the latest copy of the data and that all clients see the same view of the data?

## Solution

In a distributed environment, a quorum is the minimum number of servers on which a distributed operation needs to be performed successfully before declaring the operation's overall success.

Suppose a database is replicated on five machines. In that case, quorum refers to the minimum number of machines that perform the same action (commit or abort) for a given transaction in order to decide the final operation for that transaction. So, in a set of 5 machines, three machines form the majority quorum, and if they agree, we will commit that operation. Quorum enforces the consistency requirement needed for distributed operations.

In systems with multiple replicas, there is a possibility that the user reads inconsistent data. For example, when there are three replicas, `R1`, `R2`, and `R3` in a cluster, and a user writes value `v1` to replica `R1`. Then another user reads from replica `R2` or `R3` which are still behind `R1` and thus will not have the value `v1`, so the second user will not get the consistent state of data.

**What value should we choose for a quorum?** More than half of the number of nodes in the cluster:  where  is the total number of nodes in the cluster, for example:

- In a 5-node cluster, three nodes must be online to have a majority.
- In a 4-node cluster, three nodes must be online to have a majority.
- With 5-node, the system can afford two node failures, whereas, with 4-node, it can afford only one node failure. Because of this logic, it is recommended to always have an odd number of total nodes in the cluster.

Quorum is achieved when nodes follow the below protocol: , where:  
 = nodes in the quorum group  
 = minimum write nodes  
 = minimum read nodes

If a distributed system follows  rule, then every read will see at least one copy of the latest value written. For example, a common configuration could be (N=3, W=2, R=2) to ensure strong consistency. Here are a couple of other examples:

- (N=3, W=1, R=3): fast write, slow read, not very durable
- (N=3, W=3, R=1): slow write, fast read, durable

The following two things should be kept in mind before deciding read/write quorum:

- R=1 and W=N ⇒ full replication (write-all, read-one): undesirable when servers can be unavailable because writes are not guaranteed to complete.
- Best performance (throughput/availability) when , because reads are more frequent than writes in most applications

### How It Works

- **Majority-Based Quorum**: The most common type of quorum where an operation requires a majority (more than half) of the nodes to agree or participate. For instance, in a system with 5 nodes, at least 3 must agree for a decision to be made.
- **Read and Write Quorums**: For read and write operations, different quorum sizes can be defined. For example, a system might require a write quorum of 3 nodes and a read quorum of 2 nodes in a 5-node cluster.

## Use Cases

### Distributed Databases

- Ensuring consistency in a database cluster, where multiple nodes might hold copies of the same data.

### Cluster Management

- In server clusters, a quorum decides which nodes form the 'active' cluster, especially important for avoiding 'split-brain' scenarios where a cluster might be divided into two parts, each believing it is the active cluster.

### Consensus Protocols

- In algorithms like Paxos or Raft, a quorum is crucial for achieving consensus among distributed nodes regarding the state of the system or the outcome of an operation.

## Advantages

1. **Fault Tolerance**: Allows the system to tolerate a certain number of failures while still operating correctly.
2. **Consistency**: Helps maintain data consistency across distributed nodes.
3. **Availability**: Increases the availability of the system by allowing operations to proceed as long as the quorum condition is met.

## Challenges

1. **Network Partitions**: In cases of network failures, forming a quorum might be challenging, impacting system availability.
2. **Performance Overhead**: Achieving a quorum, especially in large clusters, can introduce latency in decision-making processes.
3. **Complexity**: Implementing and managing quorum-based systems can be complex, particularly in dynamic environments with frequent node or network changes.

## Conclusion

Quorum is a fundamental concept in distributed systems, playing a crucial role in ensuring consistency, reliability, and availability in environments where multiple nodes work together. While it enhances fault tolerance, it also introduces additional complexity and requires careful design and management to balance consistency, availability, and performance.


-> More details on service bus, quoram and load balancing types (might require networking knowledge more)


