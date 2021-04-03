# event driven applications

## Events

### events.emit()

- triggers `.on()` event methods
- `.emit()` takes in 2 parameters
  1. the event that you want to fire off
  2. information that you want to pass to the `.on()` event method

### events.on()

- triggered by `.emit()` event methods
- `.emit()` takes in 2 parameters
  1. the event that you want the method to respond to
  2. a call back function that you want to run when the event is triggered.
    - this callback function always takes in a parameter `payload` that will use the data passed from the `.emit()`

### caps.js

- similar to a `server.js` the `caps.js` file contains all events from the other files that contain events.. if that makes sense

```javascript
require('./driver');
require('./vendor');
const events = require('./events.js');

events.emit('start')
```

### events.js

- global event pool
- this file instantiates the event packages ONCE
- this event pool is then exported to be used in the other files so that the events are all implemented within the same pool

```javascript
const Events = require('events');
const events = new Events();

module.exports = events;
```

## Testing

### Fake timers

- use fake timers if code that you are testing has some type of timer
- in this case.. i used `setInterval()` and `setTimeout()` within the functions that I performed tests on 

#### jest.useFakeTimers()

- `.useFakeTimers()` initiates a fake timer within a test

#### jest.useRealTimers()

- `jest.useRealTimers()` resets the timer

#### jest.advanceTimersByTime(1000)

- `jest.advanceTimersByTime(1000)` should be used after the function has been invoked
- this allows the time needed by the function order to retrieve the end result

```javascript
'use strict';

const driver = require('../driver.js');

describe('VENDOR TESTING', () => {
  let consoleSpy;
  let payload = {orderId: 111};

  beforeEach(() => {
    consoleSpy = jest.spyOn(console, 'log').mockImplementation();
    jest.useFakeTimers()
  });

  afterEach(() => {
    consoleSpy.mockRestore()
    jest.useRealTimers()
  })

  it('function "pickUpItem" properly logs some output', () => {
    driver.pickUpItem(payload)
    jest.advanceTimersByTime(1000)
    expect(consoleSpy).toHaveBeenCalled();
  })
  
  it('function "inTransit" properly logs some output', () => {
    driver.inTransit(payload)
    jest.advanceTimersByTime(5000)
    expect(consoleSpy).toHaveBeenCalled();
  })
})
```

## GENERAL

- The purpose of event driven app is to execute code when we need to. Code executes based on events which then trigger the actions ONLY WHEN NEEDED