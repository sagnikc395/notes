## Middlewares,Authentication , Global Catches and Zod

- decent stuff of hard backend stuff to understand.
- doctor is single threaded.
- 50% of backend stuff that we do.
- eg: Hospital(Covid) -> bull run

  - Before you reach to the doctor:
    - predo a lot of stuff , to decrease load in the main methods, picky checks to happen.
    - your aadhar/insurance info is taken. Only if we have insurance then we proceed.
    - Blood test is done, inly if no STD does user proceed.
    - BP is checked, only if BP is reasonable, then user proceeds.

- Equivalent code for this -> exposing a single route for now,
- simple function to simulate.

```js
const express = require("express");

const app = express();

app.get("/health-checkup", (req, res) => {
  res.send(`Your heart is healthy!`);
});
```

### Prechecks

- how to do the prechecks ? should we handle this at doctor's level ? or check them previously at reception level?
  i.e

  - Auth checks ? -> Does this user have funds to visit the doctor.
  - Ensure input by the user is valid (BP/ blood tests)

- To do this we do -> **Middlewares**

### Basic way to do validation:

```javascript
app.get("/health-checkup", function (req, res) {
  // slop way of doing health checkups here
  const kid = req.query.kid;
  const username = req.headers.username;
  const password = req.headers.password;

  if (username !== "sagnik" || password !== "pass") {
    res.status(403).json({
      msg: "Failed to Authenticate!",
    });
    return;
  }

  if (kid !== 1 || kid !== 2) {
    res.status(403).json({
      msg: "wrong inputs!",
    });
    return;
  }
  //valid kidneys
  res.json({ msg: `Your kidney is 🔥!` });
});
```

- not very repetable or abstracted approach, and does not support the DRY principle.

- ugly solution of create the new route and repeat the code.

### better way:

- slightly better solution: write the validation checks written in seperate functions and we call the functions for different types.
- slightly leaner validation logic.
- any change that we need in a validator, we can write the change in other places.

- but still a lot of code repetition.
- real optimal solution -> use middlewares

  - since we know that we need to do a series of prechecks, we move them some other place, and that other place is called middleware.

- in the methods for our express app, we are not constrained by one callback function, we can give a range of callback functions.
- actually three parameters to the callback function -> (req,res,next). next is a function in itself, which we call if we think things are fine.
- express lets us chain through prechecks.
- the last one is where we will not require next, rather send directly via res.

### Global Catches

- at the end of the all the methods, if we do:

````js

app.use((err,req,res,next) => {
  //can do something here
})```
````

- it will act as a global catch , handling all the errors.
- Global catches help us give the user a better error response.
- Error-handling middleware -> special type of middleware function in Express that has 4 arguments instead of 3. Express recognizes it as a error-handling middleware because of these 4 arguments.

### Zod.

- very common use case to do user validation on any http server.
- need to do multiple checks for the input and common fields need to be checked and do input validation checks.
- lots of growing concerns to address.
- lots of input validation libraries ike zod to validate the user input.
- to prevent for user to write ugly logic to clean the changes and use zod to do input validation the right way.
- for js based , it's just schema validation.

### Authentication

- As we can tell now, anyone can send requests to our backend.
- They can just go to postman and send a request.
- How do we ensure that this user has access to a certian resource ?

- Dumb Way to do auth -> ask user to send username and password in all requests as headers.

- Use crypto to seed and then add those changes.
