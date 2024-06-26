# Graph Problems

## Easy

T.C = O(1) 
S.T = O(1)
1.  1791 Find Center of Star Graph

```
/**
 * @param {number[][]} edges
 * @return {number}
 */
var findCenter = function(edges) {
    let [p1, p2] = edges[0];
    let [p3, p4] = edges[1];

    return p1 == p3 || p1 == p4 ? p1 : p2;
};
```

## BFS of Directed Graph
https://practice.geeksforgeeks.org/problems/bfs-traversal-of-graph/1

TC -  O(V + E)
SC - O(V)

```
class Solution {
    // Function to return Breadth First Traversal of given graph.
    bfsOfGraph(V, adj) {
        // code here
        // need to use queue in this
        let q = new Array();
        let ans = new Array();
        let visited = new Set();
        this.bfs('0', q, adj, ans, visited)
        return ans;
    }
    bfs(v, q, adj, ans, visited){
        q.push(v);
        visited.add(v);
        while(q.length > 0){
            v = q.shift();
            ans.push(v);
            for(let i=0; i<adj[v].length; i++){
                if(!(visited.has(adj[v][i]))){
                    q.push(adj[v][i]);
                    visited.add(adj[v][i]);
                } 
            }
        }
    }
}
```

### Given an integer n representing number of vertices. Find out how many undirected graphs (not necessarily connected) can be constructed out of a given n number of vertices.

https://www.geeksforgeeks.org/problems/graph-and-vertices/1

TC and SC -  O(1)
```
//User function Template for javascript
/**
 * @param {number} n
 * @returns {number}
*/

class Solution
{
    //Function to count the number of digits in a number.
    count(n)
    {
        return Math.pow(2, (n * (n - 1) / 2));
    }
}
```
### Print the Adjacency List

TC - O(E) - E is Edges
SC - O(N) -  N no, of Nodes
```
// User function Template for javascript
class Solution {
    printGraph(V, edges) {
       // Initialize an empty adjacency list with V vertices.
        const res = Array.from({ length: V }, () => []);
    
        // Iterate through each edge and add it to the adjacency list.
        edges.forEach(edge => {
            const [u, v] = edge;
            res[u].push(v);
            res[v].push(u); // For undirected graphs, add both directions.
        });
    
        return res;
    }
}
```

### 

DFS Implementation
```
class Solution {
    // Function to return a list containing the DFS traversal of the graph.
    dfsOfGraph(V, adj) {
        let visited = new Array(V).fill(false);
        let stack = [];
        let ans = [];
        
        // Helper function to perform DFS from a given vertex
        const dfs = (vertex) => {
            stack.push(vertex);
            
            while (stack.length > 0) {
                let v = stack.pop();
                
                if (!visited[v]) {
                    visited[v] = true;
                    ans.push(v);
                    
                    // Push all adjacent vertices to the stack
                    // Important to add in reverse order to maintain traversal order
                    for (let i = adj[v].length - 1; i >= 0; i--) {
                        if (!visited[adj[v][i]]) {
                            stack.push(adj[v][i]);
                        }
                    }
                }
            }
        };
        
        // Start DFS from each vertex to handle disconnected graphs
        for (let i = 0; i < V; i++) {
            if (!visited[i]) {
                dfs(i);
            }
        }
        
        return ans;
    }
}

```

***
***
***


## Medium

### 207. Course Schedule

TC - O(V + E)
SC O(V)
```
/**
 * @param {number} numCourses
 * @param {number[][]} prerequisites
 * @return {boolean}
 */
var canFinish = function (numCourses, prerequisites) {
    const indegree = new Array(numCourses).fill(0);
    const queue = [];
    for (const [course, prereq] of prerequisites) {
        indegree[course] += 1;
    }
    for (let i = 0; i < indegree.length; i++) {
        if (indegree[i] === 0) {
            queue.push(i);
        }
    }
    let count = 0;

    while (queue.length !== 0) {
        const c = queue.pop();
        count += 1;

        for (const [course, prereq] of prerequisites) {
            if (prereq === c) {
                indegree[course] -= 1;
                if (indegree[course] === 0) {
                    queue.push(course);
                }
            }
        }
    }
    return count === numCourses;
};
```
*** 
547. Number of Provinces 

TC: O(n) + O(V + E) =  O(n) N Recursive Stack  Vertex + Edge
SC: O(N)   Store Visited Array

```
/**
 * @param {number[][]} isConnected
 * @return {number}
 SC O(n)
 TC O(n) + O(V + E) =  O(n)
 */
var findCircleNum = function (isConnected) {

    let adj = {};

    for (let i = 0; i < isConnected.length; i++) {
        for (let j = 0; j < isConnected[i].length; j++) {
            if (!adj[i]) adj[i] = [];
            if (!adj[j]) adj[j] = [];

            if (isConnected[i][j] == 1 && i != j) {
                adj[i].push(j);
                adj[j].push(i);
            }
        }
    }

    let visited = [0];
    let provinces = 0;

    for (let i = 0; i < isConnected[0].length; i++) {
        if (!visited[i]) {
            provinces++;
            dfs(i, adj, visited);
        }
    }

    return provinces;
};


function dfs(node, adj, visited) {
    visited[node] = 1;
    for (let item of adj[node]) {
        if (!visited[item]) {
            dfs(item, adj, visited);
        }
    }
}

```
[![YT Video](https://img.youtube.com/vi/ACzkVtewUYA/0.jpg)](https://www.youtube.com/watch?v=ACzkVtewUYA)

*** 


994. Rotting Oranges -n https://leetcode.com/problems/rotting-oranges/description/

TC and SC  = O(M * N)

```
/**
 * @param {number[][]} grid
 * @return {number}
 */
var orangesRotting = function (grid) {
    let queue = [];
    let time = 0, freshOranges = 0;
    let rows = grid.length;
    let cols = grid[0].length;

    // Count the no, of fresh orangesand push the rotten oranges
    for (let row = 0; row < rows; row++) {
        for (let col = 0; col < cols; col++) {
            if (grid[row][col] == 1) freshOranges++;
            if (grid[row][col] == 2) {
                queue.push([row, col]);
            }
        }
    }

    let directions = [[0, 1], [0, -1], [1, 0], [-1, 0]];
    while (queue.length && freshOranges > 0) {
        let newQueue = [];
        while (queue.length) {
            let [r, c] = queue.shift();

            for (let dir of directions) {
                let [row, col] = [dir[0] + r, dir[1] + c];
                // on end bounds and when not a fresh orange continue
                if (row < 0 || row == rows || col < 0 || col == cols || grid[row][col] != 1) continue;

                grid[row][col] = 2;
                newQueue.push([row, col]);
                freshOranges--
            }
        }
        time++;
        queue = newQueue;
    }

    return (freshOranges == 0) ? time : -1;
};

```

[![YT Video](https://img.youtube.com/vi/y704fEOx0s0/0.jpg)](https://www.youtube.com/watch?v=y704fEOx0s0)

*** 
