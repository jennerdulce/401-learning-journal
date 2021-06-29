# Redux

## How to use Redux

1. Make a store directory
2. Create the store

- index.js

```jsx
// Create the Store
import { createStore, combineReducers } from 'redux'
import { composeWithDevTools } from 'redux-devtools-extension'
import inventory from './inventory.js'

const reducers = combineReducers({ inventory })
const store = () => {
  return createStore(reducers, composeWithDevTools())
}

export default store();
```

3. Create state and reducer

- name.js

```jsx
// Initial State
const initialState = {
  products: [],
  inventory: [],
  currentSort: ''
}

// Reducer Function
export default function reducer(state = initialState, action) {

  const { type, payload } = action

  switch (type) {
    case 'CHANGE':
      let newList = state.products.filter((obj) => payload === obj.category)
      console.log("INVENTORY ===========", newList)
      return { ...state, inventory: newList, currentSort: payload }
    case 'RENDERLIST':
      console.log(payload)
      return { ...state, products: payload }
    default:
      return state
  }
}

// Action Creators
export const changeCategory = (category) => {
  return {
    type: 'CHANGE',
    payload: category
  }
}

export const updateList = (list) => {
  return {
    type: 'RENDERLIST',
    payload: list
  }
}
```

4. Wrap around app

- app.js

```jsx
import { Provider } from 'react-redux'

function App() {
  return (
    <ThemeContext>
      <Provider store={store}>
        <Header />
        <Categories />
        <CategoryBanner />
        <ItemCard />
        <Footer />
      </Provider>
    </ThemeContext>
  );
}
```

## Material UI

- To customize styling

```jsx
import React from 'react'
import { When } from 'react-if'
import { useSelector } from 'react-redux'
import { Typography, makeStyles } from '@material-ui/core';


const useStyles = makeStyles({
  root: {
    width: '100%'
  },
  header: {
    textAlign: 'center',
    marginTop: '10rem'
  },
  description: {
    textAlign: 'center',
    color: '#B8B8B8'
  }
});

function CategoryBanner() {
  const category = useSelector((state) => state.inventory.currentSort)
  const classes = useStyles()

  return (
    <When condition={category}>
      <div className={classes.root}>
        <Typography className={classes.header}variant="h3" gutterBottom>
          {category.toUpperCase()}
        </Typography>
        <Typography className={classes.description} variant="h6" gutterBottom>
          Description of Category Items
      </Typography>
      </div>
    </When>
  )
}

export default CategoryBanner

```

## Tips

- when you are within the reducer `state` refers to the initial state