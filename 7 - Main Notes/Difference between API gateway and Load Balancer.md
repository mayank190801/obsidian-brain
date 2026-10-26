

2024-06-27 09:12
Status: #baby 
Tags: [[4 - Tags/system design|system design]] [[api gateway]] [[load balancer]]

# Difference between API gateway and Load Balancer

- An API gateway is focused on **routing** requests to the appropriate microservice, while a load balancer is focused on **distributing** requests evenly across a group of backend servers.

- These requests specific URL that identifies the API that the client is trying to access, and the API gateway routes the request to the appropriate microservice based on this URL. 

- A load balancer used to handle requests that are sent to a single, well-known IP address, and then routes them to one of many possible backend servers based on factors such as server performance and availability.




# **References**