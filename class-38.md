# Asynchronous actions

## New

### Middleware / Thunk

- The main importance of thunk / middleware is to handle asynchronous calls effectively and is a part of overall architecture of the application

```jsx
// middleware file
// Thunk
const thunk = store => next => action =>
  typeof action === 'function'
     ? action(store.dispatch, store.getState)
     : next(action);

export default thunk;

// Logger
const logger = store => next => action => {
  // Do work in here
  console.log('__ACTION__ =====> ', action)
  try {
    // Does work and then passes the action to the next middleware and eventually the reducer
    const result = next(action)
    console.log('__STATE__', store.getState())
    return result;
  } catch (e) {
    // Adding a property called action to the Error object
    e.action = action

    // Refers to 
    return e;
  }
}
```

- First, make the middleware that you want to use
- Middleware returns a function also known as a Singleton
- Allows access to the store, much like the request object from express middleware.
- You return next which brings you to the next middleware and eventual dispatch

```jsx
// index/store file
// Import Middleware
import { createStore, combineReducers, applyMiddleware } from 'redux'
import { composeWithDevTools } from 'redux-devtools-extension'
import inventory from './inventory.js'
import cart from './cart.js'

const reducers = combineReducers({ inventory, cart })
const store = () => {
  // Also apply Middleware
  return createStore(reducers, composeWithDevTools(applyMiddleware(loggerMiddleware, thunk)))
}
```

- You import a new midethod called `applyMiddleware` from the redux library
- You insert the middleware like so

```jsx
// reducer file
export const updateList = () => async dispatch => {
  axios.get('https://storefront-db.herokuapp.com/api/v1/electronics')
    .then(res => {
      axios.get('https://storefront-db.herokuapp.com/api/v1/food')
        .then(resTwo => {
          dispatch(actualUpdateList([...res.data, ...resTwo.data]))
        })
    })
}

function actualUpdateList(data) {
  return {
    type: 'RENDERLIST',
    payload: data
  }
}
```

- Action creators look a little different.
- We export a function that is modified to handle a asynchronous call
- This function is dispatched through middleware where work is done
- The last thing that happens is the dispatch which goes through middleware AGAIN with the action object to be used by the reducer

```jsx
// component file
async function getData(payload) {
  dispatch(updateList())
}

useEffect(() => {
  getData()
}, [])
```

- Within a component, we import the function

## Old

```jsx
// reducer file
export const updateList = (list) => {
  return {
    type: 'RENDERLIST',
    payload: list
  }
}
```

- This is still okay, if you do not need to handle an asynchronous call. You can continue to write action creators like so

```jsx
// index/store file
import inventory from './inventory.js'
import cart from './cart.js'

const reducers = combineReducers({ inventory, cart })
const store = () => {
  return createStore(reducers, composeWithDevTools())
}
```

- There is no usage of middleware within this example

```jsx
// component file
async function fetch() {
  axios.get('https://storefront-db.herokuapp.com/api/v1/electronics')
    .then(res => {
      axios.get('https://storefront-db.herokuapp.com/api/v1/food')
        .then(resTwo => {
          dispatch(updateList([...res.data, ...resTwo.data]))
        })
    })
}

useEffect(() => {
  fetch()
}, [])
```

- In this example, the fetching of data happens within a component of the application rather than from the reducer.
- This just looks weird and is not the proper way to make an asynchronus call

## General Tips

- Be sure to check what state you are changing that reflects what state you are displaying!
- I was having trouble figuring out why state was not changing on a component
- I have 2 arrays that I am utilizing `products = []` and `inventory = []`
- Products holds ALL of the items
- Inventory holds the items of the selected category
- At the time I was only reiterating the products state.
- While doing so, my state was not changing because I was displaying the Inventory state

### Testing

- I am unsure the best way to tackle testing. I want to get better at it but I hit a huge block where I cannot find resources and am unsuccessful with the help of multiple TAs.
- I want to dive deep with a person who is good at testing so that I may develop their perspective