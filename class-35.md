# Graphs

- SO, out of all the data structures, I find graphs the most useful.

## Graph

- Utilizing a `new Map()` constructor, we create a graph

## addVertex(vertex)

- Set a value within the Map
- `this.adjacencyList.set(vertex, []);`

## addDirectedEdge(startVertex, endVertex, weight = 0)

- This works by retriving the empty array tied with a value
- Then we push an Edge to this list

## getNeighbors(vertex)

- Using the `.get()` method on the Map, retrieves the edges / neighbors of the vertex passed in as an argument

## getNodes()

- Using `.keys()` on a Map, will retrieve all the values of the Map object

## size()

- The a Map object has a `.size` property that returns the size of the Map object

## Reference

https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-35/resources/graphs.html