# Login and Auth

## login.js

- The purpose of the `login` component is to retrieve form data from the user and pass this to update the state of `context`
- We update the state that lies within `context` by first importing context by `import { LoginContext } from './context.js';` and using it in conjunction with `useContext`
- This allows us to utilize state and methods that live in the `context.js` file
- We also pull in the `isLoggedIn` state from the context. This allows us to control what we render on screen.
- In this instance, if `isLoggedIn` is true, app will render the 'Log Out' button
- If false, will render the form that the user will use to sign in along with a Submit button

## context.js

- In this file, we create context which is global state that only children of this component have access to.

### State

- `isLoggedIn` state is created, this state is important because it is used toward authorization and the rendering of certain items on the app
- If suppose the user is not logged in, means that `isLoggedIn` is false and the user will not be able to see sections of the application
- `user` state is used to store the user info that is retrieved from the API and is used toward auth

### validateToken

- `validateToken` is another layer of authentication. This method is used within the `login` method where a token is passed in as an argument. The purpose of `validateToken` is to validate the token and create a cookie. `validateToken` is also where access is either granted or denied

### logout

- Is a method applied to an onClick event. This method is imported from the form and applied to a button that when clicked, changed global context state to logout the user. The state that is changed are the `user` and `setIsLoggedIn`. This data affects what will be rendered on the app.

### can

- This method returns a boolean and verifies if a user is granted certain permission based on the `user` state.

### login

- As mentioned before, this method is imported into the login.js. This method fetches data from the form which is used toward an API request to retrieve user data.
- This is where we also invoke the `validateToken` method to validate the token

### useEffect

- The `useEffect` statement within this file checks to see if a user is logged in. To do this, it goes into the browser and looks for a `cookie` which contains a token. This token is then validated through the `validateToken` method as well. I made possible by utilizing the `react-cookies` library

### sharedThings

- Since this is context, `sharedThings` is a object that contains all of the piece of state and methods that we want to pass as global start for any of its children to use.

### Provider

```jsx
  return (
    <LoginContext.Provider value={sharedThings}>
      {props.children}
    </LoginContext.Provider>
  )
```

- in order for data to be used we have to remember what the return statement looks like. Data you want to pass as global state has to be passed through the `value` prop of the `Provider` element.

## auth.js

- This component first import context from the `context.js` and is used toward a condition that renders data or not
- This component is used as a wrapper and is given a 'capability' prop. This prop is used toward parts of auth which determines if a use has access to certain parts of the application
- This component is imported and used as a wrapper in different parts of the app

```jsx
// Within list.js
return (
    <>
      <Auth capability="read">
        {
          props.list.map(item => (
            <Card aria-label="list-item" key={item._id} style={{ width: '40em', marginBottom: '1em' }}>
              <Card.Header className="header-container">
                <Auth capability="update">
                  <span
                    className="pending"
                    onClick={() => props.handleComplete(item._id)}
                    style={{ ...completionStyles, backgroundColor: item.complete ? 'green' : 'red' }}>
                    {item.complete ? "Completed" : "Incomplete"}
                  </span>
                </Auth>
                <span> {item.assignee}</span>
                <Auth capability="delete">
                  <span aria-label={item} className="deleteItem" value={item.id} onClick={() => props.handleDelete(item._id)}> x</span>
                </Auth>
              </Card.Header>
              <ListGroup variant="flush">
                <ListGroup.Item>
                  <div>{item.text}</div>
                  <div className="difficulty">Difficulty: {item.difficulty}</div>
                </ListGroup.Item>
              </ListGroup>
            </Card>
          ))
        }
      </Auth>
    </>
  );

// Within form.js
return (
    <>
      <Auth capability="create">
        <form data-testid="formTest" onSubmit={handleSubmit}>
          <Card style={{ width: '18rem' }}>
            <Card.Body>
              <Card.Title>Add Item To Do Item</Card.Title>
              <Card.Text>To Do Item</Card.Text>
              <input
                data-testid="addItemTest"
                type="text"
                name="text"
                placeholder="Add To Do List Item"
                onChange={handleChange}
              />
              <Card.Text>Difficulty Rating</Card.Text>
              <input
                data-testid="difficultyTest"
                defaultValue="1"
                type="range"
                min="1"
                max="5"
                name="difficulty"
                onChange={handleChange} />
              <Card.Text>Assigned To</Card.Text>
              <input
                data-testid="assigneeTest"
                type="text"
                name="assignee"
                placeholder="Assigned To"
                onChange={handleChange} />
              <button>Add Item</button>
            </Card.Body>
          </Card>
        </form>
      </Auth>
    </>
  )
```

### canDoThing

- Checks to see if what value of is given through the `capability` prop which is compared to the capabilities that the user has access to

### okToRender

- Ultimate boolean that determines the rendering of data

```jsx
  return (
    <When condition={okToRender}>
      {props.children}
    </When>
  )
```