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

### Weighted Edge Graphs.

```
class GraphEdge {
  this.source;
  this.destination;
  this.weight;

  GraphEdge(source, destination, weight){
    this.source = source;
    this.destination = destination;
    this.weight = weight;
  }

  this.getSource = function () { return this.source };
  this.getDesitnation = function () { return this.destination };
  this.getWeight = function () { return this.weight };
}
```

<img width="632" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/49d674da-28de-468d-8e1e-bb9939599166">

### Minimum Spanning Tree.
<img width="603" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/c2b985bf-1b1d-4aa5-acd6-a2e5ae3ea22f">

A Spanning Tree is a Sub graph where all the entire graph is connected, even after removing all the poossible redundant edges in the graph.

Eg Spanning tree
<img width="444" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/482dd153-89ca-4279-b0e7-bbcac0cfdcfd">

## Minimum Spanning Tree
The Spanning tree applied over a weighted graph to obtain a minimum weighted graph.

#### Real life Examples
1. Transportation
2. Power Grid
3. Water Supply
4. CDN's
 

## Prim's Algorithm
Used to derive a Minimum spanning tree.

```
class MinHeap {
    constructor() {
        this.heap = [];
    }

    insert(key, value) {
        this.heap.push({ key, value });
        this.bubbleUp();
    }

    bubbleUp() {
        let index = this.heap.length - 1;
        while (index > 0) {
            let parentIndex = Math.floor((index - 1) / 2);
            if (this.heap[parentIndex].value <= this.heap[index].value) break;
            [this.heap[parentIndex], this.heap[index]] = [this.heap[index], this.heap[parentIndex]];
            index = parentIndex;
        }
    }

    extractMin() {
        const min = this.heap[0];
        const end = this.heap.pop();
        if (this.heap.length > 0) {
            this.heap[0] = end;
            this.sinkDown(0);
        }
        return min;
    }

    sinkDown(index) {
        const length = this.heap.length;
        const element = this.heap[index];
        while (true) {
            let leftChildIndex = 2 * index + 1;
            let rightChildIndex = 2 * index + 2;
            let leftChild, rightChild;
            let swap = null;

            if (leftChildIndex < length) {
                leftChild = this.heap[leftChildIndex];
                if (leftChild.value < element.value) {
                    swap = leftChildIndex;
                }
            }
            if (rightChildIndex < length) {
                rightChild = this.heap[rightChildIndex];
                if (
                    (swap === null && rightChild.value < element.value) ||
                    (swap !== null && rightChild.value < leftChild.value)
                ) {
                    swap = rightChildIndex;
                }
            }
            if (swap === null) break;
            [this.heap[index], this.heap[swap]] = [this.heap[swap], this.heap[index]];
            index = swap;
        }
    }

    isEmpty() {
        return this.heap.length === 0;
    }
}

class Graph {
    constructor() {
        this.adjacencyList = {};
    }

    addVertex(vertex) {
        if (!this.adjacencyList[vertex]) {
            this.adjacencyList[vertex] = [];
        }
    }

    addEdge(vertex1, vertex2, weight) {
        this.adjacencyList[vertex1].push({ node: vertex2, weight });
        this.adjacencyList[vertex2].push({ node: vertex1, weight });
    }

    prim(startVertex) {
        const heap = new MinHeap();
        const result = [];
        const visited = new Set();
        const edges = {};

        heap.insert(startVertex, 0);
        edges[startVertex] = null;

        while (!heap.isEmpty()) {
            let { key: currentVertex, value: currentWeight } = heap.extractMin();

            if (visited.has(currentVertex)) continue;
            visited.add(currentVertex);

            if (edges[currentVertex]) {
                result.push(edges[currentVertex]);
            }

            this.adjacencyList[currentVertex].forEach(neighbor => {
                if (!visited.has(neighbor.node)) {
                    heap.insert(neighbor.node, neighbor.weight);
                    edges[neighbor.node] = { vertex: currentVertex, node: neighbor.node, weight: neighbor.weight };
                }
            });
        }

        return result;
    }
}

// Example Usage:
const graph = new Graph();
graph.addVertex("A");
graph.addVertex("B");
graph.addVertex("C");
graph.addVertex("D");
graph.addVertex("E");
graph.addVertex("F");

graph.addEdge("A", "B", 2);
graph.addEdge("A", "C", 3);
graph.addEdge("B", "D", 3);
graph.addEdge("C", "E", 5);
graph.addEdge("D", "E", 1);
graph.addEdge("D", "F", 4);
graph.addEdge("E", "F", 2);

const mst = graph.prim("A");
console.log(mst);

```

f## Kruskal's Algorithm.

Algorithm
<img width="563" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/3f848861-2462-404b-b60d-415cc3823118">

