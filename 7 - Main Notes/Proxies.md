
2024-07-17 09:45
Status: 
Tags:

# Proxies

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









# **References**