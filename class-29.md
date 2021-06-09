# LAB 29 - Routing

## App Component

- The 'APP' component acts as the overall parent component/wrapper of all the components
- This APP component will be the only component rendered by React
- All other are layered within the App component and are all children/decendents of App
- I used app to store all state used in my Application. I chose this direction because it only made sense to me that I any child would be able to utilize this state by passing state as a prop.
  - Although this works, I later learned that better architecture would be to have state in other components. This is better because not all components need access to all of the state, leading to cleaner code.
  - Having state only within child components does cause some minor workarounds.
    - Doing so, its important to note that you cannot pass state from CHILD to CHILD. Instead, The parent of the two siblings would have to acquire the state by using a fetch function, utilizing that information to create its own state within the parent function, and then sending newly created state within the parent function as a property to the other sibling.

### handleGo(e)

- This function does work based on the current state in which the user alters. Pressing 'Go', other state within the App are updated and used toward an axios called to request data from an API.
- The response from the API is taken apart where the state of the App is altered yet again.
- The updated state is then collected to make an object which will be added to a `searchHistory` that will be stringified and stored into a local storage.
- Changes of state will passed on to children component as props and will reflect what is displayed on the page
- I loved watching John's example. I loved that he did in depth walkthrough because it gave me a different perspective on how I will be building out the architecture on my next React App. I'm just glad that my app is working and functional.

### handleChange(e)

- This function is used on different areas of the `Form` component and instantly changes state within the App on `onChange` events.
- React syntax tell us that we need to 'spread' the state.
- Depending where this function is utilized, the `e.target.name` reflects the key of the state which is also correlates to the `name` attribute on the input tag that this function is placed on. `e.target.value` reflects what will be the value of the key and also correlates to the `value` attribute on the input tag.

```jsx
<input data-testid="radioTestGet" onChange={this.props.handleChange} type="radio" name="method" value="get" checked={this.props.method === 'get'}/>

this.state = {
  method: 'get'
}
```

### handleSearch(e)

- This function is placed on history buttons placed on the homepage.
- The purpose of this function is to change the state of the `urlInput` and `method` which when clicked will load values in so that previous searches are easily accessed

### handleRetrieve(e)

- This function is placed on history buttons placed on the history.
- The purpose of this function is to change the state of the `headers` and `results` which when clicked will instantly render previous responses that are recorded in local storage

### componentDidMonut()

- Happens everytime state is updated.
- Contains a code block that retrieves the data from local storage.

#### Local Storage Flow

- When the App starts, this hook retrieves the search history.
- State is updated after a request from an API has been successfully been made.
- Part of this change of state is that the search history has been updated.
- The updated search history is then strigified and saved into local storage.
- At this point, the app rerenders and this `componentDidMount()` function is ran again and updated the current state of searchHistory with the newly saved search history.

## Routes

- '/' Home Path
  - contains a form field and history searches

- '/history'
  - contains history searches

- '/help'
  - renders a tutorial on how to use the Application

## Header Component

- Renders an `H1` header tag

## Navbar Component

- Renders a list of items that act as a navbar.
- Clicking these links will render specific parts of the app.

## Form Component

- Renders a form.
- Methods from the App are passed in as props to the Form Component and are used to change state of the overall app.
- State is also displayed on certain parts of the form fields

## Content Component

- Takes in App's search history as props and is used to display all of the searches on the App.
- Clicking the button will run a method that is passed in as a prop

## Results Component

- Made as a function component
- Uses react-if to display API reponses
- Utilizes `react-json-view` to present data in an organized manner
- The props that are passed in are data that is extracted from a response from an API

## Help Component

- Static page that gives a walkthrough on how to use the RESTy Application