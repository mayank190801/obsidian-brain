
2024-07-17 10:06
Status: 
Tags:

# Distributed Messaging System

### Introduction to Messaging System
- Issues its solves 
	- Extreme high number of messages per second
	- multiple aggregator services, how to divide work among them?
	- highly coupled 
	- What is all aggregator services fails?

![[Screenshot 2024-06-18 at 10.37.31 PM.png]]

- A **messaging system** is responsible for transferring data among services, applications, processes, or servers. Such a system helps **decouple** different parts of a distributed system by providing an **asynchronous** way of transferring messaging between the sender and the receiver.
- Mainly de-coupling and asynchronously transferring data from one place to another 
### Queue

![[Screenshot 2024-06-18 at 10.38.50 PM.png]]

- messages are stored sequentially in a queue
- A particular message can be consumed by a maximum of one consumer only.
- limits the system as multiple consumers cannot read the same message from the queue.

### Publish-subscribe messaging system

![[Screenshot 2024-06-18 at 10.40.23 PM.png]]

- messages are divided into topics
- A publisher (or a producer) sends a message to a topic that gets stored in the messaging system under that topic
- Subscribers (or the consumer) subscribe to a topic to receive every message published to that topic.
- if two consumers subscribe to the same topic, they will receive all messages published to that topic.
- The messaging system that stores and maintains the messages is commonly known as the message **broker**.
-  This **loose coupling** enables subscribers and publishers to read and write messages at different rates.
- **fault-tolerance**, so messages do not get lost between the time they are produced and the time they are consumed.

In Summary - 
- Messaging Buffering - (handling sudden peak of load)
- Guarentee of message deliver
- Provides abstraction 
- Scalability 
- Fault Tolerance
- Asynchronous Communication 
- Load Balancing 
- Messages Persistence 
- Security 
- Interoperability 

### Introduction to Kafka
- open-source **publish-subscribe**-based messaging system
- Kafka was created at LinkedIn around 2010
##### Use Cases
1. Reliably storing a huge amount of data.
2. Enabling high throughput of message transfer between different entities.
3. Streaming real-time data.

At a high level, we can call Kafka a distributed **Commit Log**. (understand more in depth)
![[Screenshot 2024-06-18 at 10.48.37 PM.png]]
 - A Commit Log (_also known as a Write-Ahead log or a Transactions log_) is an **append-only** data structure that can persistently store a sequence of records.
 - Records are always appended to the end of the log, and once added, records cannot be deleted or modified.
 - Reading from a commit log always happens from left to right (_or old to new_).
 - Kafka takes advantage of sequential disk reads (_more on this later_) .

Use cases 
- Metrics
- Log Aggregation 
- Stream Processing (pick from one topic and put in another topic)
- Commit Log (useful for recovery failed nodes)
- Website Activity Tracking (product suggestions)

### Kafka common terms
- Brokers - (A Kafka server is also called a broker. Brokers are responsible for reliably storing data provided by the producers and making it available to the consumers.)
- Records - (A record contains a key, a value, a timestamp, and optional metadata headers.)
![[Screenshot 2024-06-18 at 10.52.09 PM.png]]

##### Topics
- A topic is like a table in a database, and the messages are the rows in that table.
- Consumers can subscribe to a topic to get notified when new messages are added to that topic
- In a Kafka cluster, a topic is identified by its name and must be unique.
- Kafka retains messages for a configurable amount of time or until a storage size is exceeded
- Kafka's performance is effectively constant with respect to data size (hence storing data for a long time is no issue)

![[Screenshot 2024-06-18 at 10.54.39 PM.png]]

#### High-level architecture
###### Kafka cluster
Kafka is deployed as a cluster of one or more servers, where each server is responsible for running one Kafka broker.
###### ZooKeeper
- It is a distributed key-value store and is used for coordination among kafka brokers and storing configurations.
- Highly optimized for reads
- It maintains metadata information about the kafka cluster.
![[Screenshot 2024-06-19 at 10.21.49 AM.png]]

### Messaging patterns
##### 1. Point-to-Point (Direct Messaging):
- Single producer to Single consumer 
- Queue are often used to implement it (FIFO)
- Simple to implement, No intermediaries, Limited Scalability 

##### 2. Publish-Subscribe (Pub/Sub):
- Messages are sent from a producer (publisher) to multiple consumers (subscribers).
- Ideal where the information needs to be shared among multiple people, or the sender doesn't know who could be the reciever
- Decoupling, Scalable, Dynamic Subscription (consumers can added and removed dynamically)

