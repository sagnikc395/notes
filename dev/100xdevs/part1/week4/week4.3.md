## Databases and MongoDB Deep Dive:

- DB -> a place where the data is stored persistently.
- Browser -> Express -> Database.
- Examples of data stroed in databases:
  - For linkedin for example:
    - User data
    - Users Posts
    - Users connection relationships
    - Messages
- Database is the thing that always remain the same -> they are persistent, servers are transient.
- there is not a single server where dbs are connected is stored, the data almost always stays up forever. We mostly keep the data together in a single place.

### why dont we allow the users to hit the database layer directly ? why do we have the HTTP layer in the middle ?

- what extra does the HTTP server provide exactly ?
- Reason:
  - Databases were created using protocols that browsers don't understand.
  - Databases dont have granular access as a first class citizen. Very hard to do user specific access in them.
  - There are some databases (firebase) that gets rid of the http server and tries their best to provide granular access.
- Express does the auth check and also to restrict access, and express server will restrict the query for the given user.

- Database usually allow access to 4 primitives:
  - Create data
  - Read data
  - Update data
  - Delete data
- These operations are popularly known as CRUD operations.
- Currently we will use the mongoose library to connect to a database, later shift to an ORM(Prisma) which is like the industry standard way of doing this.

### Mongoose:

- In Mongoose, we first have to define the schema.
- This sounds counterintuitive since mongodb is NoSQL/Schemaless ?

  - That is true, but mongoose makes us define schema for things like autocompletions/ validating data before it goes in the DB to make sure we are doign things right.
  - Schemaless DBs can be very dangerous, using schemas in mongo makes it slightly less dangerous.

- TODO!
