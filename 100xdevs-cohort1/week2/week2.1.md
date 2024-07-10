---
title: express, node and backend systems
tags:
  - "#backend"
  - nodejs
  - Javascript
---
## backend systems 

- learning basics backend design using nodejs and express
- why and how fullstack was developed ?
- learn how basic communication happens on the internet.

### how to communicate with server:
1. Request Methods
2. URL Routes 
3. Query Parameters , Headers and Body
4. Status Codes
5. Response, HTML,JSON,Test

### client server model, HTTP servers and express

- pre internet days:
	- had a lot of wires, had lot of ethenernet and connect and stuff
	- had large universities where research happend, where there were big machines and run algorithms on each of these machines seperately.
- never could anyone else talk to these machines 
	- for having some compute
	- today this is possible with the modern compute stack and also with the help of chatgpt and returns the output of the compute to us.
- need some ways the computer to talk to each other:
	- ie. send some input and get the computation of the output
	- and the server can respond to the client and gives the output for the input we gave to it.

 - the question is how do you do that ?
	 - essentially very complicated process, especially if we have to write this in code.
	 - there is a very defined way of how machines talk to each other.
		 - PROTOCOLS -> defined set of rules about how 2 machines communicate
	- we have to worry about how the protocol work in layer5.
	- HTTP works for that -> 
		- defined set of rules on how they need to communicate 
		- how to handle incoming traffic and how to control outgoing traffic
		- Hyper Text Transfer Protocol.
### Client server Model:
![[Screenshot 2024-04-28 at 10.04.28 PM.png]]
- one machine needs to a client, one needs to be a server .
- there are limited very machines in the world, and a lot of clients that want to connect to the server.
- any big business, is to make profit and gate access to the resources and to derive profit.
- use the HTTP protocol to communicate and to make servers and clients.

### intricacies of the protocol
- do the computations that you want, render the process and return the result to the client.
- needs to allow anyone to talk to it and they give it some input 
- the way it does it through is called the HTTP server.
- people started making fullstack applications with the backend and the frontend to make them useful for others to use and to access sites on their fingertips.

### how does the communication happens ?
- different layers (7 layers) at which communication happen
- request has a bunch of parameters that we need to send in the request.
- but first we need to know first where we need to send the request.
- we have so many servers available on the internet ->
	- to know something we need to know the location where we need to send the data
	- URL -> to identify who we need to talk to
	- URL + route is the most important thing while we are talking to a backend server.

### backend basics:
- can read from a file using the fs module 
- input using a very nice api
- that is the use cases for libraries and packages in the ecosystem
- npm -> node pacakge manager
- express not shipped with nodejs and npm ; need to import it externally using npm

### package.json and package.lock.json
-  to lock the versions for the development and to able to install in a new machines with a minimum config.
- not need to worry about it for the longest time.

### most of the times, need to know the higher level api to interact with stuff in node.js -> don't need explicit code knowledge and the internal functions it has 

- don't have to care about how to externally write a http server internally, need to only care about the inputs that we need to send to it.

- app.port sets up the port for the application
- http server should always be ready to receive request -> 24h availability is required, and also makes sure that app runs indefinitely.

- app.listen to start the server by passing the port and some callback function.
- app.get, app.post  etc other methods to different actions that we can take part in.
- each route does a different thing ->
	- app.get will call one methods
	- app.post will call another method and so on...


### handling input from user:
- can be passed in request body or it in the parameter itself.
- query params, headers and body are the 3 ways in which we can send data to the backend.
- to send more in query parameter ; after the route add a? and join the others using & between the parameters.


- http need to pass along some input along with the url to do some meaningful work.
- http servers handle a variety of things , apart from other things.
- every server need to take some input, do some work and handle the result.
- most of the arguments and the methods in real world, the inputs to the service will be given by the end users.
- need to tell what to do with the URL, that is the method for it:
	- GET
	- PUT
	- POST 
	- DELETE
- catchall :
	- app.get("/:username",handler)
		- : anything means that this is a wildcard and handles accordingly for it.



