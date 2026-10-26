
2024-06-27 18:46
Status: #baby 
Tags: [[4 - Tags/system design|system design]] [[distributed systems]]

# Resilience and Error Handling

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






# **References**