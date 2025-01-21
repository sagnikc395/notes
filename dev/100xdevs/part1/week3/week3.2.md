## Fetch, Authentication and Databases

- Fetch:
  - send HTTP requests from a real website.
- Auth:
  - auth is the real world stuff most sites need.
- DBs:
  - mongodb and how to add to the storage layer and create an end to end project.
- How to trigger requests on clicking of button ?
  - browser provides the specification , later became part of the JS specification.
  - Browsers expose fetch -> lets us fetch data from the backend.

### fetch api:

- The third way to craete a HTTP request.
- Lets says we create an HTML page:
  - where we can see the names of 10 people
  - we need to make sure that we get these data from an API call.
  - Write some frontend code that hits the backend code, hits the backend code and returns back the data.
- by default fetch will do a GET request. For POST and others, we have to send it with body along with headers.
- when we click on the response tab, we see a network call being going to the backend servers and get back the data and render on our UI.
- can also use the async/await syntax or the promise based one.

- 99.9 % website will return need to return to the backend servers.
- browsers returns fetch -> to fetch data from the backend.
- until now we have sent requests using

  - postman/hoppscotch
  - URL bar

- there is a third way:

  - using the fetch api call.

- write this frontend code, hit the endpoint and renders that on the browser -> i.e GET requests on the endpoint.
- fetch will by default send GET requests, we can customize and send POST requests as

```js
fetch(url,{
  method:"POST",
  ...
});
```

### Authentication :

- allow only registered users to see people and see content -> create a dummy people list.
- almost all website have auth.
- there are complicated ways to login.
- easiest way is a username password based auth.
- let users sign up to your website.
- some cryptography jargon to understand about auth:

  1. Hashing
  2. Encryption
  3. JSON web tokens
  4. Local Storage

- Hashing :

  - This stores the password somewhere (some database), i.e some centralized place where the passsword is stored.
  - The plaintext is stored into a hashed version to an "encrypted" form.
  - People generally repeat password -> standard practice for developers to hash the input and 1 single input will always give the same output.
  - Hashing -> converting a single string to a complicated version. Can never decrypt this back to the original plaintext. This is also called a one way function.
  - Backend servers reconfigrues into the jibberish and redoes the authentication system.
  - We do in our memory backtrack the solution and get back the password for the next login and check if the authentication is correct.
  - one-way function -> given a hash we can never guess the original string.
  - hashing does not require a password.
  - changing the input a lil bit whill change the value by a lot.

- Encryption :

  - given a string we can hash it and provided we have a key, we can get back the original message.
  - Encryption requires a password and is 2 way.
  - Encrypted thing can be decrypted , given we have a password.

- JSON Web Tokens(JWT) ->

  - it will take some JSON as input and will give us a structured data as output.
  - Takes JSON as input and differs significantly from string.
  - Returns a token at the end.
  - On their server, they will run jwt.verify(code, password) -> get back the original password and to verify the login.
  - Creates a digital signature.
  - anyone can see the original output, given the signature.
  - signatures can be verified only using the password. -> like bank i.e anyone can create it , but only the bank can verify it -> by using the password.(kept in server side, not exported)
  - JWT Summary:
    - JWT to create tokens
    - User gets back a token after the signin request
    - User sends back tokens in all authenticated requests.

- local storage ->

  - place in our browser , where we can store some data , usually things that are stored include:

    - Authentication Tokens
    - User Language Preferences
    - User Theme Preferences.

  - Client Settings and Themes.

### Databases:

- Until now , we have been storing data in memory.
- This is bad for few reasons:
  - Data can't be dynamic, if you update in memory objects, the updates are lost if the process restarts.
  - There are multiple servers in the real world.
- There are various types of DBS:
  - RDBMS
  - Graph DBs
  - NoSQL DBs
- For this class we look at MongoDB a famous NoSQL DB.

- read mongodb docs to learn more
