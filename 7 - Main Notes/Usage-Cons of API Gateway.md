
2024-06-27 09:15
Status: 
Tags: [[4 - Tags/system design|system design]] [[api gateway]]

# Usage-Cons of API Gateway

Usage of API gateway (tons of usages)
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

Cons of API Gateway
- Single point of failure
- latency
- vendor lockin
- cost
- maintenance overhead 
- complexity to setup




# **References**