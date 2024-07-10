---
title: middlewares, request and responses
tags:
  - backend
  - API
  - Javascript
  - nodejs
---
### learning about middleware and request response cycles

- till now learnt about routes, what are URL and what are the methods ->
	- GET 
	- POST 
	- PUT
	- DELETE 
- other way to send data to backend :
	- why headers and body required when we have query parameters ?

- by default we can send only GET headers in the browser and not custom headers, that's why using POSTMAN for POST requests.
- most of the time we send data in the body. not in the query parameters.

### middlewares
- right now when we send the request , it goes to the app.get handler in the specific route and get back the right thing.
- middlwares are a way for us to capture the request before they reach us.
- any request that comes to us first comes to us in a middleware , it can then pass the request or stop the request.
- usually used for things like authentication , sign in using google, github etc.
	- send all the payload to auth middleware , checks and then forward it or prevents it.

- in express we add app.use(<\function-name>) as middlewares.takes 3 arguments req,res,and next.
	- first the control goes to the middleware and then it goes to that specific route.
	- it can decide whether to stop the specific request or to forward the specific request.
	- else the request just ends there.

- the way to register your middleware is to use app.use(<\method-name>) to register the middleware, at the top of the file definition.
- in middlewares we can see if we try to respond again, we will see an error that can't set the headers 2 times .
- thanks to nodejs there are a lot of middlewares available for common use cases.
- body is something which express does not give us out of the box , need to use body parser seperately for it.
- req.body becomes undefined ->
	- google 
	- the reason it there are various type of bodies and need to use external libraries to parse that and send the response in json to express
- bodyParser.json() extracts the body into JSON key value pairs.
- given input and put the output in the body value .
- we can add a middleware for route specific -> pass a third argument in the function call definition.
### status codes 
- things that server can send it back apart from text
	- status code 
	- body
	- headers
- what are status codes ?
	- the server along with the body can give back a numeric response, that determines what the state of our application backend is in.
	- 100-199 -> Informational responses 
	- 200-299 -> successful responses
	- 300-399 -> redirection messages
	- 400-499 -> client error messages
	- 500-599 -> server error messages
- 'ideal things that the server should respond with'
- JSON is a more structured way to send back the data.


### sending over HTML 
- send using tilde tags to multiline  send the HTML over using the res.send method
- or can also use res.sendFile to send the file directly. make sure to know about the co-location of the HTML file.


### using promises:

```js
function fileRead(err,data) {
console.log(data);
}

fs.readFile("a.txt","utf-8").then(fileRead);
```


- servers can talk to servers also.
-  nodejs processes can even send out responses to other nodejs processes.
- 