```
class DisjointSet {
    constructor() {
        this.parent = {};
    }

    // Create a new set with a single element
    makeSet(vertex) {
        this.parent[vertex] = vertex;
    }

    // Find the root of the set in which the element is
    find(vertex) {
        if (this.parent[vertex] !== vertex) {
            this.parent[vertex] = this.find(this.parent[vertex]); // Path compression
        }
        return this.parent[vertex];
    }

    // Union two sets
    union(vertex1, vertex2) {
        let root1 = this.find(vertex1);
        let root2 = this.find(vertex2);

        if (root1 !== root2) {
            this.parent[root2] = root1; // Simple union
        }
    }
}

class Graph {
    constructor() {
        this.edges = [];
        this.vertices = new Set();
    }

    // Add a vertex to the graph
    addVertex(vertex) {
        this.vertices.add(vertex);
    }

    // Add an edge to the graph
    addEdge(vertex1, vertex2, weight) {
        this.edges.push({ vertex1, vertex2, weight });
    }

    // Kruskal's algorithm to find MST
    kruskal() {
        const disjointSet = new DisjointSet();
        const mst = [];

        // Initialize the disjoint sets
        this.vertices.forEach(vertex => disjointSet.makeSet(vertex));

        // Sort edges by their weight
        this.edges.sort((a, b) => a.weight - b.weight);

        // Process each edge
        for (let edge of this.edges) {
            const { vertex1, vertex2, weight } = edge;

            // If adding this edge doesn't form a cycle
            if (disjointSet.find(vertex1) !== disjointSet.find(vertex2)) {
                disjointSet.union(vertex1, vertex2); // Union the sets
                mst.push(edge); // Add edge to MST
            }
        }

        return mst;
    }
}

```


## Dijikstra's Algorithm

Appllied to find the shortest path when given a graph

Needs
1. A Priority Queue
2. A Map or Object

```
class PriorityQueue {
    constructor() {
        this.values = [];
    }

    enqueue(value, priority) {
        this.values.push({ value, priority });
        this.sort();
    }

    dequeue() {
        return this.values.shift();
    }

    sort() {
        this.values.sort((a, b) => a.priority - b.priority);
    }

    isEmpty() {
        return this.values.length === 0;
    }
}

class Graph {
    constructor() {
        this.adjacencyList = {};
    }

    addVertex(vertex) {
        if (!this.adjacencyList[vertex]) {
            this.adjacencyList[vertex] = [];
        }
    }

    addEdge(vertex1, vertex2, weight) {
        this.adjacencyList[vertex1].push({ node: vertex2, weight });
        this.adjacencyList[vertex2].push({ node: vertex1, weight }); // If the graph is undirected
    }

    dijkstra(start) {
        const distances = {};
        const priorityQueue = new PriorityQueue();
        const previous = {};
        const path = []; // To store the shortest path
        let smallest;

        // Initialize distances, priorityQueue and previous
        for (let vertex in this.adjacencyList) {
            if (vertex === start) {
                distances[vertex] = 0;
                priorityQueue.enqueue(vertex, 0);
            } else {
                distances[vertex] = Infinity;
                priorityQueue.enqueue(vertex, Infinity);
            }
            previous[vertex] = null;
        }

        while (!priorityQueue.isEmpty()) {
            smallest = priorityQueue.dequeue().value;

            if (smallest === start) {
                // We are looking for the shortest path from start to all vertices
                for (let neighbor of this.adjacencyList[smallest]) {
                    let candidate = distances[smallest] + neighbor.weight;
                    let nextNeighbor = neighbor.node;
                    if (candidate < distances[nextNeighbor]) {
                        // Updating new smallest distance to neighbor
                        distances[nextNeighbor] = candidate;
                        // Updating the previous vertex to the neighbor
                        previous[nextNeighbor] = smallest;
                        // Enqueue in priority queue with new priority
                        priorityQueue.enqueue(nextNeighbor, candidate);
                    }
                }
            }
        }

        return { distances, previous };
    }

    findShortestPath(start, end) {
        const { distances, previous } = this.dijkstra(start);
        const path = [];
        let current = end;

        while (current) {
            path.push(current);
            current = previous[current];
        }

        return path.reverse(); // Return reversed path
    }
}

// Example Usage:
const graph = new Graph();
graph.addVertex("A");
graph.addVertex("B");
graph.addVertex("C");
graph.addVertex("D");
graph.addVertex("E");
graph.addVertex("F");

graph.addEdge("A", "B", 4);
graph.addEdge("A", "C", 2);
graph.addEdge("B", "E", 3);
graph.addEdge("C", "D", 2);
graph.addEdge("C", "F", 4);
graph.addEdge("D", "E", 3);
graph.addEdge("D", "F", 1);
graph.addEdge("E", "F", 1);

const shortestPath = graph.findShortestPath("A", "E");
console.log("Shortest Path from A to E:", shortestPath);

const distances = graph.dijkstra("A").distances;
console.log("Shortest distances from A:", distances);

```

