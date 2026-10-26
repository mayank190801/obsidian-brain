
2024-07-17 09:24
Status: #baby
Tags: [[5 - Indexes/System Design|System Design]] 

# DNS

### Introduction to DNS

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









# **References**

[[Grokking System Design Fundamentals]]