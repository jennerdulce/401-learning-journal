## Tips

- You can make components dynamic by passing in a prop with the using the SAME NAME that you used to pass in a prop to the component that was utilized in a different area
- Always see if you can find a React package to accomplish what you have in mind.
- You cannot pass state from child to child
- Child -> Parent -> Sibling

- Retrieve state from child components by creating a function from the parent, use this info to make state within the parent component. Pass state from parent component and pass as a prop to the child's sibling

```jsx
PARENT

state = {
  method: '',
  url: ''
}

fetch = (data) => {
 let method = data.method
  let url = data.url
}

<ChildComponent fetch={this.fetch}/>
<ChildComponent2 />



CHILDCOMPONENT

this.state = {
  method: '',
  url: ''
}

handleClick = (e) => {
  e.preventDefault()
  let data = this.state
  this.props.fetch(data)
}

<button onClick={this.handleClick}> 
</button>

```

### Local Storage

- Save Local Storage within axios calls since you have access to the response of the call
- Retrieve local storage on `componentDidMount()`

