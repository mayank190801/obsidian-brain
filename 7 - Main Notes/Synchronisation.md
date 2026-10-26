
2024-06-27 18:35
Status: #baby 
Tags: [[4 - Tags/system design|system design]]  [[distributed systems]] 

# Synchronisation

Primary Goal: It is to coordinate the timing of multiple concurrent processes or threads. It's about managing the execution order and timing of processes to ensure correct operation.

Focus : It ensures that concurrent processes execute in a way that respects certain timing constraints, like making sure certain operations happen before others or that operations do not interfere destructively with one another.

(go deeper into all these once - useChatGPT)
- **Barriers:** Barriers are used to synchronize the execution of multiple processes or threads, ensuring that they all reach a specific point before proceeding.
- **Semaphores:** Semaphores are signaling mechanisms that control access to shared resources and maintain synchronization among multiple processes or threads.
- **Condition variables:** Condition variables allow processes or threads to wait for specific conditions to be met before proceeding with their execution.



# **References**