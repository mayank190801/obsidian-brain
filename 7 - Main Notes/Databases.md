
2024-07-17 09:52
Status: 
Tags:

# Databases

## Databases 

### Introduction to Databases
- A database is an organised collection of structured data that is stored and managed electronically.
- managing, storing, and retrieving data efficiently
##### Database Management Systems (DBMS)
- A Database Management System (DBMS) is software that interacts with users, applications, and the database itself to capture, store, and manage data
- The primary goal of a DBMS is to ensure that data remains consistent, secure, and easily accessible.

Two Main Types 
- **Relational Database Management Systems (RDBMS):** These systems store data in tables with predefined schema and relationships between them. The most common query language for RDBMSs is SQL (Structured Query Language). MySQL, PostgreSQL etc. 
    
- **Non-Relational Database Management Systems (NoSQL):** These systems store data in various formats, such as key-value, document, column-family, or graph. NoSQL databases are known for their ability to scale horizontally and handle unstructured or semi-structured data. MongoDB, Redis, Apache Cassandra and Neo4j

##### High level differences between SQL and NoSQL
- Schema is fixed (if modify then modify the whole data and go offline), Schema is dynamic 
- SQL (structured query language) for defining and manipulating the data, In NoSQL the database queries are focused on a collection of documents - UnQL (Unstructured Query Language)
- SQL - Vertical Scaling, NoSQL - horizontal scaling 
- SQL - Acid compliant, NoSQL - partial ACID for availability and partition tolerance

### SQL Databases
- SQL databases follow the ACID properties (Atomicity, Consistency, Isolation, Durability) to ensure reliable data transactions.
- **Indexes:** Database indexes are data structures that help to speed up data retrieval operations. They work similarly to the index in a book, allowing for faster lookups and searches.
- SQL is a standardized language for managing and querying relational databases.
	- **Data Definition Language (DDL):** Allows for the creation, modification, and deletion of database structures, such as tables, indexes, and constraints.    
	- **Data Manipulation Language (DML):** Enables data insertion, updating, deletion, and retrieval operations on database tables.
	- **Data Control Language (DCL):** Deals with user permissions and access control for database objects.
	- **Transaction Control Language (TCL):** Manages database transactions and ensures ACID compliance. 

### NoSQL Databases
- also known as "Not Only SQL" databases
- Query languages, depending on the specific type of NoSQL database being used.
- perform well under specific workloads, such as high write loads or large-scale data storage and retrieval.
##### Types of NoSQL Databases

![[Screenshot 2024-06-14 at 4.37.09 PM.png]]
###### 1. Key-value databases
- key is a unique identifier and the value is the associated data
- Best case - high write and read performance for simple data models, such as session management and real-time analytics.
- **Examples:** Amazon DynamoDB, Azure Cosmos DB, Riak.
###### 2. In-memory key-value databases
- primarily stored in memory
- minimal response times (eliminating disk access)
- risk losing data upon a process or server failure
- It can persist data on disks by storing each operation in a log or by taking snapshots.
- **Examples:** Redis, Memcached, Amazon Elasticache.
###### 3. Document databases
- structured similarly to key-value databases
- except that keys and values are stored in documents written in a markup language like JSON, BSON, XML, or YAML.
- nested fields, arrays, and other complex data structures
- User profiles, product catalogs
- **Examples:** MongoDB, Amazon DocumentDB, CouchDB.
###### 4. Wide-column databases
- based on tables but without a strict column format
- Rows do not need a value in every column
- segments of rows and columns containing different data formats can be combined. (what does that mean??)
- **Examples:** Cassandra, Accumulo, Azure Table Storage, HBase.
###### 5. Graph databases
- map the relationships between data using nodes and edges
- Nodes are the individual data values, and edges are the relationships between those values.
- Social graphs, recommendation engines
- **Examples:** Neo4j, Amazon Neptune, Cosmos DB through Azure Gremlin.
###### 6. Time series databases
- store data in time-ordered streams
- Data is not sorted by value or id but by the time of collection, ingestion, or other timestamps included in the metadata.
- Industrial telemetry, DevOps
- **Examples:** Graphite, Prometheus, Amazon Timestream.
###### 7. Ledger databases
- based on logs that record events related to data values
- data changes that are used to verify the integrity of data.
- Banking systems, registrations
- **Examples:** Amazon Quantum Ledger Database (QLDB).

