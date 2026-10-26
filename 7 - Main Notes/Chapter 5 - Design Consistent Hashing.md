[[Alex Xu System Design Essentials]]

- To achieve horizontal scaling, it is important to distribute requests/data efficiently and evenly across servers.

### The Rehashing Problem

- Normally we hash the request in such fashion - (serverIndex = hash(key) % N)
- Works well when N is fixed 
![[Screenshot 2024-08-28 at 10.38.05 AM.png]]

As soon as even one server goes offline, almost all the requests are now distributed to different servers 
- This causes a lot of cache to connect to the wrong servers 
- Causing a storm of cache miss 
- But why cache will miss? 
- Imagine a scenarion of memcached a distributed cache structure, which stores keys in different servers. Now suppose the above happens, it would cause hell lotta cache miss !! 

Normally the solution is basically remap all the keys to different servers 
- Benefit of consistent hashing is only k/n keys need to be remapped on average, where k is the number of keys, and n is the number of slots.

### Hash space and hash ring
- Assuming SHA-1 is used as a hash function f
- Output range is x0 .... xn (where x0 = 0 and xn = 2^160 - 1) 

![[Screenshot 2024-08-28 at 10.47.34 AM.png]]

![[Screenshot 2024-08-28 at 10.47.47 AM.png]]

### Hash Servers 
