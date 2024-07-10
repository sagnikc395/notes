- writing scripts, migration issues and no good DX improvement and types for the developer and not provide any good improvement.
- ORMs came into the picture.
- Give basic functions that is provided to us.
- ORM:
	- Data Model
	- Automated Migrations 
	- Type Safety 
	- Auto Completion
- Layer in the middle between database, and its syntax is same and can provide an abstraction over a particular database.
- Other ORMs:
	- drizzle
	- sequelize
	- ..
- Libraries Provided by Prisma:
	- Prisma Client:
		- auto gen and type safe query builder for Node and TS
	- Prisma Migrate:
		- migration tool to easily evolve our database schema from prototyping to production
	- Prisma Studio:
		- GUI to view and edit data in our database.
- Automated Migrations:
	- DB Changes often, we add more columns, add new tables , we need to have MIGRATIONS to keep syncing DB state.
	- Pre ORM days - manually update the prod DB, dev DB.
		- ssh into the AWS Instance, create the query and run the migrations.
	- There was no log of the changes made to the DB.
- Prisma used a lot in the industry and used by cal.com and dub.sh.
- Running migrations and creating tables , Prisma needs access to a database and also needs to create temporary database on it to manage the migrations.

### setup prisma (refer the official docs):
- create typescript project and install prisma, typescript, @types/node as dev dependencies.
- setup ts config with tsc --init 
- init prisma in our project:
	- npx prisma init --datasource=provider postgresql
	- creates a file in prisma/schema.prisma
- dont commit secret to Github, add .env file to gitignore
- Model your data in the Prisma Schema:
	- a single source of truth of our schema 
	- only once we have defined our schema we can put our data and connect to the db.
	- the migrations and the dx experience is provided by prisma itself.

### Prisma Constructs:
- @id @default(autoincrement())
- @unqiue
- @default(false)
- @relation(fields:\[authorId],references:\[id])
- Eg:
```prisma
	model User{
	id Int @id @default(autoincrement()) -> id is integer type, with a default value and it increments automatically
	email String @unqiue ->  email should be a string and should be uniuqe type
	name String? ->  name is optional type
	posts Post[] -> for a user, posts array for the user.
	}
```
### relate data together:
- todos are related to users. every todo will have a user here and a foreign key.
- making a database construct strong -> no orphan todo present.
- same as can't delete user with multiple todos.
- Using foreign keys in prisma
```prisma 
model Post {
	id Int @id @default(autoincrement())
	title String 
	content String?
	published Boolean @default(false)
	author User @relation(fields :[authorId],references:[id])
	authorId Int
}
```
- the authorId is a foreign key for the Post table.
- Author is never stored in Post database, high level abstraction and are related conceptually and can use them using foreign keys and constraints.

### run a migration :
- run a migration with prisma/migrate library.
- npx prisma migrate dev --name init
- whenever prisma creates migrations , needs access to hidden table to run these migrations.
- This will create a new folder under migrations folder called migrations which will have the generated sql files.
- \_prisma_migrations is the database is what Prisma looks for and has a track of what all migrations are present here and what all migrations need to be run.


### adding data:
- create a create-data.ts in src directory , and import the prismaClient dynamically generated for our codebase.
- add the query to insert into the database entries
- run the build and then run node dist/crete-data.js to make the changes and see 
### to visualize:
- use npx prisma studio to view the tables and the entries.


### debug:
- add log info and query in our prisma client to give log queries under the hood for our prisma queries to give underlying query info.
-  ![[Screenshot 2024-04-02 at 7.22.19 AM.png]] 
- does a transaction, send these queries as a single query.

### get data:
- find all users using findMany().
- ![[Screenshot 2024-04-02 at 7.46.46 AM.png]]'
- find specific thing using findMany , using a where clause.
- to find a unique thing, use findUnique.

### update data:
- update using await prisma.users.update and pass the row id with the field that we want to update.
- ![[Screenshot 2024-04-02 at 8.05.57 AM.png]]


### delete data:
- same as update data.



### delete on cascade:
- delete all the post for a user.
- ![[Screenshot 2024-04-02 at 8.09.24 AM.png]]
- can go more and more deeper and nest it to delete it.
- can also add another update and do deleteMany to delete another query.

### filtering and sorting:
- ![[Screenshot 2024-04-02 at 8.12.44 AM.png]]
- findMany and then add other conditions as required.

### pagination and offset:
- min query return using limit and to limit the number of response.
- offset: need users after this number of offset.
```sql
select * from question offset 0 limit 1;
```
- take and skip properties in Prisma.
- ![[Screenshot 2024-04-02 at 8.22.18 AM.png]]

