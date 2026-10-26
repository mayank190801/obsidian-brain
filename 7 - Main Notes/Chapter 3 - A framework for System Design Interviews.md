[[Alex Xu System Design Essentials]]

Important skills interviewer look for 
- Ability to ask good questions 
- Overengineering red flags 
- stubborn etc 

### Step - 1 Understand the problem and establish design scope 

- There is no right answer, don't play trivia there. 
- Thoroughly understand the requirements first and then take actions 
- Slow down and clear all the assumptions

Some good to ask questions 
- What specific features are we going to build? 
- How many users does the product have? 
- How fast does the company anticipate to scale up? 
- What are the anticipated scales in 3 months, 6 months, and a year? 
- What is the company’s technology stack? 
- What existing services you might leverage to simplify the design?

### Step - 2 Propose high level design and get buy-in

- come up with intial design (talk with your interviewer)
- Draw box diagrams 
- Discuss back of the envelope estimations to figure out if you are close or not 

Question- Should we include API endpoints and database schema here?
- For large problems probably not, but for multi-player poker game yes 
- Better ask your interviewer 

### Step - 3 Design deep dive

- Now it depends on the interviewer which direction they want this to go
- If senior, esitmations and stuff, if junior more into particular algo or stuff (unsure)
- Don't get into too much details of anything and be smart to utilise your time to showcase your design abilities 

### Step - 4 Wrap up 

- Interviewer might want you to identify the system bottlenecks, never say your design is perfect 
- recap of your design might help him 
- Error cases are interesting to talk about 
- How to figure out the next scale curve ie moving from 10MAU to 100MAU
- Propose other refinements which could have taken place 


Do's:

- Ask for clarification, don't assume your assumption is correct.
- Understand problem requirements.
- There is no right or perfect answer. A solution for a small company is different from one for a larger one.
- Let interviewer know what you're thinking.
- Suggest multiple approaches.
- Agree on blueprint and then design the most critical components first.
- Share ideas with interviewer. They should work with you.

Dont's:

- Come unprepared for typical interview questions.
- Jump into a solution without understanding the requirements first.
- Don't go into too much details on a single component at first. Design at a high-level initially.
- Feel free to ask for hints if you get stuck.
- Communicate, don't think silently.


### Time Allocation for each step 

45 minutes are not enough to cover any design into sufficient detail.

- Understand problem & establish design scope - 3-10m
- Propose high-level design & get buy-in - 10-15m
- Design deep dive - 10-25m
- Wrap-up - 3-5m