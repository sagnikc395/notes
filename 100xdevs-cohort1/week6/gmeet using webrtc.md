
## About:
- making a gmeet clone using webRTC and socket.io
- NICHE CLASS 

## Why go nicher?
- webRTC -> niche tech ; huge growth in 2020
- pure video streaming 
- actual theoretically is very huge and theoretical.
- know how to search niche technologies and how to target them.
- Easier for people to know base technolgoies and not marketable.
- Everyone mostly uses meta-frameworks like Nuxt and Next and at base uses React and Vue. not a better job, purely because it is harder to understand and oppurtunities are more.
- there are good niches and bad niches (in terms of money):
	- if you like a specific tech, do that 
	- learn current niche tech.
- webRTC today is not a good niche, AI and web3 are the best niche -> depends on the bull run.
- there is a learning path, most baseline knowledge can be understood better in ~ 3 months.
- zoom is based on webRTC and google captures the webrtc calls that are happening.
- things that power live video:
	- webRTC.
- increased stock prices of many companies like zoom, streamyard and got acquired for 250 mill.
- ![[Screenshot 2024-03-12 at 7.49.51 PM.png]]
- the right way to do it:
	- keep throwing your hands left,right and center. 
	- dont need to build the best thing on day0 , build on things that can be better to be developed.
- Overdeliver at start and then develop over time.
## How to learn WebRTC:
	1. Websockets(general real time comm)
	2. WebRTC in the same tab 
	3. WebRTC across the internet
- Real Time Communication:
	- Incrementally keep sending the fetch request on route and update the list  -> polling.
		- without having to refresh the page, the update data comes from the server.
		- since fetch is calling each time we are calling the fetch.
		- bad as , lots of time the server data might have not got updated.
		- how do we deermine the time to update ?
		- not feels snappy.
	- in polling, your browser send requests after certain time.
	- in web sockets, we do server side events, where the server sends events without asking from it.
	- whenever a new todo is added, websockets lets us fetch the data asynchronously whenever the data in a certain section is changed through a pipe.
- what is HTTP?
	- protocol with the status code.
	- websockets are also a protocol.(IETF)
	- the doc explains what the protocol should look like.
	- imp thing is to how to use it to build it to make real time communication.
## Making a backend websockets server:
- make a empty nodejs project.
- the API is very similar to HTTP, changes very little and can understand the intracacies of the black box of websockets.
- there are lot of libraries that providers a good interface and higher level api over websockets like socket.io.
- can use bidirectional socket without prior requests.
- Eg: chat is also a bidirectional use of websockets. can also poll or can can ask the server using websockets.
- can run websockets without express as well, but socket.io uses express.
### Socket.io basics:
- websocket library.
- it is composed of 2 parts:
	- a server that integrated with on the Node.js HTTP server socket.io
	- a client library that loads on the browser side socket.io-client
- socket.emit will send the event to the websocket the event to the server and the server's responsibility is to forward it to other clients.

## How can to send video across tabs ?
- for chat, there is a central server , taking input from a tab and sending back data to different tabs/ clients.
- every 1s , 60 frames of phots need to be send.
- 30 frames/second -> 30 images / second.
- WebRTC needs to take video and need to send to the other browser. (30 images to be send in 1 sec.)
- very hard to do via TCP protocol.
- in video , even if a frame is missed, its fine. so we use UDP for that.
- UDP -> Another protocol, not as reliable or retries as TCP. It just sends the data and not just care if sent or not.
- in video it's fine if we skip some segment. So websockets dont work, rather we use WebRTC protocol.
- webrtc designed in a peer-to-peer fashion. meaning , browsers talk to each other, and we do not necessarily need a server.
## How does webRTC work peer-to-peer?
- simple p2p architecture 
- we dont know what the other user's URL is 
- the way to identify a server is via url and port 
- how do i as a browser find the other side ?
- the way to do that is using **[STUN](https://www.3cx.com/pbx/what-is-a-stun-server/)**
- what if there is a public ip and port to send to the machine here ?
	- to find the port and ip , people can find me easily ->
		- using a STUN server, whenever we send it a request, it returns with a IP and the port through which it returns to the server.
	- the general lifecycle:
		- browser1 will connect to a stun server and stun will respond back, same with browser2 and same thing. and then they connect with each other.
		- ip,port from b1 and connect with websocket to b2 with the given ip and port.
		- ws in the signalling server.
	- for the initial handshake that we need to go and complete the initial handshake.
	- creating offer and receiving the offer.
	- signalling , websocket server and p2p.
- webrtc protocol:
	- stun server 
	- ice candidates
	- PeerConnection object 
	- localDescription
	- remoteDescription 
	- tracks

- localDescription and rootDescription is where we store the candidate information.

- 