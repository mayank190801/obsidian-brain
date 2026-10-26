[[Grokking System Design Interview]]



#### Why??

Benefits 
- User experience 
- Easy to read and share 
- Less likely to mistype 
- Analyse audience measure and click rate etc 

#### Requirements

Functional Requirements
- shorter and unique alias 
- redirect to original link 
- able to pick custom short link 
- link expiration should have some time 

Non-Functional Requirements 
- highly available 
- real time, minimum latency 
- not be predicatable 

Extended Requirements
 - Analytics of how many times clicked 
 - REST API availability 

#### Capacity Estimations and Constraints 

Traffic estimates 
- Ready heavy (100:1) read write ratio 
- 500 million new URL / month  (who gives this estimate?)
- According to read write ration - 50 B redirections per month 
- ~200 URLs / second added to the database 
- 20K/s URL redirections 

Storage estimates 
- Assuming we will store data for next 5 years 
- Total 30 B objects to store 
- Lets assume each object size ~ 500 bytes 
- Need 15TB of storage 

Bandwidth estimates 
- Total incoming data for our service ~ 200 URLS/ second x 500 bytes ~ 100KB/s
- For read requests ~ 20K/s x 500 bytes ~ 10MB/s

Memory estimates 
-  20% of URLs generate 80% of traffic
- We should cache 20% of URLs in that case 
- 1.7 B requests per day, ~20% of those ~ 170GB 
- Since multiple duplicate request, actual usage would be much less 

Hence,
**High level estimates from 500 Million new URL every month and 100:1 read write ration**

- New Urls - 200/s
- URL redirections - 20K/s
- Incoming data - 100KB/s
- Outgoing data - 10MB/s
- Storage for 5 years - 15TB
- Memory for Cache - 170GB

#### System Interface Definition

Let's decide the APIs now, since we have the requirements 

createURL(api_dev_key, original_url, custom_alias=None, user_name=None, expire_date=None)
deleteURL(api_dev_key, url_key)

- api_dev_key (unique to the user)
- custom_alias, user_name (used for enconding and optional)
- url_key (shortened url)

With the suse of api_dev_key, malicious user will be restricted, otherwise they would consume the entire thing. hence quota limited to per user

#### Database Design

1. We need to store billions of records.
2. Each object we store is small (less than 1K).
3. There are no relationships between records—other than storing which user created a URL.
4. Our service is read-heavy.

Two tables you can image 

- URL Table 
	- Primary Key - shortened URL   (varchar)
	- OriginalURL (varchar)
	- UserID (int)
	- ExpirationDate (datetime)
	- CreationDate (datetime)
- User Table 
	- Primary Key - UserID - (int)
	- CreationDate (datetime)
	- LastLogin (datetime)
	- Name (datetime)
	- Email (datetime)

Since we anticipate storing billions of rows, and we don’t need to use relationships between objects – a NoSQL store like [DynamoDB](https://en.wikipedia.org/wiki/Amazon_DynamoDB), [Cassandra](https://en.wikipedia.org/wiki/Apache_Cassandra) or [Riak](https://en.wikipedia.org/wiki/Riak) is a better choice. A NoSQL choice would also be easier to scale. Please see 'SQL vs NoSQL' for more details.

#### Basic System Design and Algorithm








