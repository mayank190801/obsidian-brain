
2024-07-17 09:53
Status: 
Tags:

# Indexes

### What are Indexes?
- The goal of creating an index on a particular table in a database is to make it faster to search through the table and find the row or rows that we want
- Example - Library Catalog

![[Screenshot 2024-06-15 at 4.36.29 PM.png]]

- Simply saying, an index is a data structure that can be perceived as a table of contents that points us to the location where actual data lives
- Finding a small payload in such a large dataset can be a real challenge, since we can’t possibly iterate over that much data in any reasonable time
##### Purpose of Database Indexes
- **Faster Data Retrieval** (reduction in disk I/O operations and CPU usage)
- **Sorting and Ordering** (quickly sort the data using indexes)
##### How Indexes Improve Query Performance
- **Reduced Table Scans** (avoid full table scans)
- **Efficient Data Access** 
- **Index Selectivity** (indexes with high selectivity, reduces the numbers of rows to be accessed)
##### How Indexes decrease write performance?
- require additional storage space
- slow down write operations (insert, update and delete) as the indexes must be updated along with the table 
- Adding unnecessary indexes on tables should be avoided and indexes that are no longer used should be removed. (since updation is required on each write operation)
- If more write, and less read (then kindly do not use it)

### Types of Indexes
##### 1. Clustered Indexes
- It determine the physical order of data storage in a table
- sorted and stored based on the columns specified in the clustered index
- only be one clustered index per table
- high efficient for range queries
- Example - In a table with a clustered index on the 'DateOfBirth' column, the rows would be stored in the order of the 'DateOfBirth' values.
##### 2. Non-Clustered Indexes
- It do not affect the physical order of data storage in a table
- maintain a separate data structure that points to the rows in the table
- Multiple non clustered indexes can created per table 
- Example - In a table with a non-clustered index on the 'LastName' column, the index would store pointers to the rows sorted by the 'LastName' values, while the actual table data remains unordered.
##### 3. Unique Indexes
- It ensures that the indexed columns do not contain duplicate values
- **Example:** In a table with a unique index on the 'Email' column, no two rows can have the same email address.
##### 4. Partial Indexes
- only a subset of rows in a table based on a specified filter condition
- large table has a relatively small number of rows that are frequently queried
- **Example:** In a table with a partial index on the 'Status' column where the condition is "Status = 'Active'", only rows with an 'Active' status would be included in the index.
##### 5. Filtered Indexes
- only a subset of rows based on a specified filter condition
- filtered indexes are specific to Microsoft SQL Server
- provide additional optimisation options for queries with specific predicates.
- **Example:** In a table with a filtered index on the 'ProductID' column where the condition is "Price > 100", only rows with a price greater than 100 would be included in the index.
##### 6. Full-Text Indexes
- designed to support complex text-based searches, such as natural language queries or pattern matching
- **Example:** In a table with a full-text index on the 'Description' column, users can search for rows containing specific words or phrases in the 'Description' field.
##### 7. Spatial Indexes
- used to optimize queries involving spatial data types, such as geometry or geography data
- **Example:** In a table containing location information, a spatial index on the 'GeoCoordinates' column would enable fast retrieval of nearby locations based on latitude and longitude coordinates.








# **References**