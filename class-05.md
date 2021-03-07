## Linked Lists
- A type of data structure
- A linked list is a linear data structure where elements are linked using pointers
- 3 types: singular, doubly, circular
-[Linked List assignment](https://github.com/jennerdulce/data-structures-and-algorithms/tree/main/javascript/code-challenges/Data-Structures/linkedList)

## Big O Notation
- time complexity -> efficiency
- space complexity -> storage
- describes the # of operations an algorithm will make
- provides transparency into time and space without actually running the code!
  - "this is basically how efficient it is"

- bad example. dont do this
```javascript
for (let i = 0...){
  for(let j = 0...)
}
```

- basic main functions of a data structure:
  - `.find()`
  - `.remove()`
  - `.insert()`
- find the simplified version of worst case scenario

- O(1) -> storage -> consistent time (A++)
  - 1 : 1 thing
  - object look up
  - given an array index
  - property of index

- O(log, n) -> logrithmic time (A++)
  - binary search tree
  - divide and conquer algorithm
    - cut in half search

- O(n) -> linear time (A -)
  - loop