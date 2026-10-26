Acronym
FCC + SLEDS
F ault Tolerance C AP C ompliance
S calability L atency E nvironment D urability S ecurity

### Requirements (5 minutes)
- Functional Requirements - what user can do stuff 
- Non Functional Requirements - Latency, number of requests etc (quantifiable rather than vague pls)
	 - CAP Theorem (consistent or available?  partition tolerance is given to be there )
	 - Environment Constraints (phone only or something)
	 - Scalability (special days where more traffic, read:write ratio is important - read heavy, write heavy)
	 - Latency 
	 - Durability (data loss how serious?)
	 - Security 
	 - Fault Tolerance (redundancy, failover and recovery mechanisms)
	 - Compliancy (data protection laws)
-  Capacity Estimation 
	 - like to skip estimations upfront, will do the math while designing stuff 
	 - numbers calculation when it impacts the actual design is more meaningful

### Core Entities (2 minutes)
- first figure out entities, basic ones would work 
- After that start writing the columns belonging to it 
- Twitter - (User, Tweet, Follow) - example 
- Be good at naming entities please 

### API or System Interface (5 minutes)
- REST, GraphQL, RPC, Websockets etc 
- Ideally REST, and design your core api first 
- Auth token in the request header and not in the body (user impersonation can happen)
- Tweets (plural for collections pls)
```java
POST /v1/tweets
body: {
  "text": string
}

GET /v1/tweets/{tweetId} -> Tweet

POST /v1/follows
body: {
  "followee_id": string
}

GET /v1/feed -> Tweet[]
```
![[Screenshot 2023-08-27 at 4.08.45 PM.png]]

### (Optional) Data Flow (5 minutes) 
- define the data flow via a simple list
- high level sequence of actions basically 
- first this, then that and so on.... 

### High Level Design (10-15 minutes)
- drawing boxes and arrows 
- server, databases, caches etc 
- practise the software beforehead (don't fumble there)
- keep it simple, and with time add more complexity (sometimes simple callout and written note works)
- Talk throughout the process, tell what you are thinking 
- When request reached your database, good time to start identifying the columns for each entity (directly next to database)

![[Screenshot 2026-01-07 at 12.59.26 AM.png]]

### Deep Dives (10 minutes)
- harden the design so that it meets all the non functional requirements 
- addressing edge cases
- identifying issues and bottlenecks 
- improving the design acc to interviewer inputs 
- don't talk too much, collaborate as well (don't be red flag)




SOME GOOD COMMENTS

"I haven't actually thought about the choice yet, apart from the fact that I would definitely need a persistent store that would store structured/unstructured/key-value (choose depending on the use case) data. May be I would be better able to dive deeper into this choice when I have a more holistic high-level view of the entire system. Let me note this down as this definitely is a critical part of this whole architecture"












