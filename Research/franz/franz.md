
franz is a beginner's write of a distributed message queue to understand the pub/sub architecture.

#### Motivation:
- TBD 

#### Structure and Thinking about the Project:
1. Think about the pre-reqs that are required for the system to function.
2. Need an underlying storage mechanims -> like in memory, on disk , S3 or anything.
	1. Start with memory and can have something on disk and that can store on memory or disk.
	2. So the disk itself has a interface defined for this.
3. Need a way for the storage to be attached to an top-lever structure , for our use cases , we are attaching it to the server / daemon (to connect to the instance) 
4. Then define the network layer
	1. An http, tcp server 
5. Server listens for bytes and serves the things.
6. A transport is basically how it is getting transported from your machine to other machine.
7. Most of the things going over TCP(abstracted over HTTP/ gRPC(proto buffer protocol on top of TCP)).
	1. Maybe we should have an internal protocol like Redis Protocol to communicate .
8. Adding mutex to read/ write blocks to make optimization easier.
9. Add some topics and define the Start server method to inti thosea topics to subscribe to.














