
2024-06-27 18:33
Status: 
Tags: [[4 - Tags/system design|system design]] [[distributed systems]] [[concurrency]]

# Concurrency Control

Primary Goal : Manage access to shared resources (like data or hardware resources) in an environment where multiple processes or threads are executing simultaneously.

Focus : It is concerned with how to handle situations where multiple processes need to access or modify shared data at the same time.

- **Locking:** Locks are used to restrict access to shared resources or data, ensuring that only one process can access them at a time.
- **Optimistic concurrency control:** This approach assumes that conflicts are rare and allows multiple processes to work simultaneously. Conflicts are detected and resolved later, usually through a validation and rollback mechanism.
- **Transactional memory:** This technique uses transactions to group together multiple operations that should be executed atomically, ensuring data consistency and isolation.


(this is a huge topic on its own, you will definitely come across so much in here, figure that out)

# **References**