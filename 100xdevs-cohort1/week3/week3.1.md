---
title: finishing backend, starting frontend
tags:
  - nodejs
  - frontend-foundations
  - Javascript
---
- we started learning about how to expose to the world using express and cors , dont need to explicitly know how to create http servers and difficult to know is middlewares and how to expose them to other services.
- databases and authentication are 2 other things we need to know while creating and frontend ->
	- connecting frontend to backend is how to build actual backend services.
 
- learn about AJAX , cores and DOM, connecting frontend to backend.

### arrow functions 

- another way of writing functions in js.
```js 

const func = (req,res) => {
  res.json(todos);
}

app.get('/todos',func);

```
- they look more consicise and better for the function overall and look better.
- very subtle difference between normal functions and arrow functions , 
- [Differences](https://dmitripavlutin.com/differences-between-arrow-and-regular-functions/)


### using api 

- create a express http server that will mock a todo app.
  - dont use any database, just store all the data in a array tp store the todo list data in-memory.
  - hard todo: try to save the responses in files, so that even if we exit the app and run it again, the data will remain the same.
  
- basic endpoints that are required
  - GET /todos -> get all the todos
  - GET /todos/:id -> retrive a specific todo by id
  - POST /todos -> add to the todos array 
  - PUT /todos/:id -> update a existing todo by id 
  - DELETE  /todos/:id -> delete and todo item by ID

- app.get is giving us back the empty array.

### todoServer 

- write all the endpoints as directed 
- add a findIndex method that gets the first index of the item and return the index of the given index.
- currently saving the todos in a global array and saving the responses.
- then can use the file to save the file. 

### storing in a file 

- storing our todos in a file rather than in memory.
- storing in a database is safer and is much more fault tolerant than storing in a file.
- using the fs module, to write asynchonrously to a file while we write.


### CORS 
- 