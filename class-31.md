# Hooks API

## Functional Components

- State is handled differently when using a functional component

```jsx
function SomeComponent(props){

  // Method for handling state
  const [list, setList] = useState([])
  const [id, setId] = useState(0)

  // How you handle methods
  // Assign them to a variable
  const addItem = (item) => {
    setId(id + 1)
    const newString = 'Hello';
    setList([...list, newString])
  }

    return (
    <>
    // bring in props like this
    <h3>{props.title}</h3>
    </>
  )
}

export default ToDo

```

## react-bootstrap

### How to use

- `import { Navbar, Container, Row, Col } from 'react-bootstrap';`
- `import 'bootstrap/dist/css/bootstrap.min.css';`
- Reference react-bootcamp for examples!

## TIPS

- You can add classes on react-bootstrap elements
- Be sure to use ternery operations for boolean statements
- Add some inline styling for simple boolean statements