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