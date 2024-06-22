# Graphs - Custom datatype

<img width="621" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/8c4363e9-0ed7-4396-a4a1-ba40a6e0bb06">

Types.
<img width="248" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/e2d35864-3e01-4ad4-9575-179b72e0aebb">

Directed Graph
<img width="619" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/5cdb83b9-7a10-450b-8264-1578f6fdc054">

Undirected Graph
<img width="608" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/e108d1e3-8e7f-4434-851b-0be880434475">

Few More types of Graph
<img width="582" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/9c58d67b-c166-4640-902c-3dd9c741ec8b">

# Usage
<img width="220" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/36f2175e-7e5e-4691-91ae-a39085e71951">


## Degrees in a Graph
No, of nodes atached to the current node

### Property
1. Total Degree  = 2 * no, of edges in the graph
   
### Indegree - No, of incoming edges in Directed Graph
### OutDegree edges - No, of outgoing edges in Directed Graph

### Edge Weight -  The weights assigned to each edge in the graph.

## Graph Representation

Adjacency matrix

<img width="599" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/d744d848-2cf4-42de-b054-23b13842fd1e">

<img width="591" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/877c1c3a-df4d-43c5-8928-2b7b9d66974d">



Adjacency List

<img width="622" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/a2afa6c0-08c0-46ea-91bf-3d12d46975c1">

<img width="563" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/fd83ccb5-a882-4c67-8c85-4c1425796a6a">



Adjacency Matrix VS List
<img width="611" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/c154a38b-1423-426d-a958-1e3a7c9b1ad1">



## Data Structure

```
Class Graph {
  constrcutor(){
    this.adjacencyList = [];
  }

  addvertex(vertext){ // TC O(1)
    if(!adjacencyList[vertex]){
      adjacencyList[vertex] = new Set();
    }
  }

  addEdge(vertex1,  vertex2){ // TC O(1)
    addVertex(vertex1);
    addVertex(vertex2);
    this.adjacencyList[vertex1].add(vertex2);
    this.adjacencyList[vertex2].add(vertex1);
  }

  display(){
    for(let vertex in this.adjacencyList){
       console.log(vertex, "->" + [... this.adjacencyList[vertex]]);
    }
  }

  hasEdge(vertex1, vertex2){
    return (this.adjacencyList[vertex1].has(vertex2) && this.adjacencyList[vertex2].has(vertex1));
  }

 removeEdge(vertex1, vertex2){ // TC O(1)
    this.adjacencyList[vertex1].delete(vertex2);
    this.adjacencyList[vertex2].delete(vertex1);
  }

  removeVertex(vertex){ /// TC deoendes upon No, of vertices
    if(!this.adjaccencyList[vertex]) return "Not Found";
  
    for(let adjVertex in this.adjacencyList[vertex]){
      this.removeEdge(vertex, adjVertex);
    }
  
    delete this.adjaccencyList[vertex];
  }

}

const graph = new Graph();
```


## Conneted Components

## Traversal Algorithm.

### DFS
<img width="437" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/9c235560-24a9-42d4-9049-9b6cac202d06">

 Requirements
 1. Set
 2. Stack

 ## Iterative Method.

```
TC -  V + e -  Vertex + Edges
function dfsIterative(startVertex) {
  let visited = new Set();
  let stack = [];

  stack.push(startVertex);

  while (stack.length) {
    let currentVertex = stack.pop();
    visited.add(currentVertex);

    for (let neighbour of this.adjacecentList[currentVertex]) {
      if (!visited.has(neighbour)) {
        stack.push(neighbour);
      }
    }
  }
}
```

## Recursive Solution

```
function dfsRecursive(startVertex) {
  let visited = new Set();
  dfs(startVertex, visited)
 
}


function dfs(vertex, visited){
  visited.add(vertex)
  
 for(let neighbour of adjacencyList[vertex]){
  if(!visited.has(neighbour)){
    dfs(neighbour, visited)
  }
 }
}
```

## BFS
<img width="598" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/e101391e-f9ac-4bde-bffd-9225d32bea40">

### Iterative Solution
```
function BFSIterative(startVertex){
  let visited = new Set();
  let queue = [];

  queue.push(startVertex);
  visited.add(startVertex);

  while (queue.length) {
    let currentVertex = queue.shift();

    for (let neighbour of this.adjacecentList[currentVertex]) {
      if (!visited.has(neighbour)) {
        queue.push(neighbour);
        visited.add(neighbour);
      }
    }
  }
}

```

### Recursive Solution.

```
function bfsRecursive(startVertex) {
  let visited = new Set();
  bfs([startVertex], visited);
}

function bfs(queue, visited) {
  if (queue.length === 0) {
      return;
  }

  let nextQueue = [];
  for (let vertex of queue) {
      if (!visited.has(vertex)) {
          visited.add(vertex);
          console.log(vertex); // You can push this to a result array if needed

          for (let neighbor of this.adjacencyList[vertex]) {
              if (!visited.has(neighbor)) {
                  nextQueue.push(neighbor);
              }
          }
      }
  }

  bfs(nextQueue, visited);
}

```



