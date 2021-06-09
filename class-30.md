# Hash Tables

- Hash tables provide a consistent way to search for items in a list with a speed of O(1);
- Hash tables hold unique values as a way to store and search for things.
  - Hash tables have the ability to store a key as well as quickly retrieve values.
- Hashing is a result of some algorithm which takes a string and converts it into a value that could be used for security or some other purpose.

## Parts to a Hash Table

- An array `this.map = new Array(size).fill();`
- A Linked List
- Nodes

`.hash(key)`
  - hashes the argument into a index which reflects an index of the hash table

`.set(key, value)`
  - a method that utilizes the hash function in order to add a value to the hash table

`.get(key)`
  - retrieves the value of the passed in argument

`.has(key)`
  - returns a boolean based on the argument that was passed in