##### 3. Request-Reply (Request-Response):
- a producer (requester) sends a message to a consumer (responder) and waits for a response.
- Synchronouse communication, Sender requires response before moving ahead 
- Inside payment gateways when the usern the consumer is waiting for the response 
- Tight coupling is there, also latency is also present (since user has to wait now)
##### 4. Fan-Out/Fan-In (Scatter-Gather):
- a message is sent to multiple consumers (fan-out), and the responses from these consumers are aggregated before being sent back to the original sender.
- tasks needs to distributed among multiple worker nodes 
- Parallelism, load balancing and also aggregration step would cost extra resources 
- Ex - A search engine sends query to multiple index servers, each of them return relevant results, which are then combined and return back to the user. 
##### 5. Dead Letter Queue (DLQ):
- This pattern is used to handle erroneous or invalid messages that cannot be processed by consumers.
- They are sent to an dedicated queue called the dead letter queue, where they can be monitored, analyzed and reprocessed.
- Help to not block the queue. 
- Error handling, monitoring and debugging, fault isolation and retention 
- Ex -  An email delivery system where messages that fail to be delivered (store is some another queue and figure out the issue by trying to redeliver it)

### Popular Messaging Queue Systems
##### 1. RabbitMQ
- It an open-source message broker 
- Supports - publish-subscribe, request-reply, and point-to-point communication.
- Flexible, extensible (more protocols using plugins), internal tools for monitoring, clustering and high availability possible 
##### 2. Apache Kafka
- distributed streaming platform - high throughput, fault tolerant and scalable messaging 
- stream processing, log aggregation and event driven architectures 
- Horizontal scalable (distributed architecture), Durability (messages are stores persistently on disk), low latency, kafka provides stream process API for real time processing 
##### 3.  Amazon Simple Queue Service (SQS)
- messaging queue provided by AWS 
- automatic scaling, reliable and secure, pay as you go model (might be or not be cost efficient)
##### 4. Apache ActiveMQ
- open-source, multi-protocol message broker
- Highly available, message persistence, Integration with spring (simple)

### RabbitMQ vs. Kafka vs. ActiveMQ
1. **Performance and Scalability:** Kafka is designed for high throughput and horizontal scalability, making it well-suited for handling large volumes of data. RabbitMQ and ActiveMQ both offer high performance, but Kafka generally outperforms them in terms of throughput, particularly in scenarios with high data volume.
    
2. **Message Ordering:** RabbitMQ and ActiveMQ guarantee message ordering within a single queue or topic, respectively. Kafka ensures message ordering within a partition but not across partitions within a topic.
    
3. **Message Priority:** RabbitMQ and ActiveMQ support message prioritization, allowing messages with higher priority to be processed before those with lower priority. Kafka does not have built-in message priority support.
    
4. **Message Model:** RabbitMQ uses a queue-based message model following the Advanced Message Queuing Protocol (AMQP), while Kafka utilizes a distributed log-based model. ActiveMQ is built on the Java Message Service (JMS) standard and also uses a queue-based message model.
    
5. **Durability:** All three message brokers support durable messaging, ensuring that messages are not lost in case of failures. However, the mechanisms for achieving durability differ among the three, with RabbitMQ and ActiveMQ offering configurable durability options and Kafka providing built-in durability through log replication.
    
6. **Message Routing:** RabbitMQ provides advanced message routing capabilities through exchanges and bindings, while ActiveMQ uses selectors and topics for more advanced routing. Kafka's message routing is relatively basic and relies on topic-based partitioning.
    
7. **Replication:** RabbitMQ supports replication through Mirrored Queues, while Kafka features built-in partition replication. ActiveMQ uses a Master-Slave replication mechanism.
    
8. **Stream Processing:** Kafka provides native stream processing capabilities through Kafka Streams, similarly RabbitMQ offers stream processing too, while ActiveMQ relies on third-party libraries for stream processing.
    
9. **Latency:** RabbitMQ is designed for low-latency messaging, making it suitable for use cases requiring near-real-time processing.
    
10. **License:** RabbitMQ is licensed under the Mozilla Public License, while both Kafka and ActiveMQ are licensed under the Apache 2.0 License.

### Scalability and Performance
##### 1. Partitioning
- process of dividing a data set into smaller, manageable pieces called partitions.
- helps in distribute messages evenly among multiple nodes
- Ex -  Apache Kafka uses partitions to divide a topic's messages
##### 2. Consumer Groups
- It is a way to manage multiple consumers of a messaging system that work together to process messages from one or more topics
- Each consumer group ensures that all messages in the topic are processed, and each message is processed by only one consumer within the group
##### 3. Load Balancing and Parallel Processing
- Load balancing refers to distributing incoming messages evenly among multiple consumers or processing units, while parallel processing involves processing multiple messages simultaneously
##### 4. Message Batching and Compression
- process of combining multiple messages into a single batch before processing or transmitting them
- For ex - Producers can batch messages together, and the system can compress these batches using various compression algorithms like Snappy or Gzip, reducing the amount of data transmitted and improving overall performance.








# **References**