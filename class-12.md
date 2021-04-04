# Socket.io

- Today I built small app that uses Socket.io! An incredible tool that uses sockets within a port that allows different apps to communicate in REAL TIME by using Events!

- Socket.io replaces the event pool
  - functions the same as events by using listeners and emitting events

## hub.js

```javascript
const PORT = process.env.PORT || 3000;
const io = require('socket.io')(PORT);

io.on('connection', (socket) => {
  // code block
  // global main connect
}
```

- create a namespace by importing `socket.io` and enter a port as a parameter
  - this establishes a connection
- create a namespace

```javascript
io.on('connection', (socket) => {
  // code block
  // global main connect
  socket.on('event', (payload) => {

  })
}
```

- use `socket.broadcast.emit()` to emit to all listeners within namespace

### Create another namespace

```javascript
let newNamespace = io.of('/secondaryNamespace')
newNamespace.on('connection', (socket) => {
    // code block
  // global main connect
})
```

## seprate.js

```javascript
const io = require('socket.io-client')
const host = 'http://localhost:3000'
const mainsocket = io.connect(host) // connects to socket
```


## Rooms

## caps.js

```javascript
const PORT = process.env.PORT || 3000;
const io = require('socket.io')(PORT); // main namespace
const house = io.of('/house') // creates new namespace

house.on('connection', (socket) => {
  socket.on('enter', (payload) => {
    socket.join(payload) // whoever file emits this listener, joins the channel they pass as an argument
    io.of('house').to('kitchen').emit('door', payload)
    // emits the 'door' event to clients that are connected to the 'house' namespace and are also in the 'kitchen' room
  }
}

```

## seprate.js

```javascript
const io = require('socket.io-client')
const host = 'http://localhost:3000'
const mainsocket = io.connect(host) // connects to socket
const housesocket = io.connect(host+'/house')
housesocket.emit('enter','kitchen')
```
