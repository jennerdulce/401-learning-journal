# Message Queue

## Parts to creating a message queue

### hub.js

- create a queue system
- make catchup listeners that activate when apps initially start
  - these listeners will work with a specific queue and will work with each item within the queue

```javascript
const queues = {
  vendorID: {
    flowers: new Queue('Flowers'),
    acme: new Queue('ACME Inc.')
  }
}

 socket.on('catchupQueue', (payload) => {
    queues.vendorID[payload].delievered.forEach(value => {
      // triggers delievered in vendor
      if (payload === 'flowers') {
        io.to('flower delievery').emit('delievered', value)
      } else if (payload === 'acme') {
        io.to('acme delievery').emit('delievered', value)
      }
    })
  })

  // flush pickup
  socket.on('pickupQueue', (payload) => {
    queues.vendorID[payload].pickup.forEach(value => {
      socket.emit('newPickup', value)
      console.log(`Catching up on ${value}`)
    })
  })
```

### vendor.js

- this file will emit a 'catchup' as soon as app boots up

```javascript
caps.emit('catchupQueue', 'flowers')
```


## Creating rooms/subscribing

- In my project, I chose to work within the 1 main namespace and had rooms to emit unique messages to the other apps

### hub.js

- the `.join()` method here is what actually assigns the subscription/joining of a room
- pay special attention to how to EMIT A MESSAGE using the actual socket.. `io.to('acme delievery').emit('delievered', payload)`

```javascript
io.on('connection', (socket) => {
  console.log(`${socket.id} HAS CONNECTED!`)
  // subscribes to 'delievered' 
  socket.on('join', (payload) => {
    // 'acme delievery'
    socket.join(payload)
    console.log(`User ${socket.id} has joined '${payload}'`)
  })

// to send to an app that joined a room
// this allows the emit event 'delievered' to be used dynamically
io.to('room name').emit('delievered', payload)
```

### vendor.js

- the app emits a `join` event on start up followed by the room that they want to join, this is then received at the listener where 'acme delievery' is used as an argument within the `.join()` event method
- the subscription has been made
- `.on('connect')` is a special kind of listener.. is listening for a `connect` event which is made when the client connects to the host `const caps = io.connect(host)`

```javascript
const caps = io.connect(host)

caps.on('connect', (socket) => {
  // subscribes to 'delievered'
  caps.emit('join', 'acme delievery')
  console.log(`joined 'acme delievered'`)
})
```

### driver.js

- works the same way as vendor

```javascript
caps.on('connect', (socket) => {
  // subscribes to 'pickup'
  caps.emit('join', 'pickup')
  console.log(`joined 'pickup'`)
})
```