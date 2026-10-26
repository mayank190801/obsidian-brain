
2024-07-17 09:55
Status: 
Tags:

# Bloom Filters

### Introduction to Bloom Filters

- a space-efficient and probabilistic data structure
- to quickly find if an element might be present in a set.
- It returns false positives but accurate no ie. if it returns true, then the element could be present or it could not be present. But if it return false, then it definitely does not exist 
- It is a tradeoff between spaced used vs accuracy (if we increase the space more accuracy will be there)
###### Basic Principles
- two main components: a bit array and a collection of hash functions
- The bit array is initially set to all zeroes, and the hash functions are used to map elements to positions in the bit array
- hash functions should ideally be independent and uniformly distributed to minimize the probability of false positives.
- Hash function generates three position suppose, so if we are inserting we will mark all these positions as 1, later on while checking if something exist we can use these three function and check if all three values are 1 or not (if even one bit is set to 0, we can definitely know it was never inserted)
![[Screenshot 2024-06-15 at 7.48.42 PM.png]]
##### Purpose and Use Cases
-  situations where storage space is limited, and exact membership testing is not critical
- It can be used to efficiently check if a requested web resource is present in the cache.
- Spell Checking, Network Routing, Data synchronization
- Best use case - NoSQL database, before going to search for an index in the entire database they use bloom filter to have surety whether to go searching for that index or not 
- Or earlier chrome used to use this in order to know if for a malicious url, they should be searching their entire database or not 
##### Benefits 
- Space Efficiency - uses bit array to store information about the elements in the set, (far less compared to hashset and set) 
- Time Efficiency - constant time compexity O(1) for both insertion and query
- No False Negatives
- Scalability - large number of elements with minimal increase in storage space
- Easy union and intersection of two bloom filters - Just OR ya AND on both Bit arrays 
##### Limitations 
- False positives 
- No Removal of elements - if one time a bit is set to 1, we set it back to zero (it could affect other elements)
- No extraction of exact element - if you want, require use of another data structure with it
- Dependency on Hash Function - poor hash function -> more false positives (hence proper analysis is required here)
- Tuning parameters - bit array and hash functions to achieve optimal performance

### Variants and Extensions of Bloom Filters

###### 1. Counting Bloom Filters
- Using array of counters instead of a simple bit array
- Gives ability to delete, as each counter can be incremented or decremented
- Comes at the cost of extra space and complexity
###### 2. Compressed Bloom Filters
- reduce the storage overhead by compressing the underlying bit array
- compression techniques - run-length encoding/ Golomb coding
- Additional computation overhead during insertion and query 
###### 3. Spectral Bloom Filters
- designed to estimate the frequency of elements in a dataset
- uses multiple standard Bloom filters in parallel, each representing a different frequency range
- Used in data mining or network traffic analysis.
###### 4. Scalable Bloom Filters
- issue of dynamically growing datasets by automatically adjusting the filter's size and parameters as the number of elements increases
- maintain a target false positive rate while accommodating an unpredictable number of elements.
###### 5. Cuckoo Filters
-  similar functionality with improved space efficiency and support for element removal
- combination of cuckoo hashing and a compact fingerprint representation of elements to achieve these benefits
- cuckoo filters can outperform standard Bloom filters (in multiple scenarios)

### Applications of Bloom Filters (can do deeper in this one whenever you want to)
###### 1. Database Systems
- Bloom filter as a pre-filter, unnecessary disk reads can be avoided when querying for non-existent keys
- In distributed databases, Bloom filters can also help reduce network overhead by minimizing the number of remote requests for non-existent data.
###### 2. Network Routing and Traffic Analysis
- I did not get this one
###### 3. Web Caching and Content Distribution
- By using a Bloom filter to represent the contents of a cache, a proxy server can quickly determine if a requested resource is in its cache or not, reducing unnecessary cache misses and network requests
###### 4. Spam Filtering and Malware Detection
- By querying the filter, incoming messages or files can be quickly checked against the known signatures, allowing for efficient filtering of unwanted content.
###### 5. Distributed Systems Membership Testing
- Bloom filters can be utilized to perform efficient membership testing for sets shared among multiple nodes.









# **References**