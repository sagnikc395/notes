
- moderately hard concept
- will require marination
- not used everywhere and but used in cal.com
- filter out from the general crowd.
- other than the basics of mern -> frontend in next, backend in node and prisma and postgres/mysql and some other niche tech
- after some point need to learn tech on our own.
- new way to write backend systems that even abstracts over the router by using adapters.

### why trpc ?
- RPC -> remote procedure calls
- if i can call a function remotely from somewhere
- traditional be-fe architecture(REST based):
	- ![[Screenshot 2024-04-02 at 8.40.03 AM.png]]
	- nuances:
		- what is GET,POST ?
		- HTTP Protocol 
- better to have a protocol that can just call the functions in our frontend wihtout understanding the HTTP protocol.
- in this case, remote procedure call is useful.
	- under the hood it uses HTTP or any other protocol.
	- but for the application developer the complexity is mitigated.
- ![[Screenshot 2024-04-02 at 8.42.40 AM.png]]
- you as the application developer just do createTodo and dont poke under the hood.
- another famous is gRPC -> defined by google.
- Written in TS uses JSON-RPC under the hood and use the functions in the frontend.

### features of trpc:
- automatic types for fe and be 
	- never had very strict type checking on frontend , trpc solves this through the communication of its types.
- generic code that can be converted to express backend and also nextjs backend ...


### how does trpc provide connections from both fe and be 
 - **adapeters**
 - hosting trpc with adapters:
	 - standalones
	 - express
	 - fastify
	 - next.js
	 - aws lambda + api gateway 
	 - we as a backend developer can write the application and any existing backend application can use the adapters and integrate.
 -  ![[Screenshot 2024-04-02 at 8.50.19 AM.png]]
 - end users just interacts with express or next etc.
 - because of this it is very nicehly popular.



- just functions, making call to a server and showing response to us.
- simply be calling the api fucntions and get by id as we send the arguments.
- vocabulary:
	- procedure -> API Endpoint ; tells that one function that end users can run.
		- They can be of 2 types: query or mutation.
	- query -> GET for getting some data for end users.
	- mutations -> UPDATE data for the end user.
	- router -> collection of procedures, like app in express.

- we have to have the input defined very strictly defined here , somewhat equivalent to express + zod validation added.
- ![[Screenshot 2024-04-03 at 8.31.40 AM.png]]
- .get -> .query 
- todoCreate -> identifier to the specific route 
- .input -> need to be very well defined and constrained by zod

### basic todo server and client ->
- init trpc 
- define router 
- use the adapter to serve the API.
- here client for us -> node server ; a client could be anything that can send http requests / consume http requests.
### init trpc:
- define a t object 
- export router := t.router
- export publicProcedure -> a procedure that lets us create other procedures.
- lets us create a bunch of queries and mutations.

- can't get specific data in trpc like graphql, all though we send all the data in graphql.

## authentication:
- using header information
- create a users procedure:
	- signup 
	- input 

### Contexts and Middleware:
- very very important for various tech and used everywhere.

### Context:
- When we initialize our router, trpc allows us to:
	- setup request context
		- whenever the user sends back a context, it is context for the specific response, usually id/session for the particular user.
		- contexts are important i.e some extra information in headers along with the standard header information.
		- another thing that is put into the context is the global database variable.
	- assign metadata to procedures
	- format and handle the errors
	- transform the data as required.
	- customize our runtime configurator.
- we can then use method chaining to initalize our t object on initialization.
- context is a request specific information.
- Your context holds data that all of your tRPC procedures will have access to, and is a great place to put things like database connections or authentication information.
- setting up the context is done in 2 steps:
	- defining the type during initialization 
	- and then creating the runtime context for each request.

- in the client, define a function called headers, right next to the url , which will return whatever headers we want in the backend.

### Dont have to use zod:
- can also other things , or can write our own validation libraries and functions of our own.

### Merging Routers:
- all the routers defined currently in a single file.
- can also define in different locations and then merge those routers together.
- add support with mergeRouter.
- can structure and merge them as routers.

### TBD in Lec2:
- Data Tranformers 
- connecting with Next.js
- Middlewares