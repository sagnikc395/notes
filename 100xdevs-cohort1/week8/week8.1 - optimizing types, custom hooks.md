- more typescript
- zod for backend validation and why we need it.
- custom fetch hooks -> write our own custom hooks
- useSWR
- why used all thoughout all open source projects.
- till 54:26 did some TS challenges on types and generics.

### Process Managers:
- backend can go down, to check and restart that we can start index.js immediately.
- forever, pm2 are such libraries used to mitigiate it.
- PM2 is a Production Process Manager for Node.js applications with a built-in Load Balancer.
### Why backend validation?
- erroneous inputs can break your server.
- if we dont validate end user's inputs they can do malicious things. can do system ls and get access of the directory.
- started working on the week8 repo.
- hard to add checks and bounds at the top of every route.
- can keep on adding these keypad conditions and validations for different use cases or we can use a library like zod, which are meant to solve this problem. cal.com etc.
- also very useful in backend and we get types that we can use in our frontends.
	- write strict types on backend and use these types on the frontend.
- zod: a library to do backend validation ->
	- same thing that we did in the checks, except just describe that we did.
	- and we describe the object , what constraints that we have and what final form it should be.
	- in the object that we create, we pass the input in the safeParse method for it and checking its validity and gives a value and a error.
	- zod is a runtime checker, the final js also has this checks, unlike the compile time checks present in ts in the form of interfaces and types.
### custom fetch hooks:
- needs to start with use and is simply a function 
- need to return two keys : loading and todos
- useTodos ->
	- sends a backend request and set the value in the todos and is populated eventually from the db.
	- helpful for making it resuable across many things 
	- can use swr and useSWR to cache the thing.
- good refactor and can be use in many parts.