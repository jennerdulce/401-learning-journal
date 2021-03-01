## Key Ideas

### RESTful / CRUD and Express
- What is REST?
  - representational state transfer
  - there is no state when making a request over the internet
  - has no knowledge before or after
  - we CREATE STATE with using a REST verb/action
    - `.get() .put() .post() .delete()`
    - these are consideres REST methods
- make requests are stateless.. so since we have a stateless protocol.. we are representing a request with a stateful action by using a REST verb/action to transfer the data.
- representing actions of state in a pseudo way

- The key is to build with RESTful methods in a server that then handles request and communicates with the database with CRUD actions
- REST maps to CRUD; they work with each other
- REST handles internet
- CRUD handles databases
- It is often that when you want to get something from the internet, has to retrieve information through a database..
- the back-end uses a RESTful method on the request which is transcribed to a CRUD action.
- the CRUD action is what actually retrieves the information from the database, and then return the data back to the server, then to the client.

- R: POST -> C: Create
- E: GET -> R: Read
- S: PUT -> U: Update
- T: DELETE -> D: Delete


### in-memory DB
- created an in-memory database utilizing an array within a class
- in-memory stores memory as long as server is running.
- we made this to visualize how databases work
- in-memory data resets when the server is turned off

- Overview
1. client -> server
2. server captures information from client requests
3. uses this information to do some sort of CRUD action on the database
4. database -> server -> client

- Process
1. build routes that will talk to these methods
2. methods then talk to db property that will then: create, read, update, or delete from the database

- adding or creating something, respond with:
  - 'added'
  - return information that you just added

### class
- provides us with structure and readbility

### route modules
- RESOURCE DRIVEN ROUTING
- we are just modularizing routes.. dont panic..

- setup:
  - require express
  - import model of database
  - set a variable to instantiate `express.Router()`
  set a variable to instantiate `new Database()`
  - export the routes
  - use the variable router in conjunction with REST method.
  - main server then `app.use(routeFilePath)` to allow the use of the route on the server.

- `express.Router()
  - gives this custom ability to use:
    - `app.get() -> router.get()`


- Process:
1. REST
  - `router.get('/things', getThing)`
2. CRUD
  - `let all = items.get()`
3. Send back
  - `res.status(200).json(all)`

### general
- After modles and models have been made `module.exports`
- import into `server.js`;
- "REST ROUTES map to CRUD Methods"
  - live in server through the use of importing modules