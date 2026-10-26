
2024-07-17 09:44
Status: 
Tags:

# CDN

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










# **References**