## express and HTTP with real world examples | Postman / Hoppscotch debugging

### going to a doctor

- doctors have a skill
- they have acquired that skill over years
- they provide service to other people who want to use their skill
- to expose this life skill, they open a clinic
- people who want to use their skill line up in a waiting room.
- one by one, the doctor meets with them.
- the doctor is single threaded
- how do people reach the doctors ?

  - google address
  - once we get their address we navigate to it.

- patients wait in the waiting area.
- doctors tend to them one by one.
- async tasks delegating.

### doctors are similar to a javascript thread !

- your logic is like a doctor -> essentially single threaded, sometime async nature!
- relatives using you like a patient, relative doesnt need to find your address, they stay in the same house.

### How to expose your logic to the world ?

- HTTP comes into the picture ! It lets us create a hospital where people can comes and find us !
- How to expose the doctor functionality ?

  - by creating a HTTP server.

- How do I create HTTP server ?

  - Express for Nodejs / hono , Golang Fiber etc.

- Express is the name of a library, that lets us create a HTTP server. -> encapsulates the complexity of creating a HTTP servers that are optimized.

- Exposing the doctors one functionality -> like a route handler -> with methods like GET,POST.
- People can come in and doctor can come for various functionality.

- adress of the doctor's chamber -> port .

- can build a hopsital i.e multiple servers that can have multile doctors and various functionalities to users and return that to users back.
- the port needs to be unique for each server - otherwise it would be able to serve requests.

### Users passing input:

- query parameters:

```
?para1=arg1&para2=arg2
```

- req -> request -> anything we pass in input, or headers etc.
- res -> response -> whatever the server responds back with, status code, HTML etc, data/headers to send back.

- in our doctor example , we can think of our CRUD logic as:

  - GET -> going for a consultation to get a check up
  - POST -> going to get new metal supportrs due to fracture
  - PUT -> going to get kidney replaced.
  - DELETE -> going to get a kidney removed.

### Status Code

- 200 -> everything OK
- 404 -> not found
- 500 -> Server down
- 411 -> inputs are incorrect

### input handling

- query parameters for GET requests
- for post requests, we send requests via body
- to send posts requests , use hoppscotch to send data via body.
- cannot read properties of undefined -> isHealthy.

  - req.body translates to undefined.
  - use middlewares to parse and use bodyParser.json() -> to parse the JSON body on the server.

- backend should do a lot of input validation, handle edge cases, data cleanup, proper errors messagingin.
- some basic one in the assignment ?

  - what should happen if they try to delete when there are no kidneys ?
  - what should happen if they try to make a kidney healthy when all are already healthy ?

-
