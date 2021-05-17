# Props and State

## Terms

### State

- An instance of `React.Component` class that can be defined as an object of a set of observable properties that control the behavior of the component
- State of a component is an object that holds some info that may change over the lifetime of the component
- The state of a component is an observable object that holds some information and controls the behavior of the component. The difference between props and state is that props don’t change over time during the lifetime of a component. The state holds the data that can be changed over time and changes the component rendering as a result.

### Props

- React is a component-based library which divides the UI into little reusable pieces. In some cases, those components need to communicate (send data to each other) and the way to pass data between components is by using props.
- “Props” is a special keyword in React, which stands for properties and is being used for passing data from one component to another.
- But the important part here is that data with props are being passed in a uni-directional flow. (one way from parent to child)
- Furthermore, props data is read-only, which means that data coming from the parent should not be changed by child components.

## Code

- Refer to RESTy lab 27
