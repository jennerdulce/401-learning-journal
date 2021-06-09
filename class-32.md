# Custom Hooks

## General

### Initial Render

```jsx
const [list, setList] = useState([])
const [{ data, loading, error }, refetch] = useAxios({
  url: 'https://api-js401.herokuapp.com/api/v1/todo', method: "GET"
});

useEffect(() => {
    if (data && data.results) {
      console.log('THIS IS DATA: ', data.results)
      setList(data.results)
    }
  }, [data]);
```

- These 2 code blocks are used to render intial data when the browser opens

### Toggling

```javascript
  const toggleComplete = async (id) => {
    // Selects single item
    let item = list.filter(i => i._id === id)[0] || {};

    if (item._id) {
      // Toggles the 'complete' property
      item.complete = !item.complete;
      // Recreates array of tasks and looks for the matching id to swap out that specific item
      let updateItems = list.map(listItem => listItem._id === item._id ? item : listItem);
      // Updates / rerenders the 'list' state
      // Send axios calls to actually make changes on the API
      let url = `https://api-js401.herokuapp.com/api/v1/todo/${id}`
      setList(updateItems)
      await axios.put(url, item)
        .then(function (response) {
          console.log(response);
        })
        .catch(function (error) {
          console.log(error);
        });
    }
  };
```

### Delete from API

```javascript
  const handleDelete = (id) => {
    // Send axios calls to actually delete on the API
    let url = `https://api-js401.herokuapp.com/api/v1/todo/${id}`
    axios.delete(url)
      .then(function (response) {
        console.log(response);
        refetch()
      })
      .catch(function (error) {
        console.log(error);
      });
  }
```

## Testing

```javascript
import MockAdapter from 'axios-mock-adapter'

let mock = new MockAdapter(axios)

const mockPostsData = [
  { _id: 1, complete: false, text: 'Clean the Kitchen', difficulty: 3, assignee: 'Person A' },
  { _id: 2, complete: false, text: 'Do the Laundry', difficulty: 2, assignee: 'Person A' },
  { _id: 3, complete: false, text: 'Walk the Dog', difficulty: 4, assignee: 'Person B' },
  { _id: 4, complete: true, text: 'Do Homework', difficulty: 3, assignee: 'Person C' },
  { _id: 5, complete: false, text: 'Take a Nap', difficulty: 1, assignee: 'Person B' }
];


describe("Todo Tests", () => {

  mock.onGet("https://api-js401.herokuapp.com/api/v1/todo").reply(200, {
    results: mockPostsData
  })

  it('Should initially render 5 task items', async () => {
    render(<App />)
    await waitFor(() => {
      const items = screen.getAllByLabelText('list-item');
      expect(items.length).toBe(5)
    })
  })
)}

```

- Its important to use `axios-mock-adapter` when testing
- Creates pseudo calls to the API
  - Renders the data that is returned by the mock API

## Creating Custom Hooks

```javascript
// EXPORTING
import {useState} from 'react';

const useForm = (callback) => {
  const [values, setValues] = useState({})

  function handleChange(e) {
    e.persist();
    let name = e.target.name;
    let value = e.target.value;
    setValues({...values, [name]: value});
  }

  function handleSubmit(e){
    e.preventDefault();
    callback(values)
  }

  // You return state and functions
  return [handleSubmit, handleChange, values]
}

export default useForm;


// IMPORTING INTO ANOTHER FILE

const [handleSubmit, handleChange, formData] = useForm(props.addItem)


 <form data-testid="formTest" onSubmit={handleSubmit}>
            <input
              data-testid="addItemTest"
              type="text"
              name="text"
              placeholder="Add To Do List Item"
              onChange={handleChange}
            />
            <input 
            data-testid="difficultyTest"
            defaultValue="1" 
            type="range" 
            min="1" 
            max="5" 
            name="difficulty" 
            onChange={handleChange} />
            <input 
            data-testid="assigneeTest"
            type="text" 
            name="assignee" 
            placeholder="Assigned To" 
            onChange={handleChange} />
            <button>Add Item</button>
        </Card>
      </form>

```
