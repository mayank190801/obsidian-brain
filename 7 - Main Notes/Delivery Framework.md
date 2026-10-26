
- Requirements ( 5 mins )
- Core Entities 
- API/ Interface 
- Date Flow 
- HLD 
- Deep Dives 

![[Screenshot 2025-11-04 at 10.57.39 PM.png]]

Requirements
- functional 
- non functional

Functional - 
" User/Clients should be able to " -- statements basically 	
Ex - 
- Users should be able to post tweets
- Users should be able to follow other users
- Users should be able to see tweets from users they follow

Keep maximum 3 and extremely focused


Non Functional
"The System should be able to " -- statements basically
Ex - 
- The system should be highly available, prioritizing availability over consistency
- The system should be able to scale to support 100M+ DAU (Daily Active Users)
- The system should be low latency, rendering feeds in under 200ms

With target is much more important like < 200 ms etc 


Checklist for non functionaly 

- CAP Theorem 
Basically should you prioritize consistency or availability. Parititon tolerance is given in dis



Twitter 
User 
Post 
Follow

APis 

- user should be able to read tweet 
- user shoudl be able to post tweets
- user should be able to follow a perosn 

Apis? 

GET  /tweets -> Tweet[]
	

POST /tweets -> 201 status 
		{
			message : "hello there peeps"
		}

POST  /users/{userId}/follows

Keep at it without giving up 
			











	

