##### Pros and cons of using NoSQL databases
- schema-less design
- accommodate new data types without the need for extensive schema modifications
- built-in support for data replication, sharding, and partitioning
- superior performance under specific workloads, such as high write loads, large-scale data storage and retrieval, and complex relationships.
- NoSQL databases often prioritize Availability and Partition Tolerance over Consistency, resulting in a trade-off known as “eventual consistency.”
-  not be as expressive or versatile as SQL when it comes to complex data manipulation and analysis
- need to learn multiple query languages and paradigms when working with different types of NoSQL databases.

Things to consider 
- Deployment
- Monitoring 
- Backup and Recovery 
- Security 
- Community and Support 
- Cost 

### ACID vs BASE Properties
##### ACID Properties

![[Screenshot 2024-06-15 at 1.01.52 PM.png]]

- **Use Cases**: Ideal for systems requiring high reliability and data integrity, like banking or financial systems.
##### BASE Properties

![[Screenshot 2024-06-15 at 1.03.20 PM.png]]
- favoring availability over consistency.
- **Use Cases**: Suitable for distributed systems where availability and partition tolerance are more critical than immediate consistency, like social networks or e-commerce product catalogs.
- some level of data inconsistency.

### SQL Normalization and Denormalization
###### SQL Normalization
- Normalization in SQL is a database design technique that organizes tables in a manner that reduces redundancy and dependency. 
- It involves dividing a database into two or more tables and defining relationships between them to achieve a more efficient database structure.
- Avoids duplication of data.
- Ensures data accuracy and consistency.
- **Normalization** is about reducing redundancy and improving data integrity but can lead to more complex queries.

( Study Normalization even more achche se )***
###### Levels (Normal Forms)
- **1NF (First Normal Form)**: Data is stored in atomic form with no repeating groups.
- **2NF (Second Normal Form)**: Meets 1NF and has no partial dependency on any candidate key.
- **3NF (Third Normal Form)**: Meets 2NF and has no transitive dependency.

###### SQL Denormalization
- Denormalization, on the other hand, is the process of combining tables to reduce the complexity of database queries. 
- This can introduce redundancy but may lead to improved performance by reducing the number of joins required.
- **Improves Query Performance**: Reduces the complexity of queries by reducing the number of joins.
- In read-heavy database systems where query performance is a priority.
- **Denormalization** simplifies queries but at the cost of increased data redundancy and potential maintenance challenges.

If read heavy - then prefer denormalization, since you don't have to perform join optimisations

### In-Memory Database vs. On-Disk Database

###### In-Memory Database (IMDB)
- Primarily stores data in the main memory (RAM) of the server.
- Some can persist data on disk, but the primary data access and manipulation happen in memory.
- Offers high performance and low latency, efficient for read-heavy operations and complex, real-time computations.
- Use case : Real time analytics, Caching, Session Storage
- Limitations : Cost, Scalability and Data Volatility (unless maintained with persistance mechanism)
- Examples - Redis, Memcached, SAP HANA, Apache Ignite
###### On-Disk Database
- Stores data on persistent disk storage (HDD or SSD).
- slower due to disk I/O operations
- More suited for applications where the speed of data access is less critical.
- Use cases: Transactional Systems, Large Data sets, General Purpose Databases
- Speed and I/O Bottlenecks are limitations 
- Example - MySQL, PostgreSQL, MongoDB, Oracle Databse, Microsoft SQL server, SQLLite

### Data Replication vs. Data Mirroring

##### Data Replication
- It involves copying data from one location to another. The replication can be synchronous or asynchronous.
-  Often creates multiple copies of data, which can be stored across different servers or locations.
- Enhances data availability and accessibility, 
- used for load balancing, 
- enables data analysis without impacting the primary data source.
##### Data Mirroring
- the process of creating an exact replica of a database or storage system, usually in real-time.
- synchronous, data is always in sync in both primary and mirror locations 
- In critical applications requiring high availability and data integrity, such as financial transaction system
- Primarily for disaster recovery and high availability.

### Database Federation
- Federated databases integrate data from different sources, which can include both traditional databases and other forms of data repositories.
- data remains in its original location but is logically unified
- can combine data from different types of databases (such as SQL, NoSQL, XML databases)
-  allow queries to span across multiple databases
- Use cases : Enterprise Data Access, Business Inteligence and Analytics, Data warehousing, Mergers and Acquisitions
- Advantages - Reduced Complexity (no need to physically move/replicate data), Flexibility (easy to add and remove data), real-time access 
- Challenge - Performance, Security and Compliance, complex queries (requires advanced techniques)









# **References**