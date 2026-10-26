
2024-06-27 18:40
Status: #baby 
Tags: [[4 - Tags/system design|system design]] [[distributed systems]]

# Consistency Models

(requires some clarity on some of the models discussed here)

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







# **References**