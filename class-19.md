# Component Based UI

## Terms

### State

- An instance of `React.Component` class that can be defined as an object of a set of observable properties that control the behavior of the component
- State of a component is an object that holds some info that may change over the lifetime of the component
- The state of a component is an observable object that holds some information and controls the behavior of the component. The difference between props and state is that props don’t change over time during the lifetime of a component. The state holds the data that can be changed over time and changes the component rendering as a result.

### Components

- User Definied Component: Component that a user creates
- Allows developers to split UI into independent, reusable pieces, and thin kabout each piece in isolation

#### Class Componenets

- Additional benefits class components offer by default are state and lifecycle. That is why class components are also known as “stateful” components. 

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

#### Function Componenets

- This function is a valid React component because it accepts a single “props” (which stands for properties) object argument with data and returns a React element. We call such components “function components” because they are literally JavaScript functions.

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

- Props: Inputs for components
- important task to pass information from component to component helped to build dynamic user interfaces
- read only: components should not change their inputs

## Code

- Refer to RESTy lab 26