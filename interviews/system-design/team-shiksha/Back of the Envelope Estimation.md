
- Sometimes we are asked to estimate system capacity or performance requirements using the back-of-envelope estimate.
- We create common thought experiments and common perf numbers.
- Eg: Build a URL shortner for Insta,Twitter etc.
- Need to estimate what is the load we will be dealing with.
- We will be thinking about these loads, and what is the approach we should follow.
- Imp: Latency numbers, power of 2 

#### Power of 2:
- To obtain correct calcualtions, need to know the data volume using power of 2.
- 1 Byte -> 8 bits.
- 10 (power) -> 1KB 
- 20 (power) -> 1 mb ETC.

#### Latency Numbers every programmer should know
- These numbers should be able to give us this idea of these numbers (even if the numbers are outdated.)
- Eg: Write the code for LRU Cache.
- We would need to have certain thing , how much time does a certain cache takes , which level of the pipeline.
- Search the table for Latency Numbers [[8 nov 2024]]


### Building a Rate Limiter:
- from lecture 2 and lecture 3 , building the systems from scratch.
- having sort of a discussion and brainstorming session and which way to move forward.
- Next Session: Designing a rate limiter.

#### Debouncing:
- Whenever we make a search from a search engine (chrome,amazon inventory) on each keystroke they are going and making a query if will increase the api call.
- What if we add a debouncing -> wait 1s , batching the indv characters into a string before doing a API call.

#### Throttling:
- To limit the no of API calls from a service, artificially block the calls.
- Eg: Twitter allows only 300 tweets per 3 hours window.
- Eg: Google doc have 300 users have 60s read requests.
- Prevents DDOS attacks either intentional or non-intentional.
- Service would be highly available for more -> less usage of resources.
- Eg: free api is rate limited and certain requests , paid api having more uses.

- Debouncing can be easily done on the client side.
- But throttling can also be done on the client side -> add client side checks.
#### Ratelimiting:
- [[Drawing 2024-11-08 18.39.56.excalidraw| Rate Limiter Basic Architecture]]
- Rate limiting never on the client side -> client requests can easily be forged and is unreliable.
	- capture the curl for any 300 requests -> can use the API and call that n number of times -> wouldnt be able to block the api calls.
- So server side implementation makes much more sense.

- better approach:
	- remove ratelimiter from server also (to reduce the api calls)
	- add a API gateway in between -> this could take care of rate limiting on your behalf.
	- So the number of requests we send for this would reduce.
	- API gateways gives us a lot of flexibility : like checking for logic and then we can check.
	- also putting the API gateways's closer to distribution of users can reduce latency.
	- n number of ways to geoblock according to various properties.
	- in a broader sense , this is also we can do geoblocking. 

- HW: come up with a system to build a Rate limiter that can handle the load.