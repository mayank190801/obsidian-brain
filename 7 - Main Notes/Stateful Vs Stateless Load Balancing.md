
2024-06-27 08:50
Status: #child
Tags: [[4 - Tags/system design|system design]] [[load balancer]]

# Stateful Vs Stateless Load Balancing

Stateless
- It operate without maintaining any information about the clients' session or connection state.
- They make routing decisions based solely on the incoming request data, such as the client's IP address, request URL, or other headers.
- quickly and efficiently

Ex -  A stateless load balancer can allocate requests to servers based on the user's geographic location, without retaining any session data.

Stateful 
- It preserves session information between requests.
- It assigns a client to a specific server and ensures that all subsequent requests from the same client are directed to that serve
- Two types - Source IP Affinity and Session Affinity

1. Source IP Affinity 
	- It assigns a client to a specific server based on the client's IP address.
	- Issues if the client's IP address frequently changes, such as in mobile networks.

2. Session Affinity
	- It allocates a client to a specific server based on a session identifier, such as a cookie or URL parameter.
	- No issues even if client's IP address changes in future 



# **References**