# Context API

## Pagination


```jsx
// Put into App
  const [currentPage, setCurrentPage] = useState(1)
  const [postsPerPage, setPostsPerPage] = useState(3)

  const indexOfLastPost = currentPage * postsPerPage;
  const indexOfFirstPost = indexOfLastPost - postsPerPage;
  const currentList = list.slice(indexOfFirstPost, indexOfLastPost);

// Import into App
import Pagination from '../pagination/pagination.js'
<Pagination
postsPerPage={postsPerPage}
totalPosts={list.length}
paginate={paginate}
currentPage={currentPage}
/>
```

```jsx
// Create pagination component
const { Pagination } = require("react-bootstrap");

const createPagination = ({ postsPerPage, totalPosts, paginate, currentPage }) => {
  const pageNumbers = [];

  for (let number = 1; number <= Math.ceil(totalPosts / postsPerPage); number++) {
    pageNumbers.push(
      <Pagination.Item 
      onClick={() =>paginate(number)}key={number} 
      active={number === currentPage} 
      activeLabel="">
        {number}
      </Pagination.Item>
    )
  }

  return (
    <>
      <Pagination>{pageNumbers}</Pagination>
    </>
  )
}

export default createPagination;
```

- Utilizing react-bootstrap to create the buttons
- It is used in conjunction with logic in this video
- https://www.youtube.com/watch?v=IYCa1F-OWmk
- The logic works with how many items are returned from the API. Will create the calculate how many pages based on how many items are to be displayed on the page.


## Sorting

```jsx
let { sort, setSort } = useContext(SortContext);

  useEffect(() => {
    switch (sort) {
      case 'all':
        setList(data.results)
        break;
      case 'completed':
        let completedList = data.results.filter(value => value.complete)
        setList(completedList)
        break;
      case 'incomplete':
        let incompleteList = data.results.filter(value => value.complete === false)
        setList(incompleteList)
        break;
      case 'ascending':
        let ascending = data.results.sort(function (a, b) {
          return b.difficulty - a.difficulty;
        });
        setList(ascending)
        break;
      case 'descending':
        let descending = data.results.sort(function (a, b) {
          return a.difficulty - b.difficulty;
        })
        setList(descending)
        break;
      default:
      //
    }
  }, [sort, list])

<DropdownButton id="dropdown-basic-button" title="Sort">
<Dropdown.Item onClick={() => setSort('all')} >All</Dropdown.Item>
<Dropdown.Item onClick={() => setSort('completed')} >Completed</Dropdown.Item>
<Dropdown.Item onClick={() => setSort('incomplete')}>Incomplete</Dropdown.Item>
<Dropdown.Item onClick={() => setSort('ascending')}>Difficulty (ascending)</Dropdown.Item>
<Dropdown.Item onClick={() => setSort('descending')}>Difficulty (descending)</Dropdown.Item>
</DropdownButton>

  function App() {
    const [sort, setSort] = useState("")
    const providerSort = useMemo(() => ({sort, setSort}), [sort, setSort])
    return (
      <>
        <SortContext.Provider value={providerSort}>
          <ToDo />
        </SortContext.Provider>
      </>
    );
  }

// Is made to act as a wrapper
import { createContext } from 'react';

export const SortContext = createContext(null)
```
