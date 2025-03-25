- Building my own HTTP server challenge in Go.
- HTTP is the protocol that powers the web. We will be building a HTTP server that is capable of handling simple GET/POST requests, serving files and handling multiple concurrent connections.
- Along the way, we'll learn about TCP connections, HTTP headers, HTTP verbs, handling multiple connections and more.

#### Stage 0 - Binding to a port 
- in the first stage , we bind our server to a port from the main loop.
- use the net.Listen package from the net package to connect.
- it takes the protocol and the ip address as parameters to connect to (along with the port number).
- it returns an connection and err tuple.
- the connection has the properties of Accept() to accept the connection and we can take action on that.

#### Stage 1 - Respond with 200
- here our server should respond to an HTTP request with a 200 response.
##### HTTP Response:
- HTTP response is made up of 3 parts , each seperated with a CRLF(\r\n)
	- Status line 
	- Zero or more headers, each ending with a CRLF 
	- Optional response body 
- Our response will look something like:
```sh 
HTTP/1.1 200 OK\r\n\r\n
```
- where :
	- HTTP/1.1 -> HTTP version 
	- 200 -> status code 
	- OK -> optional reason phase 
	- \r\n -> CRLF that marks the end of the status line 
	- Headers:
		- \r\n -> CRLF marks the end of the headers 
- For testing they will send a HTTP request and our server must respond to the request with following:
```sh
HTTP/1.1 200 OK\r\n\r\n
```


