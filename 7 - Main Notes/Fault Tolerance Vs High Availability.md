
2024-06-27 18:47
Status: #child
Tags: [[4 - Tags/system design|system design]] [[distributed systems]] 

# Fault Tolerance Vs High Availability

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








# **References**