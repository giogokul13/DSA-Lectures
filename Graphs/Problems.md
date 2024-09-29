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

DFS Recursion 

```
class Solution {
    // Function to return a list containing the DFS traversal of the graph.
    // Function to return a list containing the DFS traversal of the graph.
    dfsOfGraph(V, adj) {
        let visited = new Array(V).fill(false);  // Visited array to keep track of visited nodes
        let result = [];  // Array to store the DFS traversal path

        // Start DFS traversal from the first vertex (vertex 0)
        this.depthTraverse(0, adj, visited, result);

        return result;  // Return the traversal path as an array
    }

    // Helper method for DFS traversal
    depthTraverse(vertex, adj, visited, result) {
        // Mark the current vertex as visited
        visited[vertex] = true;
        result.push(vertex);  // Add the current vertex to the result path

        // Traverse all the adjacent vertices
        for (let node of adj[vertex]) {
            if (!visited[node]) {
                this.depthTraverse(node, adj, visited, result);
            }
        }
    }
}
```

***

### 997. Find the Town Judge

Time and Space are O(N)

```
/**
 * @param {number} n
 * @param {number[][]} trust
 * @return {number}
 */
var findJudge = function (n, trust) {
    if (n === 1) return 1; // If there's only one person, they are the judge by default

    let inDegree = new Array(n + 1).fill(0); // People who trust this person
    let outDegree = new Array(n + 1).fill(0); // People this person trusts

    for (let [a, b] of trust) {
        outDegree[a]++;
        inDegree[b]++;
    }

    // The town judge should be trusted by everyone else (n - 1) and trust no one
    for (let i = 1; i <= n; i++) {
        if (inDegree[i] === n - 1 && outDegree[i] === 0) {
            return i;
        }
    }

    return -1; // No judge found
};
```
***

### 1971. Find if Path Exists in Graph

Time and Space O(V + E)

```
/**
 * @param {number} n
 * @param {number[][]} edges
 * @param {number} source
 * @param {number} destination
 * @return {boolean}
 */
var validPath = function (n, edges, source, destination) {
    if (n == 1) return true;

    // If the source and destination are the same, return true
    if (source === destination) return true;

    let adjList = new Map();
    let queue = [source];
    let visited = new Set();
    visited.add(source);

    for (let [a, b] of edges) {
        if (!adjList.has(a)) adjList.set(a, []);
        if (!adjList.has(b)) adjList.set(b, []);

        adjList.get(a).push(b);
        adjList.get(b).push(a);
    }

    let front = 0; // Manage front of the queue to avoid using shift()
    let bfsTraversal = () => {
        while (front < queue.length) {
            let element = queue[front++]; // Get the current node from the queue
            for (let node of adjList.get(element)) {
                if (destination == node) return true;

                if (!visited.has(node)) {
                    queue.push(node); // Mark neighbor as visited
                    visited.add(node); // Add the neighbor to the queue
                }
            }
        }

        return false;
    }

    return bfsTraversal();
};
```

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
Another Solution

```
/**
 * @param {number} numCourses
 * @param {number[][]} prerequisites
 * @return {boolean}
 */
var canFinish = function (numCourses, prerequisites) {

    // construct a adjacency list with the Prerequisites

    let preMap = new Map();

    for (let i = 0; i < numCourses; i++) { // Set a default Map to each course ie AdjacencyList of each course
        preMap.set(i, []);
    }

    for (let [course, preReq] of prerequisites) {
        let preArr = preMap.get(course);
        preArr.push(preReq);

        preMap.set(course, preArr);
    }

    let visited = new Set();

    let traverseDFS = function (course) {
        if (visited.has(course)) return false;

        if (preMap.get(course)?.length == 0) return true;

        visited.add(course);
        let coursePreReq = preMap.get(course);
        for (let pre of coursePreReq) {
            if (!traverseDFS(pre)) return false;
        }
        visited.delete(course);
        preMap.set(course, []);
        return true;
    }

    for (let i = 0; i < numCourses; i++) {
        if (!traverseDFS(i)) return false;
    }

    return true;
};
```
[![YT Video](https://img.youtube.com/vi/EgI5nU9etnU/0.jpg)](https://www.youtube.com/watch?v=EgI5nU9etnU)

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
### Video Reference
[![YT Video](https://img.youtube.com/vi/y704fEOx0s0/0.jpg)](https://www.youtube.com/watch?v=y704fEOx0s0)

*** 

### 542. 01 Matrix

TC and SC O(M * N)

```
/**
 * @param {number[][]} mat
 * @return {number[][]}
 */
var updateMatrix = function(mat) {
    const rows = mat.length;
    const cols = mat[0].length;
    const directions = [[0, 1], [0, -1], [1, 0], [-1, 0]];
    const queue = [];

    for (let i = 0; i < rows; i++) {
        for (let j = 0; j < cols; j++) {
            if (mat[i][j] === 0) {
                queue.push([i, j]);
            } else {
                mat[i][j] = Infinity;
            }
        }
    }

    while (queue.length > 0) {
        const [row, col] = queue.shift();

        for (const [dr, dc] of directions) {
            const new_row = row + dr;
            const new_col = col + dc;

            if (new_row >= 0 && new_row < rows && new_col >= 0 && new_col < cols && mat[new_row][new_col] > mat[row][col] + 1) {
                mat[new_row][new_col] = mat[row][col] + 1;
                queue.push([new_row, new_col]);
            }
        }
    }

    return mat;    
};
```

***

### 130. Surrounded Regions

TC  O(M * N)
SP = O(1)

```
/**
 * @param {character[][]} board
 * @return {void} Do not return anything, modify board in-place instead.
 */
var solve = function (board) {
    let rows = board.length;
    let cols = board[0].length;

    // Capture the unsurrounded regions (O -> #)
    function capture(r, c) {
        if (r < 0 || c < 0 || r >= rows || c >= cols || board[r][c] != 'O') return;

        board[r][c] = "#";
        capture(r + 1, c);
        capture(r - 1, c);
        capture(r, c + 1);
        capture(r, c - 1);
    }

    // Start from the boundary and capture all connected 'O's
    for (let i = 0; i < rows; i++) { // this covers the first col and last col
        if (board[i][0] === 'O') capture(i, 0);
        if (board[i][cols - 1] === 'O') capture(i, cols - 1);
    }

    for (let j = 0; j < cols; j++) { // this covers the first row and last row
        if (board[0][j] === 'O') capture(0, j);
        if (board[rows - 1][j] === 'O') capture(rows - 1, j);
    }

    // Change all 'O' to 'X' and '#' back to 'O'
    for (let i = 0; i < rows; i++) {
        for (let j = 0; j < cols; j++) {
            if (board[i][j] === 'O') board[i][j] = 'X';
            if (board[i][j] === '#') board[i][j] = 'O';
        }
    }

};

```

### Video Reference
[![YT Video](https://img.youtube.com/vi/9z2BunfoZ5Y/0.jpg)](https://www.youtube.com/watch?v=9z2BunfoZ5Y)

*** 

1020. Number of Enclaves

Time complexity:
    O(M * N) Loop through the Grid
Space complexity:
    O(M * N) Constrcut the M * N Visited Array


```
/**
 * @param {number[][]} grid
 * @return {number}
 */
var numEnclaves = function (grid) {
    let rows = grid.length;
    let cols = grid[0].length;
    let visited = Array.from({ length: rows }, () => Array(cols).fill(false));

    function dfs(r, c) {
        if (r < 0 || r >= rows || c < 0 || c >= cols || visited[r][c] || grid[r][c] === 0) return 0;

        visited[r][c] = true;
        let res = 1;
        let directions = [[0, 1], [0, -1], [1, 0], [-1, 0]];

        for (let dir of directions) {
            res += dfs(r + dir[0], c + dir[1]);
        }

        return res;
    }

    let totalLand = 0;
    let borderLand = 0;

    // First, mark all border-connected lands
    for (let i = 0; i < rows; i++) {
        for (let j = 0; j < cols; j++) {
            if ((i === 0 || i === rows - 1 || j === 0 || j === cols - 1) && grid[i][j] === 1) {
                borderLand += dfs(i, j);
            }
        }
    }

    // Count all land cells
    for (let i = 0; i < rows; i++) {
        for (let j = 0; j < cols; j++) {
            if (grid[i][j] === 1) {
                totalLand++;
            }
        }
    }

    return totalLand - borderLand;
};
```
### Video reference 

[![YT Video](https://img.youtube.com/vi/gf0zsh1FIgE/0.jpg)](https://www.youtube.com/watch?v=gf0zsh1FIgE)

*** 


### 785. Is Graph Bipartite?
TC O(V + E)
SC O(V)

```
/**
 * @param {number[][]} graph
 * @return {boolean}
 */
var isBipartite = function (graph) {
    let odd = new Array(graph.length).fill(0);

    function bfs(i) {
        if (odd[i]) return true;

        let queue = [i];
        odd[i] = -1;

        while (queue.length > 0) {
            i = queue.shift();
            for (let node of graph[i]) {
                if (odd[i] == odd[node]) {
                    return false;
                } else if (!odd[node]) {
                    queue.push(node);
                    odd[node] = -1 * odd[i];
                }
            }
        }
        return true;
    }


    for (let i = 0; i < graph.length; i++) {
        if (!bfs(i)) return false;
    }

    return true;
};
```
[![YT Video](https://img.youtube.com/vi/mev55LTubBY/0.jpg)](https://www.youtube.com/watch?v=mev55LTubBY)

***

### 210. Course Schedule II
TC O(V + E)
SP - O(V)

```
/**
 * @param {number} numCourses
 * @param {number[][]} prerequisites
 * @return {number[]}
 */
var findOrder = function (numCourses, prerequisites) {

    // Initialize the graph as an adjacency list
    let graph = new Map();
    for (let i = 0; i < numCourses; i++) {
        graph.set(i, []);
    }

    // Build the graph
    for (let [course, prereq] of prerequisites) {
        graph.get(prereq).push(course);
    }

    let result = [];
    let white = new Set();
    let grey = new Set();
    let black = new Set();

    // Add all courses to the white set initially
    for (let i = 0; i < numCourses; i++) {
        white.add(i);
    }

    // Helper DFS function
    function dfs(course) {
        // Move course to the grey set
        white.delete(course);
        grey.add(course);

        for (let prereq of graph.get(course)) {
            if (black.has(prereq)) continue;  // Skip already processed nodes
            if (grey.has(prereq)) return false;  // Cycle detected
            if (!dfs(prereq)) return false;
        }

        // Move course to the black set
        grey.delete(course);
        black.add(course);
        result.push(course);

        return true;
    }

    // Process each course
    while (white.size > 0) {
        let course = white.values().next().value;  // Get any element from white set
        if (!dfs(course)) return [];  // Return empty if a cycle is detected
    }

    return result.reverse();  // Reverse the result to get the correct order

};
```
[![YT Video](https://img.youtube.com/vi/6vaSka3rwDQ/0.jpg)](https://www.youtube.com/watch?v=6vaSka3rwDQ)


***


### 802. Find Eventual Safe States

TC - O (V + E) Traversing all the Edges and Nodes
SC - O(V) as we use hash map it may have all vertices at worstCase

```
/**
 * @param {number[][]} graph
 * @return {number[]}
 */
var eventualSafeNodes = function (graph) {
    let safe = new Map(); // track all the safe nodes.

    let result = [];

    dfs = function (i) {
        if (safe.has(i)) return safe.get(i);

        safe.set(i, false);
        for (let neighbour of graph[i]) { // loop through all the subElements in the graph
            if (!dfs(neighbour)) {
                return safe[i];
            }
        }
        safe.set(i, true);
        return safe.get(i);
    }

    for (let i = 0; i < graph.length; i++) {
        if (dfs(i)) result.push(i); // Loop through all the nodes 0, 1, 2 ... n - 1
    }

    return result;
};
```

[![YT Video](https://img.youtube.com/vi/Re_v0j0CRsg/0.jpg)](https://www.youtube.com/watch?v=Re_v0j0CRsg)

***

### 1319. Number of Operations to Make Network Connected

TC - O(V + E);
SP O(V)

```
/**
 * @param {number} n
 * @param {number[][]} connections
 * @return {number}
 */
var makeConnected = function (n, connections) {

    // base condition if the wires/cables are less than nodes - 1;
    if (connections.length < n - 1) return -1;

    let neighbors = {};

    let isVisited = Array(n).fill(false);

    for (let node = 0; node < n; node++) { // defult construction to neighbors Map
        neighbors[node] = [];
    }

    for (let connection of connections) {
        neighbors[connection[0]].push(connection[1]);
        neighbors[connection[1]].push(connection[0]);
    }

    let networkCount = 0;

    for (let node = 0; node < n; node++) {
        if (!isVisited[node]) {
            traverseNetwork(node);

            networkCount++;
        }
    }

    return networkCount - 1;


    function traverseNetwork(node) {
        isVisited[node] = true;
        for (const neighborNode of neighbors[node]) {
            if (!isVisited[neighborNode]) {
                traverseNetwork(neighborNode);
            }
        }

    }
}; 
```

***

### 947. Most Stones Removed with Same Row or Column

TC O(N^2)
SC O(N)

```
/**
 * @param {number[][]} stones
 * @return {number}
 */
var removeStones = function (stones) {

    let visited = new Set();
    let validStones = 0;

    let traverse = function (row, col) {
        let key = "" + row + "-" + col + "";
        if (visited.has(key)) return;

        visited.add(key);

        for (let [x, y] of stones) {
            if (row == x || col == y) traverse(x, y);
        }
    }

    for (let [x, y] of stones) {
        let key = "" + x + "-" + y + "";

        if (visited.has(key)) continue;
        traverse(x, y);
        validStones++;
    }

    return stones.length - validStones;
};

```

***

### 1091. Shortest Path in Binary Matrix

TC and SC - O(N) as we might travel to all cells and store all values in the Queue. 

```
var shortestPathBinaryMatrix = function (grid) {

    let len = grid.length;

    if (grid[0][0] != 0) return -1;

    let queue = [[0, 0, 1]];
    //                 right   down    top       left   dia-right dia-left rightup  left-down
    let directions = [[0, 1], [1, 0], [0, -1], [-1, 0], [1, 1], [-1, -1], [1, -1], [-1, 1]];

    while (queue.length > 0) {
        let [row, col, length] = queue.shift();

        if (row == (len - 1) && col == (len - 1)) return length;

        for ([dr, dc] of directions) {
            let x = row + dr;
            let y = col + dc;

            if (x < 0 || x >= len) continue;
            if (y < 0 || y >= len) continue;
            if (grid[x][y] == 1) continue;

            queue.push([x, y, length + 1]);
            grid[x][y] = 1; // mark this as visited
        }
    }

    return -1;
};
```
[![YT Video](https://img.youtube.com/vi/YnxUdAO7TAo/0.jpg)](https://www.youtube.com/watch?v=YnxUdAO7TAo)

***

### 1631. Path With Minimum Effort

TC O(V + M)

```
/**
 * @param {number[][]} heights
 * @return {number}
 */
var minimumEffortPath = function(heights) {
    const rows = heights.length, cols = heights[0].length;
    const curEffort = Array.from(Array(rows), () => Array(cols).fill(Infinity));
    const minHeap = [[0, 0, 0]];  // [effort, row, col]
    
    curEffort[0][0] = 0;
    const directions = [[0, 1], [0, -1], [1, 0], [-1, 0]];
    
    while (minHeap.length > 0) {
        const [effort, row, col] = minHeap.shift();
        
        if (effort > curEffort[row][col]) continue;
        
        if (row === rows - 1 && col === cols - 1) return effort;
        
        for (const [dr, dc] of directions) {
            const newRow = row + dr, newCol = col + dc;
            if (newRow >= 0 && newRow < rows && newCol >= 0 && newCol < cols) {
                const newEffort = Math.max(effort, Math.abs(heights[row][col] - heights[newRow][newCol]));
                if (newEffort < curEffort[newRow][newCol]) {
                    curEffort[newRow][newCol] = newEffort;
                    minHeap.push([newEffort, newRow, newCol]);
                    minHeap.sort((a, b) => a[0] - b[0]);
                }
            }
        }
    }
    return -1;
};

***

var minimumEffortPath = function (heights) {
    let m = heights.length;
    let n = heights[0].length;
    let visited = new Set();
    function isMiniEffort(row, col, limit, preHeight) {
        if (row >= m || col >= n || row < 0 | col < 0) return false;
        let position = `${row}_${col}`;
        let height = heights[row][col];

        if (visited.has(position)) return false;
        if (Math.abs(height - preHeight) > limit) return false;
        if (row === m - 1 && col === n - 1) return true;
        visited.add(position);
        return isMiniEffort(row - 1, col, limit, height) ||
            isMiniEffort(row + 1, col, limit, height) ||
            isMiniEffort(row, col - 1, limit, height) ||
            isMiniEffort(row, col + 1, limit, height);
    };
    let left = 0;
    let right = 10 ** 6;

    while (left < right) {
        const mid = Math.floor((left + right) / 2);

        visited.clear();
        isMiniEffort(0, 0, mid, heights[0][0])
            ? right = mid
            : left = mid + 1
    }
    return left;
};
```
### Video Reference
[![YT Video](https://img.youtube.com/vi/XQlxCCx2vI4/0.jpg)](https://www.youtube.com/watch?v=XQlxCCx2vI4)


***

### 787. Cheapest Flights Within K Stops

The time complexity of this solution is O(k * |flights|), where k is the maximum number of stops allowed and |flights| is the number of flights. This is because we iterate k times through the flights array to update the prices array.

The space complexity is O(n) because we are using an array of size n to store the prices of each node.

```
/**
 * @param {number} n
 * @param {number[][]} flights
 * @param {number} src
 * @param {number} dst
 * @param {number} k
 * @return {number}
 Bellman ford Algorithm
 */
var findCheapestPrice = function (n, flights, src, dst, k) {
    let prices = Array(n).fill(Infinity);
    prices[src] = 0;

    for (let i = 0; i < k + 1;  i++) {
        let tempPrice = prices.slice();

        for (let [source, dest, price] of flights) {
            if (prices[source] == Infinity) continue;

            if ((prices[source] + price) < tempPrice[dest]) {
                tempPrice[dest] = prices[source] + price;
            }

        }
        prices = tempPrice
    }

    return (prices[dst] == Infinity) ? -1 : prices[dst];
};
```
[![YT Video](https://img.youtube.com/vi/5eIK3zUdYmE/0.jpg)](https://www.youtube.com/watch?v=5eIK3zUdYmE)

***

### 743. Network Delay Time

## Redo the Problem
```

```

***


### 1976. Number of Ways to Arrive at Destination

TC  =   O((V + E) * logn) as Priority Queue as been used.
SC -  O(V + E) as all the nodes and their edges were used.

```
/**
 * @param {number} n
 * @param {number[][]} roads
 * @return {number}
 */
var countPaths = function (n, roads) {
    let adjacencyList = {};
    let paths = 0;
    const MOD = Math.pow(10, 9) + 7;

    for (let [p1, p2, time] of roads) {
        if (!adjacencyList[p1]) adjacencyList[p1] = [];
        if (!adjacencyList[p2]) adjacencyList[p2] = [];
        adjacencyList[p1].push([p2, time]);
        adjacencyList[p2].push([p1, time]);
    }

    let dis = new Array(n).fill(Infinity);
    let ways = new Array(n).fill(0)
    ways[n - 1] = 1;
    dis[n - 1] = 0;

    let dijkstras = function () {
        let heap = new MinPriorityQueue({ priority: x => x[1] });
        heap.enqueue([n - 1, 0]);
        while (heap.size()) {
            let [node, time1] = heap.dequeue().element;
            if (node) {
                for (let [nextNode, time2] of adjacencyList[node]) {
                    let total = time1 + time2;
                    if (dis[nextNode] == total) {
                        ways[nextNode] = (ways[nextNode] + ways[node]) % MOD;
                    } else if (dis[nextNode] > total) {
                        dis[nextNode] = total;
                        ways[nextNode] = ways[node];
                        heap.enqueue([nextNode, total]);
                    }
                }
            }
        }
    }
    dijkstras();
    return ways[0];
};

```

```
//{ Driver Code Starts
//Initial Template for javascript

"use strict";

process.stdin.resume();
process.stdin.setEncoding("utf-8");

let inputString = "";
let currentLine = 0;

process.stdin.on("data", (inputStdin) => {
  inputString += inputStdin;
});

process.stdin.on("end", (_) => {
  inputString = inputString
    .trim()
    .split("\n")
    .map((string) => {
      return string.trim();
    });

  main();
});

function readLine() {
  return inputString[currentLine++];
}

/* Function to print an array */
function printArray(arr, size) {
  let i;
  let s = "";
  for (i = 0; i < size; i++) {
    if(arr[i] === -0)
      arr[i] = 0;
    s += arr[i] + " ";
  }
  console.log(s);
}

function main() {
  let t = parseInt(readLine());
  let i = 0;
  for (; i < t; i++) {
    let input_line = readLine().split(" ").map((x)=>parseInt(x));
    let V = input_line[0];
    let E = input_line[1];
    let adj = new Array(V);
    for(let j = 0;j<V;j++) adj[j] = new Array();
    for(let j = 0;j < E;j++){
      input_line = readLine().split(" ").map((x)=>parseInt(x));
      let u = input_line[0];
      let v = input_line[1];
      let w = input_line[2];
      adj[u].push([v,w]);
      adj[v].push([u,w]);
    }

    let S = parseInt(readLine());
    let obj = new Solution();
    let res = obj.dijkstra(V,adj,S);
    printArray(res,res.length);
  }
}
// } Driver Code Ends


//User function Template for javascript

/**
 * @param {number} V
 * @param {number[][][]} Adj
 * @param {number} S
 * @return {number[]}
 */
class Solution
{
    //Function to find the shortest distance of all the vertices
    //from the source vertex S.
    dijkstra(V,Adj,S)
    {
        
        let output = new Array(V).fill(Infinity);
        output[S] = 0;
        let queue = new MinPriorityQueue();
        queue.enqueue([S, 0]);
        while(queue.size()> 0) {
            let [vertex, distance] = queue.dequeue();
            
            for(let [neighbour, weight] of Adj[vertex]) {
                let newDist = distance + weight;
                
                if(newDist < output[neighbour]) {
                    output[neighbour] = newDist;
                    queue.enqueue([neighbour, newDist])
                }
            }
        }
        
        return output;
    }
    
}

class MinPriorityQueue {
    constructor() {
        this.queue = [];
    }

    enqueue(item) {
        this.queue.push(item);
        this.queue.sort((a, b) => a[1] - b[1]); // sort based on the distance (min-heap behavior)
    }

    dequeue() {
        return this.queue.shift(); // dequeue the element with the smallest distance
    }

    size() {
        return this.queue.length;
    }
}
```

***



***


### 1334. Find the City With the Smallest Number of Neighbors at a Threshold Distance

TC: O(N ^ 3)
SC: O(N ^ 2)

```
/**
 * @param {number} n
 * @param {number[][]} edges
 * @param {number} distanceThreshold
 * @return {number}
 Solve using Floyd Warshall
 */
var findTheCity = function (n, edges, distanceThreshold) {
    let distanceMatrix = Array(n).fill().map(() =>
        Array(n).fill(Infinity));


    for (let edge of edges) {
        distanceMatrix[edge[0]][edge[1]] = edge[2];
        distanceMatrix[edge[1]][edge[0]] = edge[2];
    }

    for (let i = 0; i < n; i++) {
        distanceMatrix[i][i] = 0; // changing the self node distance to 0 from Infinity as Slef node travesal distance is zero
    }

    for (let k = 0; k < n; k++) {
        for (let i = 0; i < n; i++) {
            for (let j = 0; j < n; j++) {
                distanceMatrix[i][j] = Math.min(distanceMatrix[i][j], distanceMatrix[i][k] + distanceMatrix[k][j]);
            }
        }
    }

    let cityCount = n;
    let cityNum = -1;

    for (let city = 0; city < n; city++) { // traverse through the cities
        let count = 0;
        for (let adjCity = 0; adjCity < n; adjCity++) {
            // check if the distance between the points is under the given threshold
            if (distanceMatrix[city][adjCity] <= distanceThreshold) count++;
        }

        if (count <= cityCount) { // if the current count city has less values then assign that to maintain the city.
            cityCount = count;
            cityNum = city;
        }
    }

    return cityNum;

    // console.log(distanceMatrix);

};
```
[![YT Video](https://img.youtube.com/vi/PwMVNSJ5SLI/0.jpg)](https://www.youtube.com/watch?v=PwMVNSJ5SLI)

***


### 721. Accounts Merge

TC: O(N LogN);
SC: O(N)

The time complexity of this solution is O(n * log(n)), where n is the total number of emails across all accounts. This is because we are iterating through each account and each email within the account, and sorting the emails in the adjacency list. The sorting operation has a time complexity of O(n * log(n)).

The space complexity is O(n), where n is the total number of emails across all accounts. This is because we are using a namesObj to store the mapping of email to name, an adjacencyList to store the relationships between emails, a result array to store the final merged accounts, and a visited set to keep track of visited emails during the depth-first search.


```
/**
 * @param {string[][]} accounts
 * @return {string[][]}
 */
var accountsMerge = function (accounts) {

    let namesObj = {};
    let adjacencyList = {};

    for (let account of accounts) { //account = [name, email1, email2, email3...];
        let name = account[0];
        namesObj[account[1]] = name;
        let emails = [];
        for (let i = 1; i < account.length; i++) {
            if (!adjacencyList[account[i]]) adjacencyList[account[i]] = new Set();
            if (!adjacencyList[account[1]]) adjacencyList[account[i]] = new Set();
            namesObj[account[i]] = name;
            if (i != 1) {
                adjacencyList[account[1]].add(account[i]);
                adjacencyList[account[i]].add(account[1]);
            }
        }
    }

    let result = [];
    let visited = new Set();

    let dfs = function (email) {
        visited.add(email);
        let emails = [email];
        adjacencyList[email].forEach((e) => {
            if (!visited.has(e)) {
                emails.push(...dfs(e));
            }
        });

        return emails;
    }


    for (let key in adjacencyList) {
        if (!visited.has(key)) {
            let temp = dfs(key);
            temp.sort();
            temp.unshift(namesObj[temp[0]]);
            result.push(temp);
        }
    }

    console.log(adjacencyList);
    return result;
};
```

***

###  Topological Sort 

### DFS 

Time Complexity: O(V + E).
Auxiliary Space: O(V).

```
/**
 * @param {number} V
 * @param {number[][]} adj
 * @returns {number[]}
*/
class Solution 
{
    //Function to return list containing vertices in Topological order.
    topoSort(V, adj) {
       let visited = new Set();
       let stack = [];
       
       const dfs = (vertex) => {
           visited.add(vertex);
           
           for(let node of adj[vertex]) {
               if(!visited.has(node)) {
                   dfs(node);
               }
           }
           
           stack.push(vertex);
       }
       
       for(let i = 0; i < V; i++) {
           if(!visited.has(i)) dfs(i);
       }
       
       return stack.reverse();
    }
}
```

### 200. Number of Islands

Time O(M * N)
Space O(1)

```
/**
 * @param {character[][]} grid
 * @return {number}
 */
var numIslands = function (grid) {
    let islands = 0;

    for (let row = 0; row < grid.length; row++) {
        for (let col = 0; col < grid[0].length; col++) {
            if (grid[row][col] == 1) {
                islands += 1;

                traverse(row, col, grid);
            }
        }
    }

    return islands;

};


function traverse(row, col, grid) {

    if (
        row < 0 || row > grid.length - 1
        || col < 0 || col > grid[0].length - 1
        || grid[row][col] == '0') return;

    grid[row][col] = "0";

    traverse(row + 1, col, grid);
    traverse(row - 1, col, grid);
    traverse(row, col + 1, grid);
    traverse(row, col - 1, grid);

}
```

***


### 310. Minimum Height Trees

Time and Space O(N)
```
/**
 * @param {number} n
 * @param {number[][]} edges
 * @return {number[]}
 */
var findMinHeightTrees = function (n, edges) {
    if (n < 2) return [0] // when the tree has less than two nodes the height is zero;

    let adjList = {};

    // Creating an Adjacency List to construct a undirected graph
    for (let [i, j] of edges) {
        if (!adjList[i]) adjList[i] = [];
        if (!adjList[j]) adjList[j] = [];

        adjList[j].push(i);
        adjList[i].push(j);
    }

    let leaves = [];

    // Check if any of the node has one path or connected to one node
    for (let node in adjList) {
        if (adjList[node].length == 1) {
            leaves.push(parseInt(node));
        }
    }

    while (n > 2) {
        n -= leaves.length;
        let newLeaves = [];

        for (let leaf of leaves) {
            let adjNode = adjList[leaf].pop();
            adjList[adjNode].splice(adjList[adjNode].indexOf(leaf), 1); // delete the identified node
            if (adjList[adjNode].length == 1) {
                newLeaves.push(adjNode);
            }
        }
        leaves = newLeaves;
    }

    return leaves;
};
```

***

### 133. Clone Graph
Time (V + E)
Space O(N)
```
/**
 * // Definition for a _Node.
 * function _Node(val, neighbors) {
 *    this.val = val === undefined ? 0 : val;
 *    this.neighbors = neighbors === undefined ? [] : neighbors;
 * };
 */

/**
 * @param {_Node} node
 * @return {_Node}
 */
var cloneGraph = function (node) {

    if (node === null) {
        return null;
    }
    const map = new Map();
    const clone = root => {
        if (!map.has(root.val)) {
            map.set(root.val, new Node(root.val));
            map.get(root.val).neighbors = root.neighbors.map(clone);
        }
        return map.get(root.val);
    }
    return clone(node);
};
```

***

### 399. Evaluate Division

The time complexity of this code is O(n * m) where n is the number of equations and m is the number of queries. This is because for each query, the code may need to traverse the graph to find the result, and the graph traversal may involve visiting all nodes in the worst case.

The space complexity is O(n) where n is the number of equations. This is because the code constructs a graph to represent the equations, and the size of the graph is proportional to the number of equations.

```
/**
 * @param {string[][]} equations
 * @param {number[]} values
 * @param {string[][]} queries
 * @return {number[]}
 */
var calcEquation = function (equations, values, queries) {
    let graph = {};
    for (let index = 0; index < equations.length; index++) {
        let val = values[index];
        let [num, den] = equations[index];

        if (!graph[num]) graph[num] = {};
        if (!graph[den]) graph[den] = {};

        graph[num][den] = val;
        graph[den][num] = 1 / val;
    }

    let execute = (num, den, visited) => {
        if (!(num in graph) || !(den in graph)) return -1;

        if (num == den) return 1;

        visited.add(num);
        let neighbours = graph[num];

        for (let neighbour in neighbours) {
            if (!visited.has(neighbour)) {
                let result = execute(neighbour, den, visited);

                if (result !== -1) {
                    return neighbours[neighbour] * result;
                }
            }
        }

        return -1;
    }

    let results = [];

    for (let query of queries) {
        let [num, den] = query;
        let visited = new Set();
        let result = execute(num, den, visited);

        results.push(result);
    }

    return results;
};
```

***


### 684. Redundant Connection
Time O(N ^ 2) Space O(N)

```
/**
 * @param {number[][]} edges
 * @return {number[]}
 */
var findRedundantConnection = function (edges) {
    // Initialize adjacency list
    const adjList = {};

    // Helper function to perform DFS
    const dfs = (source, target, visited) => {
        if (source === target) return true;  // Found a path to the target
        
        visited.add(source);  // Mark the source as visited
        
        for (const neighbor of adjList[source] || []) {  // Check neighbors
            if (!visited.has(neighbor)) {
                if (dfs(neighbor, target, visited)) {  // Recursive DFS call
                    return true;
                }
            }
        }
        
        return false;
    };

    // Process each edge
    for (const [u, v] of edges) {
        const visited = new Set();
        
        // Check if there's already a path between u and v using DFS
        if (adjList[u] && adjList[v] && dfs(u, v, visited)) {
            return [u, v];  // If path exists, this edge is redundant
        }

        // Add the edge to the adjacency list
        if (!adjList[u]) adjList[u] = [];
        if (!adjList[v]) adjList[v] = [];
        adjList[u].push(v);
        adjList[v].push(u);
    }

    return [];
};

```

***

### 797. All Paths From Source to Target

Time and Space O(N ^ 2)

```
/**
 * @param {number[][]} graph
 * @return {number[][]}
 */
var allPathsSourceTarget = function (graph) {

    if (!graph.length) return [];

    const targetNode = graph.length - 1;
    let paths = [];

    let dfs = (node, path) => {
        if (node == targetNode) {
            paths.push([...path]);
            return;
        }

        for (let neighbour of graph[node]) {
            dfs(neighbour, [...path, neighbour]) // Combine the original path + current element to get the entire path
        }
    }

    dfs(0, [0]);

    return paths;
};
```

***

### 841. Keys and Rooms

The time complexity of this solution is O(n + e), where n is the number of rooms and e is the total number of keys in all rooms. This is because we are visiting each room and each key exactly once.

The space complexity is also O(n + e) due to the space used by the visited set and the recursive call stack.

```
/**
 * @param {number[][]} rooms
 * @return {boolean}
 */
var canVisitAllRooms = function (rooms) {
    let visited = new Set();

    let recurse = (node) => {
        visited.add(node);
        for (let neighbour of rooms[node]) {
            if (!visited.has(neighbour)) {
                recurse(neighbour);
            }
        }

        return visited;
    }

    recurse(0);

    return visited.size == rooms.length;
};
```

***

### 851. Loud and Rich

Time O(N ^ 2)
Space O(N)

```
/**
 * @param {number[][]} richer
 * @param {number[]} quiet
 * @return {number[]}
 */
var loudAndRich = function (richer, quiet) {
    let richMap = new Array(quiet.length)

    for (let i = 0; i < richMap.length; ++i) {
        richMap[i] = []
    }
    for (const richerPair of richer) {
        richMap[richerPair[1]].push(richerPair[0])
    }

    let answer = new Array(quiet.length);

    let calculateLoudestPerson = (person) => {
        if (!answer[person]) {
            let loudestPerson = person;
            let richLoudestPerson;

            for (let richPerson of richMap[person]) {
                richLoudestPerson = calculateLoudestPerson(richPerson);

                if (quiet[richLoudestPerson] < quiet[loudestPerson]) {
                    loudestPerson = richLoudestPerson;
                }
            }

            answer[person] = loudestPerson;
        }

        return answer[person];
    }


    for (let i = 0; i < quiet.length; i++) {
        calculateLoudestPerson(i);
    }

    return answer

}; 
```

***

### 886. Possible Bipartition

The time complexity of this algorithm is O(n + e), where n is the number of vertices and e is the number of edges in the graph. This is because we are performing a depth-first search on each vertex, and each edge is visited once.

The space complexity of this algorithm is O(n), where n is the number of vertices in the graph. This is because we are using an adjacency list to represent the graph and an array to store the colors of each vertex.


```
/**
 * @param {number} n
 * @param {number[][]} dislikes
 * @return {boolean}
 */
var possibleBipartition = function (n, dislikes) {
    // construct a adjacency List
    let adjList = {};

    for (let i = 1; i <= n; i++) {
        adjList[i] = [];
    }

    for (let [a, b] of dislikes) {
        adjList[b].push(a);
        adjList[a].push(b);
    }

    console.log(adjList);
    let color = new Array(n + 1).fill(-1);

    let dfs = (vertex) => {
        for (let node of adjList[vertex]) {

            // If my neighbour nodes are in same color return false// bacause they cannot be Bipartite
            if (color[node] == color[vertex]) return false;

            if (color[node] == -1) {
                color[node] = 1 - color[vertex]; // mark it as Zero if it is not visited before and check the upcoming node;
                if (!dfs(node)) return false;
            }
        }

        return true;
    }

    for (let i = 1; i <= n; i++) {
        if (color[i] == -1) {
            color[i] = 0;
            if (!dfs(i)) return false;
        }
    }

    return true;
};
```

***

### 990. Satisfiability of Equality Equations
https://leetcode.com/problems/satisfiability-of-equality-equations/description

O(T) (V + E) 
O(s) (Y + E)
```
/**
 * @param {string[]} equations
 * @return {boolean}
 */
var equationsPossible = function(equations) {
    const map = new Map(),
          find = item => {
              map.set(item, map.get(item) || item);
              return item === map.get(item) ? item : find(map.get(item));
          };
    
    equations.forEach(([a, eq, , b]) => {
        if (eq === '=') {
            map.set(find(a), find(b));
        }
    });
    
    let complies = true;
    equations.forEach(([a, eq, , b]) => {
        if (eq === '!') {
            if (find(a) === find(b)) complies = false;
        }
    });
    
    return complies;
};
```

***


### 1042. Flower Planting With No Adjacent

Time complexity: O(n + m), where n is the number of nodes in the garden and m is the number of paths. This is because we are iterating through all the nodes and paths in the garden to build the adjacency list and perform the BFS traversal.

Space complexity: O(n), where n is the number of nodes in the garden. This is because we are storing the adjacency list and the answer array, both of which have a size proportional to the number of nodes in the garden.

```
/**
 * @param {number} n
 * @param {number[][]} paths
 * @return {number[]}
 */
var gardenNoAdj = function (n, paths) {
    let adjList = {};
    let answer = new Array(n + 1).fill(0);

    for (let i = 1; i <= n; i++) { adjList[i] = [] }

    for (let [a, b] of paths) {
        if (!adjList[a]) adjList[a] = [];
        if (!adjList[b]) adjList[b] = [];

        adjList[b].push(a);
        adjList[a].push(b);
    }

    let bfsTraversal = (node) => {
        let queue = [node];

        while (queue.length > 0) {
            let curr = queue.shift(); // pop the first element

            if (answer[curr]) continue;

            let visited = new Set();
            console.log(curr);
            for (let vertex of adjList?.[curr]) {
                if (answer[vertex]) visited.add(answer[vertex]);
                else queue.push(vertex);
            }

            let [flower] = [1, 2, 3, 4].filter(flow => !visited.has(flow)) // If it is not visited then assign the first non visited flow number
            answer[curr] = flower;
        }
    }

    for (let i = 1; i <= n; i++) {
        bfsTraversal(i) // traverse all gardens
    }

    answer.shift()// remove the first element as it starts from 0
    return answer;
};
```

***

### 1129. Shortest Path with Alternating Colors

Time O(V + E)
Soace O(N)
```
/**
 * @param {number} n
 * @param {number[][]} redEdges
 * @param {number[][]} blueEdges
 * @return {number[]}
 */
var shortestAlternatingPaths = function (n, redEdges, blueEdges) {
    let redGraph = new Array(n).fill(0).map(() => []);
    let blueGraph = new Array(n).fill(0).map(() => []);

    for (let [a, b] of redEdges) {
        redGraph[a].push(b);
    }

    for (let [a, b] of blueEdges) {
        blueGraph[a].push(b);
    }

    let answer = new Array(n).fill(-1);
    let visited = Array.from({ length: n }, () => [false, false]);

    let queue = [[0, 0, 0], [0, 1, 0]]; // [node, color, distance]; 0 - red; 1 - blue;

    visited[0][0] = visited[0][1] = true;

    while (queue.length > 0) {
        let [node, color, dist] = queue.shift();

        if (answer[node] == -1) {
            answer[node] = dist;
        }

        if (color == 0) {
            for (let neighbour of blueGraph[node]) {
                if (!visited[neighbour][1]) {
                    visited[neighbour][1] = true;
                    queue.push([neighbour, 1, dist + 1]);
                }
            }
        } else {
            for (let neighbour of redGraph[node]) {
                if (!visited[neighbour][0]) {
                    visited[neighbour][0] = true;
                    queue.push([neighbour, 0, dist + 1]);
                }
            }
        }
    }

    return answer;

}; 
```

***


### 1514. Path with Maximum Probability

Time complexity:
- Building the adjacency list: O(E), where E is the number of edges
- Initializing the priority queue: O(1)
- Processing the priority queue: O(E log E), as each edge is processed once and each edge is pushed and popped from the priority queue
Overall, the time complexity is O(E log E).

Space complexity:
- Adjacency list: O(E), as we store each edge in the adjacency list
- Priority queue: O(E), as at most all edges can be in the priority queue
- Maximum probability array: O(n), where n is the number of nodes
Overall, the space complexity is O(E + n).

```
class MaxHeap {
    constructor() {
        this.heap = [];
    }

    // Insert an element into the heap
    push([node, prob]) {
        this.heap.push([node, prob]);
        this._bubbleUp();
    }

    // Remove and return the maximum element
    pop() {
        const max = this.heap[0];
        const end = this.heap.pop();
        if (this.heap.length > 0) {
            this.heap[0] = end;
            this._sinkDown();
        }
        return max;
    }

    // Check if the heap is empty
    isEmpty() {
        return this.heap.length === 0;
    }

    // Bubble up the last element to maintain heap property
    _bubbleUp() {
        let index = this.heap.length - 1;
        const element = this.heap[index];

        while (index > 0) {
            let parentIndex = Math.floor((index - 1) / 2);
            let parent = this.heap[parentIndex];

            if (element[1] <= parent[1]) break; // Max-heap property is satisfied

            this.heap[parentIndex] = element;
            this.heap[index] = parent;
            index = parentIndex;
        }
    }

    // Sink down the first element to maintain heap property
    _sinkDown() {
        let index = 0;
        const length = this.heap.length;
        const element = this.heap[0];

        while (true) {
            let leftChildIndex = 2 * index + 1;
            let rightChildIndex = 2 * index + 2;
            let leftChild, rightChild;
            let swap = null;

            if (leftChildIndex < length) {
                leftChild = this.heap[leftChildIndex];
                if (leftChild[1] > element[1]) {
                    swap = leftChildIndex;
                }
            }

            if (rightChildIndex < length) {
                rightChild = this.heap[rightChildIndex];
                if (
                    (swap === null && rightChild[1] > element[1]) ||
                    (swap !== null && rightChild[1] > leftChild[1])
                ) {
                    swap = rightChildIndex;
                }
            }

            if (swap === null) break;

            this.heap[index] = this.heap[swap];
            this.heap[swap] = element;
            index = swap;
        }
    }
}

var maxProbability = function (n, edges, succProb, start_node, end_node) {
    let adjList = {};

    // Initialize the adjacency list
    for (let i = 0; i < n; i++) {
        adjList[i] = [];
    }

    // Build the adjacency list with edges and success probabilities
    for (let edge = 0; edge < edges.length; edge++) {
        adjList[edges[edge][0]].push([edges[edge][1], succProb[edge]]);
        adjList[edges[edge][1]].push([edges[edge][0], succProb[edge]]);
    }

    // Max-heap (priority queue) to prioritize nodes with higher probability
    let maxHeap = new MaxHeap();
    maxHeap.push([start_node, 1]); // [node, probability]

    // Array to store the maximum probability to reach each node
    let maxProb = new Array(n).fill(0);
    maxProb[start_node] = 1;

    // Process the priority queue
    while (!maxHeap.isEmpty()) {
        // Extract the node with the highest probability
        let [vertex, currProb] = maxHeap.pop();

        // If we've reached the end node, return the probability
        if (vertex === end_node) return currProb;

        // Traverse all neighbors
        for (let [neighbor, prob] of adjList[vertex]) {
            let newProb = currProb * prob;

            // If we find a path with a higher probability, update and push to the heap
            if (newProb > maxProb[neighbor]) {
                maxProb[neighbor] = newProb;
                maxHeap.push([neighbor, newProb]);
            }
        }
    }

    // If we exhaust the queue and haven't reached the end node
    return 0;
};

```
***

### 2192. All Ancestors of a Node in a Directed Acyclic Graph

The time complexity of this algorithm is O(n^2) because we are iterating through each node in the graph and for each node, we are potentially visiting all its ancestors. The space complexity is also O(n^2) because we are storing the ancestors for each node in a set, and there can be up to n ancestors for each node.

```
/**
 * @param {number} n
 * @param {number[][]} edges
 * @return {number[][]}
 */
var getAncestors = function (n, edges) {
    let anscestorList = new Map();

    for (let i = 0; i < n; i++) {
        anscestorList.set(i, []);
    }

    for (let [parent, child] of edges) { // construct an ancestor map
        anscestorList.get(child).push(parent);
    }

    // Array to store the ancestors for each node
    let ancestors = new Array(n).fill(0).map(() => new Set());

    // Perform DFS to find all ancestors for each node
    let dfs = (node) => {
        for (let parent of anscestorList.get(node)) {
            if (!ancestors[node].has(parent)) {
                ancestors[node].add(parent);
                // Recursively add the ancestors of the parent
                dfs(parent);
                // Add all ancestors of the parent to the current node's ancestors
                for (let ancestor of ancestors[parent]) {
                    ancestors[node].add(ancestor);
                }
            }
        }
    };

    // Run DFS for each node to find its ancestors
    for (let i = 0; i < n; i++) {
        dfs(i);
    }

    // Convert the ancestor sets to sorted arrays for the final output
    return ancestors.map(set => [...set].sort((a, b) => a - b));

};  
```
***


### 1311. Get Watched Videos by Your Friends

Time O(V + E)
Space O(N)

```
/**
 * @param {string[][]} watchedVideos
 * @param {number[][]} friends
 * @param {number} id
 * @param {number} level
 * @return {string[]}
 */
var watchedVideosByFriends = function (watchedVideos, friends, id, level) {
    let n = friends.length;

    // Step 1: Perform BFS to find friends at the required level
    let visited = new Array(n).fill(false);
    let queue = [id];
    visited[id] = true;

    let currentLevel = 0;
    let levelFriends = [];

    while (queue.length > 0 && currentLevel < level) {
        let size = queue.length;
        currentLevel++;

        for (let i = 0; i < size; i++) {
            let person = queue.shift();
            for (let friend of friends[person]) {
                if (!visited[friend]) {
                    visited[friend] = true;
                    queue.push(friend);
                }
            }
        }
    }

    // At this point, `queue` contains all friends at the desired level
    levelFriends = queue;

    // Step 2: Count the frequency of videos watched by these friends
    let videoCount = new Map();

    for (let friend of levelFriends) {
        for (let video of watchedVideos[friend]) {
            videoCount.set(video, (videoCount.get(video) || 0) + 1);
        }
    }

    // Step 3: Sort videos first by frequency, then alphabetically
    let sortedVideos = Array.from(videoCount.keys()).sort((a, b) => {
        if (videoCount.get(a) === videoCount.get(b)) {
            return a.localeCompare(b); // Alphabetical order if frequency is the same
        } else {
            return videoCount.get(a) - videoCount.get(b); // Sort by frequency
        }
    });

    return sortedVideos;
};

```

***

### 1462. Course Schedule IV

Time O(N ^ 3)
Space O(N * N)

https://leetcode.com/problems/course-schedule-iv/description

```
/**
 * @param {number} numCourses
 * @param {number[][]} prerequisites
 * @param {number[][]} queries
 * @return {boolean[]}
 */
/*var checkIfPrerequisite = function (numCourses, prerequisites, queries) {
    var preReqMap = {};
    let answer = [];

    for (let i = 0; i < numCourses; i++) {
        preReqMap[i] = [];
    }

    for (let [a, b] of prerequisites) {
        if(!preReqMap[b]) preReqMap[b] = [];
        
        preReqMap[b].push(a);
    }


    let bfsTraversal = (vertex, target) => {
        let queue = [vertex];

        while (queue.length > 0) {
            let node = queue.pop();
            for (let neighbour of preReqMap[node]) {
                if (neighbour === target) return true;

                queue.push(neighbour);
            }
        }

        return false;
    }

    for (let i = 0; i < queries.length; i++) {
        answer.push(bfsTraversal(queries[i][1], queries[i][0]));
    }

    return answer;
};*/

var checkIfPrerequisite = function (numCourses, prerequisites, queries) {
    // Step 1: Create the adjacency matrix for the prerequisite graph
    let dp = Array.from({ length: numCourses }, () => Array(numCourses).fill(false));

    // Fill the adjacency matrix with direct prerequisites
    for (let [a, b] of prerequisites) {
        dp[a][b] = true; // a is a prerequisite of b
    }

    // Step 2: Use Floyd-Warshall to compute the transitive closure
    for (let k = 0; k < numCourses; k++) {
        for (let i = 0; i < numCourses; i++) {
            for (let j = 0; j < numCourses; j++) {
                if (dp[i][k] && dp[k][j]) {
                    dp[i][j] = true;
                }
            }
        }
    }

    // Step 3: Answer each query in constant time
    let answer = [];
    for (let [a, b] of queries) {
        answer.push(dp[a][b]);
    }

    return answer;
};

```
***

### 1466. Reorder Routes to Make All Paths Lead to the City Zero

<img width="341" alt="image" src="https://github.com/user-attachments/assets/f8f0a7b6-5d60-45da-9087-defe10175aa3">


```
/**
 * @param {number} n
 * @param {number[][]} connections
 * @return {number}
 */
var minReorder = function (n, connections) {
    let adjList = {};
    let reverseRoads = 0;
    let visited = Array(n).fill(false);

    for (let i = 0; i < n; i++) {
        adjList[i] = [];
    }

    // Step 1: Build a bidirectional graph
    for (let [a, b] of connections) {
        // Store forward and reverse roads
        adjList[a].push([b, 1]); // road goes from a to b, so 1 means road is directed away from 0
        adjList[b].push([a, 0]); // road goes from b to a (reverse connection), 0 means road is directed towards 0

    }

    // Step 2: DFS Traversal
    let dfs = (node) => {
        visited[node] = true;

        for (let [neighbor, isReversed] of adjList[node]) {
            if (!visited[neighbor]) {
                reverseRoads += isReversed;  // Count if the road is directed away from city 0
                dfs(neighbor);
            }
        }
    }

    // Step 3: Start DFS from city 0
    dfs(0);

    return reverseRoads;
};  
```
***

### 1557. Minimum Number of Vertices to Reach All Nodes

<img width="339" alt="image" src="https://github.com/user-attachments/assets/da25a14d-f2db-490e-a94b-bb5fb6a0cfd9">

```
/**
 * @param {number} n
 * @param {number[][]} edges
 * @return {number[]}
 */
var findSmallestSetOfVertices = function(n, edges) {
     let inDegree = new Array(n).fill(0); // Initialize an array to store in-degrees

    // Process the edges and calculate in-degrees for each node
    for (let [a, b] of edges) {
        inDegree[b]++;
    }

    let result = [];

    // Find nodes with in-degree of 0
    for (let i = 0; i < n; i++) {
        if (inDegree[i] === 0) {
            result.push(i);  // Only nodes with in-degree of 0 are required
        }
    }

    return result;
};
```
The time complexity of this function is O(n + m), where n is the number of nodes and m is the number of edges. This is because we iterate through all the edges to calculate the in-degrees of each node, which takes O(m) time. Then, we iterate through all the nodes to find the nodes with in-degree of 0, which takes O(n) time.

The space complexity of this function is O(n), where n is the number of nodes. This is because we create an array of size n to store the in-degrees of each node. Additionally, the space complexity of the result array is also O(n) in the worst case scenario where all nodes have an in-degree of 0.

***

### 1584. Min Cost to Connect All Points

<img width="341" alt="image" src="https://github.com/user-attachments/assets/9fd1ff22-56de-4af4-a6b2-64a78543f2d2">

```
/**
 * @param {number[][]} points
 * @return {number}
 */
class MinHeap {
    constructor() {
        this.heap = [];
    }

    push([cost, point]) {
        this.heap.push([cost, point]);
        this.bubbleUp(this.heap.length - 1);
    }

    pop() {
        if (this.heap.length === 1) return this.heap.pop();
        const top = this.heap[0];
        this.heap[0] = this.heap.pop();
        this.bubbleDown(0);
        return top;
    }

    bubbleUp(index) {
        while (index > 0) {
            const parentIndex = Math.floor((index - 1) / 2);
            if (this.heap[parentIndex][0] <= this.heap[index][0]) break;
            [this.heap[parentIndex], this.heap[index]] = [this.heap[index], this.heap[parentIndex]];
            index = parentIndex;
        }
    }

    bubbleDown(index) {
        const length = this.heap.length;
        while (true) {
            const left = 2 * index + 1;
            const right = 2 * index + 2;
            let smallest = index;

            if (left < length && this.heap[left][0] < this.heap[smallest][0]) {
                smallest = left;
            }
            if (right < length && this.heap[right][0] < this.heap[smallest][0]) {
                smallest = right;
            }
            if (smallest === index) break;

            [this.heap[smallest], this.heap[index]] = [this.heap[index], this.heap[smallest]];
            index = smallest;
        }
    }

    size() {
        return this.heap.length;
    }
}

var minCostConnectPoints = function(points) {
    let n = points.length;
    let visited = new Set();
    let minHeap = new MinHeap();
    minHeap.push([0, 0]); // [cost, point index]
    let totalCost = 0;

    while (visited.size < n) {
        let [cost, u] = minHeap.pop(); // Get the smallest cost edge
        if (visited.has(u)) continue; // Skip if already visited

        visited.add(u);
        totalCost += cost;

        // Explore all unvisited neighbors
        for (let v = 0; v < n; v++) {
            if (!visited.has(v)) {
                let distance = Math.abs(points[u][0] - points[v][0]) + Math.abs(points[u][1] - points[v][1]);
                minHeap.push([distance, v]);
            }
        }
    }

    return totalCost;
};

```
The time complexity of this algorithm is O(n^2 * log(n)), where n is the number of points. This is because for each point, we iterate through all other points to calculate the distance and push it into the min heap, which has a log(n) time complexity for insertion. Since we do this for each point, the overall time complexity becomes O(n^2 * log(n)).

The space complexity is O(n) for the visited set and O(n) for the min heap, resulting in a total space complexity of O(n). This is because we are storing the visited points and the distances in the min heap.

***

### 1615. Maximal Network Rank

<img width="347" alt="image" src="https://github.com/user-attachments/assets/92c7766f-a9b6-4781-a421-2ca30980e4f0">

```
/**
 * @param {number} n
 * @param {number[][]} roads
 * @return {number}
 */
var maximalNetworkRank = function (n, roads) {
    let adjList = {};

    for (let i = 0; i < n; i++) {
        adjList[i] = new Set();
    }

    for (let [a, b] of roads) {
        adjList[a].add(b);
        adjList[b].add(a);
    }

    let maximum = 0;

    for (let i = 0; i < n; i++) {
        for (let j = i + 1; j < n; j++) {
            let rank = adjList[i].size + adjList[j].size;
            if (adjList[i].has(j)) {
                rank--;
            }
            maximum = Math.max(maximum, rank);
        }
    }

    return maximum;
};
```
The time complexity of this solution is O(n^2) because we have two nested loops iterating over all pairs of nodes in the graph. 
The space complexity is O(n) because we are storing the adjacency list for each node in the graph.

***

### 1786. Number of Restricted Paths From First to Last Node

<img width="600" alt="image" src="https://github.com/user-attachments/assets/f12fa4ea-9240-42b2-9885-b0bfd41390e4">

```
/**
 * @param {number} n
 * @param {number[][]} edges
 * @return {number}
 */
var countRestrictedPaths = function(n, edges) {
    let adjList = Array.from({ length: n + 1 }, () => []);
    for (let [a, b, c] of edges) {
        adjList[a].push([b, c]);
        adjList[b].push([a, c]);
    }

    let distance = Array(n + 1).fill(Infinity);
    distance[n] = 0;

    let dijkstra = () => {
        let queue = new MinPriorityQueue({ priority: (x) => x[1] });
        queue.enqueue([n, 0]);

        while (queue.size()) {
            let [node, cost] = queue.dequeue().element;
            for (let [nextNode, weight] of adjList[node]) {
                let totalCost = cost + weight;
                if (distance[nextNode] > totalCost) {
                    distance[nextNode] = totalCost;
                    queue.enqueue([nextNode, totalCost]);
                }
            }
        }
    };

    dijkstra();

    const MOD = 1e9 + 7;

    let dp = new Array(n + 1).fill(-1);

    let dfs = (curr = 1, rCost = distance[1]) => {
        if (curr == n) return 1;
        if (dp[curr] != -1) return dp[curr];

        let resPaths = 0;

        for (let [node, weight] of adjList[curr]) {
            // Check if the neighbor node's distance is smaller, ensuring a restricted path
            if (distance[node] < rCost) {
                resPaths = (resPaths + dfs(node, distance[node])) % MOD;
            }
        }

        return dp[curr] = resPaths;
    };

    return dfs();
};

```
Time O(N log N)
Space O(N)

*** 

### 2039. The Time When the Network Becomes Idle

<img width="836" alt="image" src="https://github.com/user-attachments/assets/82ff22c0-8047-4e74-8877-b868757e631c">

<img width="732" alt="image" src="https://github.com/user-attachments/assets/3d602afc-12f8-4932-a6c2-94537df0a503">

<img width="559" alt="image" src="https://github.com/user-attachments/assets/5c4554a1-a18e-4564-bf23-36c4f4d4b4c6">

```

```

***

### 2101. Detonate the Maximum Bombs

<img width="375" alt="image" src="https://github.com/user-attachments/assets/f4eb4f49-003a-4d73-b44f-8ebd5bf8c58e">

```
/**
 * @param {number[][]} bombs
 * @return {number}
 */
var maximumDetonation = function (bombs) {
    let bombMap = new Map();

    for (let i = 0; i < bombs.length; i++) {
        bombMap.set(i, []); // Initialize each bomb with an empty array
        for (let j = 0; j < bombs.length; j++) {
            if (i == j) continue; // Skip if it's the same bomb

            let x1 = bombs[i];
            let x2 = bombs[j];

            // Check if bomb i can detonate bomb j
            if (canBombDetonate(x1[0], x1[1], x1[2], x2[0], x2[1])) {
                bombMap.get(i).push(j); // Add j to i's adjacency list
            }
        }
    }

    let max = 0;

    // BFS to find how many bombs can be detonated starting from each bomb
    let bfsTraversal = (bomb) => {
        let queue = [bomb];
        let visited = new Set([bomb]);

        while (queue.length > 0) {
            let node = queue.shift();
            for (let neighbour of bombMap.get(node)) {
                if (!visited.has(neighbour)) {
                    visited.add(neighbour);
                    queue.push(neighbour);
                }
            }
        }

        // Track the maximum number of detonations
        max = Math.max(max, visited.size);
    };

    // Run BFS for each bomb
    for (let i = 0; i < bombs.length; i++) {
        bfsTraversal(i);
    }

    return max;
};

// Function to check if bomb1 can detonate bomb2
function canBombDetonate(x1, y1, r1, x2, y2) {
    let distanceSquared = (x1 - x2) ** 2 + (y1 - y2) ** 2; // Euclidean distance squared
    return distanceSquared <= r1 ** 2; // Check if within the range of bomb1's detonation radius
}


function canBombDetonate(x1, y1, r1, x2, y2, r2) {
    let distance = (x1 - x2) ** 2 + (y1 - y2) ** 2;  // **2 refers to the power 6**2 is Math.pow(6, 2);
    let radius = r1 * r1;

    return (distance <= radius);
}
```
Time:  O(N * N)
Space: O(N)
***


### 2115. Find All Possible Recipes from Given Supplies

<img width="373" alt="image" src="https://github.com/user-attachments/assets/50568286-f66a-49f5-8b7f-3e2ea3dd9930">

```
/**
 * @param {string[]} recipes
 * @param {string[][]} ingredients
 * @param {string[]} supplies
 * @return {string[]}
 */
var findAllRecipes = function (recipes, ingredients, supplies) {
    let suppliesSet = new Set(supplies);
    let answer = new Set();
    let found = true;
    while (found) {
        found = false;
        for (let i = 0; i < recipes.length; i++) {
            if(answer.has(recipes[i])) continue;

            let totalIngredients = ingredients[i].length;
            let ingFound = 0;
            for (let j = 0; j < totalIngredients; j++) {
                if (suppliesSet.has(ingredients[i][j]) || answer.has(ingredients[i][j])) {
                    ingFound++;
                }
            }

            if (ingFound == totalIngredients) {
                answer.add(recipes[i]);
                suppliesSet.add(recipes[i]); // Add the recipe to the supplier set for future reference
                found = true;
            }
        }
    }

    return [...answer];
};
```
The time complexity of this solution is O(n*m), where n is the number of recipes and m is the average number of ingredients in each recipe. This is because we iterate through all the recipes and for each recipe, we iterate through its ingredients to check if they are in the supplies set or the answer set.

The space complexity is O(n), where n is the number of recipes. This is because we use a set to store the answer, which can potentially store all the recipes.

Overall, this solution is efficient as it iterates through each recipe and its ingredients only once, and uses a set to store the answer for quick lookups.

***

### 2285. Maximum Total Importance of Roads

<img width="528" alt="image" src="https://github.com/user-attachments/assets/394dc8aa-6f09-4b09-8886-7ce54603dd8f">

```
/**
 * @param {number} n
 * @param {number[][]} roads
 * @return {number}
 */
var maximumImportance = function (n, roads) {
    // Step 1: Initialize degree array
    let degrees = new Array(n).fill(0);

    // Step 2: Count the degree of each node
    for (let [a, b] of roads) {
        degrees[a]++;
        degrees[b]++;
    }

    // Step 3: Sort the degree array indices by the degree values in descending order
    let sortedNodes = [...Array(n).keys()].sort((a, b) => degrees[b] - degrees[a]);

    // Step 4: Assign importance values (highest to lowest)
    let importance = new Array(n);
    for (let i = 0; i < n; i++) {
        importance[sortedNodes[i]] = n - i; // Assign importance based on sorted order
    }

    // Step 5: Calculate the total sum of importance for the roads
    let sum = 0;
    for (let [a, b] of roads) {
        sum += importance[a] + importance[b];
    }

    return sum;
};
```
The time complexity of this solution is O(n log n) because the sorting step in Step 3 takes O(n log n) time. The space complexity is O(n) because we are using additional arrays of size n to store the degrees, sorted nodes, and importance values.

***


### 2316. Count Unreachable Pairs of Nodes in an Undirected Graph

<img width="492" alt="image" src="https://github.com/user-attachments/assets/1fc6d4a3-0d37-4ec9-8bd2-b9700776c98b">


```
var countPairs = function (n, edges) {
    let uf = new UnionFind(n);

    // Union the nodes based on edges
    for (let [a, b] of edges) {
        uf.union(a, b);
    }

    // Count the size of each connected component
    let componentSizes = new Map();
    for (let i = 0; i < n; i++) {
        let root = uf.find(i);
        if (!componentSizes.has(root)) {
            componentSizes.set(root, uf.getSize(i));
        }
    }

    // Calculate the total number of pairs
    let totalPairs = Math.floor((n * (n - 1)) / 2);

    // Subtract the pairs within each connected component
    let internalPairs = 0;
    for (let size of componentSizes.values()) {
        internalPairs += Math.floor((size * (size - 1)) / 2);
    }

    return totalPairs - internalPairs;
};

class UnionFind {
    constructor(size) {
        this.parent = Array(size).fill(0).map((_, i) => i);
        this.rank = Array(size).fill(1);
        this.componentSize = Array(size).fill(1);
    }

    find(node) {
        if (this.parent[node] !== node) {
            this.parent[node] = this.find(this.parent[node]);  // Path compression
        }
        return this.parent[node];
    }

    union(node1, node2) {
        const root1 = this.find(node1);
        const root2 = this.find(node2);

        if (root1 !== root2) {
            // Union by rank/size
            if (this.rank[root1] > this.rank[root2]) {
                this.parent[root2] = root1;
                this.componentSize[root1] += this.componentSize[root2];
            } else if (this.rank[root1] < this.rank[root2]) {
                this.parent[root1] = root2;
                this.componentSize[root2] += this.componentSize[root1];
            } else {
                this.parent[root2] = root1;
                this.rank[root1]++;
                this.componentSize[root1] += this.componentSize[root2];
            }
        }
    }

    getSize(node) {
        return this.componentSize[this.find(node)];
    }
}

```
The time complexity of this solution is O(n + mα(n)), where n is the number of nodes and m is the number of edges. The UnionFind operations have an amortized time complexity of α(n), where α(n) is the inverse Ackermann function, which grows very slowly and is considered to be almost constant. Therefore, the overall time complexity is dominated by the loop that calculates the size of each connected component, which is O(n).

The space complexity of this solution is O(n), where n is the number of nodes. This is because we are using a UnionFind data structure to keep track of the connected components, which requires O(n) space. Additionally, we are using a map to store the sizes of each connected component, which also requires O(n) space.

***

### 2359. Find Closest Node to Given Two Nodes


```
/**
 * @param {number[]} edges
 * @param {number} node1
 * @param {number} node2
 * @return {number}
 */
var closestMeetingNode = function(edges, node1, node2) {
    const n = edges.length;
    
    // Function to perform BFS/DFS and calculate distances
    const bfs = (start) => {
        const dist = new Array(n).fill(Infinity); // Initialize distances to infinity
        let distance = 0;
        let current = start;

        while (current !== -1 && dist[current] === Infinity) {
            dist[current] = distance++;
            current = edges[current]; // Move to the next node via the edge
        }

        return dist;
    };

    // Get distances from node1 and node2
    const dist1 = bfs(node1);
    const dist2 = bfs(node2);

    let result = -1;
    let minDistance = Infinity;

    // Compare distances for all nodes
    for (let i = 0; i < n; i++) {
        // We need to ensure that both nodes can reach the current node
        if (dist1[i] !== Infinity && dist2[i] !== Infinity) {
            // Take the maximum distance for the current node
            const maxDist = Math.max(dist1[i], dist2[i]);

            // We want to minimize the maximum distance
            if (maxDist < minDistance) {
                minDistance = maxDist;
                result = i; // Update the result to the node with the smaller maximum distance
            }
        }
    }

    return result;
};
```

***

### 2368. Reachable Nodes With Restrictions

<img width="417" alt="image" src="https://github.com/user-attachments/assets/94ffc953-b170-4460-b9c1-de9b76212985">

```
/**
 * @param {number} n
 * @param {number[][]} edges
 * @param {number[]} restricted
 * @return {number}
 */
var reachableNodes = function (n, edges, restricted) {

    let adjList = new Map();
    let restrictedSet = new Set(restricted);

    for (let [a, b] of edges) {
        if (!adjList.has(a)) adjList.set(a, []);
        if (!adjList.has(b)) adjList.set(b, []);

        adjList.get(a).push(b);
        adjList.get(b).push(a);
    }

    let visited = new Set();
    let queue = [0];

    while (queue.length > 0) {
        let vertex = queue.pop();

        if (restrictedSet.has(vertex) || visited.has(vertex)) continue;

        visited.add(vertex);
        for (let neighbour of adjList.get(vertex) || []) {
            if (!visited.has(neighbour)) {
                queue.push(neighbour);
            }
        }
    }

    return visited.size;
};

```

The time complexity of this solution is O(n + m), where n is the number of nodes and m is the number of edges in the graph. This is because we are using a breadth-first search algorithm to traverse the graph, which visits each node and each edge once.

The space complexity is O(n), where n is the number of nodes in the graph. This is because we are using sets and queues to keep track of visited nodes and nodes to visit, which can potentially store all nodes in the graph.

***

### 2374. Node With Highest Edge Score

<img width="415" alt="image" src="https://github.com/user-attachments/assets/1d826f73-f4dd-4b86-ac46-091b42aef322">

```
`/**
 * @param {number[]} edges
 * @return {number}
 */
var edgeScore = function (edges) {
    let inDegree = new Array(edges.length).fill(0); // Array for storing edge scores
    let node = 0;  // To track the node with the highest score

    // Calculate the edge score for each node
    for (let label = 0; label < edges.length; label++) {
        inDegree[edges[label]] += label;
    }

    // Find the node with the maximum edge score (with smallest index if tied)
    for (let label = 1; label < edges.length; label++) {
        if (inDegree[label] > inDegree[node] || (inDegree[label] === inDegree[node] && label < node)) {
            node = label;
        }
    }

    return node;
};
```
The time complexity of this function is O(n), where n is the number of edges in the input array. This is because the function iterates through the edges array twice, once to calculate the edge scores and once to find the node with the maximum edge score.

The space complexity of this function is O(n), where n is the number of edges in the input array. This is because the function creates an array of size n to store the edge scores for each node.

***

### 2467. Most Profitable Path in a Tree

<img width="464" alt="image" src="https://github.com/user-attachments/assets/987ccf48-58e4-46f4-afbe-ea17643b8550">

<img width="446" alt="image" src="https://github.com/user-attachments/assets/45bcb0c8-1cf6-4e4d-bd4b-76a3071338fe">


```
var mostProfitablePath = function (edges, bob, amount) {
    let adjList = Array.from({ length: edges.length + 1 }, () => []);

    for (let [i, j] of edges)
        adjList[i].push(j), adjList[j].push(i);

    function alicePath(node, parent, time) {
        let totalBobTime = node == bob ? 0 : Infinity, newScore = -Infinity;

        for (const child of adjList[node]) {
            if (child == parent) continue;

            const [score, bobTime] = alicePath(child, node, time + 1);
            totalBobTime = Math.min(totalBobTime, bobTime + 1);
            newScore = Math.max(newScore, score)
        }

        if (newScore == -Infinity) newScore = 0;
        if (time < totalBobTime) newScore += amount[node];
        else if (time == totalBobTime) newScore += amount[node] / 2;

        return [newScore, totalBobTime];
    }

    return alicePath(0, -1, 0)[0];
};
```
The time complexity of this function is O(n), where n is the number of edges in the input. This is because the function performs a depth-first search traversal of the graph represented by the edges, visiting each node and its adjacent nodes exactly once.

The space complexity of this function is also O(n), as it uses an adjacency list to represent the graph, which requires O(n) space to store the edges. Additionally, the recursive calls in the `alicePath` function also contribute to the space complexity, but since the maximum depth of recursion is limited by the number of nodes in the graph, the overall space complexity remains O(n).

***

### 2477. Minimum Fuel Cost to Report to the Capital 

<img width="373" alt="image" src="https://github.com/user-attachments/assets/634cdef0-a9e1-4fd8-a564-f7a7cb7adf63">

```
/**
 * @param {number[][]} roads
 * @param {number} seats
 * @return {number}
 */
var minimumFuelCost = function (roads, seats) {
    if (roads.length == 0) return roads.length;

    let adjList = new Map();
    let fuel = 0;

    for (let [a, b] of roads) {
        if (!adjList.has(a)) adjList.set(a, []);
        if (!adjList.has(b)) adjList.set(b, []);

        adjList.get(a).push(b);
        adjList.get(b).push(a);
    }

    let visited = new Set();

    let DFSTraversal = (vertex) => {
        visited.add(vertex);
        let people = 1;

        for (let neighbour of adjList.get(vertex) || []) {
            if (!visited.has(neighbour)) {
                let subTreePeople = DFSTraversal(neighbour);
                fuel += Math.ceil(subTreePeople / seats);
                people += subTreePeople;
            }
        }

        return people;
    }

    DFSTraversal(0);
    return fuel;

};
```
The time complexity of this solution is O(n), where n is the number of roads in the input. This is because the solution performs a depth-first traversal of the graph represented by the roads, visiting each node only once.

The space complexity of this solution is also O(n), where n is the number of roads in the input. This is because the solution uses a map to represent the adjacency list of the graph, a set to keep track of visited nodes, and recursive function calls for the depth-first traversal. The space complexity is linear with respect to the number of roads in the input.

***

###  2492. Minimum Score of a Path Between Two Cities

<img width="529" alt="image" src="https://github.com/user-attachments/assets/0e5cd159-d043-4ac0-97c4-a1ac0916bfee">

```
/**
 * @param {number} n
 * @param {number[][]} roads
 * @return {number}
 */
var minScore = function (n, roads) {
    let adjList = new Map();

    for (let [a, b, c] of roads) {
        if (!adjList.has(a)) adjList.set(a, []);
        if (!adjList.has(b)) adjList.set(b, []);

        adjList.get(a).push([b, c]);
        adjList.get(b).push([a, c]);
    }

    let minDist = Infinity;

    let queue = [1];
    let visited = new Set([1]);
    let front = 0;

    while (front < queue.length) {
        let node = queue[front++];
        // front++;
        for (let [neighbour, distance] of adjList.get(node) || []) {
            minDist = Math.min(minDist, distance);
            if (!visited.has(neighbour)) {
                queue.push(neighbour);
                visited.add(neighbour);
            }

            if (minDist == 1) return 1;
        }
    }

    return minDist;
};  
```
The time complexity of this function is O(n + m), where n is the number of nodes and m is the number of edges in the graph represented by the roads array. This is because we are iterating through all nodes and edges in the graph to build the adjacency list and perform the BFS traversal.

The space complexity is O(n + m) as well, where n is the number of nodes and m is the number of edges in the graph. This is because we are storing the adjacency list, queue, visited set, and other variables that grow linearly with the number of nodes and edges in the graph
***

### 2497. Maximum Star Sum of a Graph

<img width="493" alt="image" src="https://github.com/user-attachments/assets/2bd0790c-b25a-46a5-b38f-a56060ed7756">

<img width="488" alt="image" src="https://github.com/user-attachments/assets/f29c14b8-d8ae-4eae-b1c1-94b1a4aae284">


```
/**
 * @param {number[]} vals
 * @param {number[][]} edges
 * @param {number} k
 * @return {number}
 */
var maxStarSum = function (vals, edges, k) {
    let maxSum = -Infinity;

    let adjList = new Map();

    for (let [a, b] of edges) {
        if (!adjList.has(a)) adjList.set(a, []);
        if (!adjList.has(b)) adjList.set(b, []);

        adjList.get(a).push(vals[b]);
        adjList.get(b).push(vals[a]);
    }

    for (let i = 0; i < vals.length; i++) {
        let neighbours = adjList.get(i) || [];

        neighbours.sort((a, b) => b - a);
        let sum = vals[i];

        for (let j = 0; j < Math.min(k, neighbours.length); j++) {
            if (neighbours[j] > 0) sum += neighbours[j];
        }

        maxSum = Math.max(sum, maxSum);
    }

    return maxSum;
};
```
The time complexity of this function is O(nlogn), where n is the number of nodes in the graph. This is because we iterate through each node in the graph and sort its neighbors in descending order, which takes O(logn) time for each node.

The space complexity is O(n), where n is the number of nodes in the graph. This is because we use a map to store the adjacency list of the graph, which takes up O(n) space.

***

### 2662. Minimum Cost of a Path With Special Roads

<img width="377" alt="image" src="https://github.com/user-attachments/assets/3a23c042-ce93-404e-bc89-7788464f34dc">

```
 /**
 * @param {number[]} start - [startX, startY]
 * @param {number[]} target - [targetX, targetY]
 * @param {number[][]} specialRoads - [[x1i, y1i, x2i, y2i, costi], ...]
 * @return {number}
 */
var minimumCost = function(start, target, specialRoads) {
    // Helper function to compute Manhattan distance
    const manhattan = (x1, y1, x2, y2) => Math.abs(x2 - x1) + Math.abs(y2 - y1);
    
    // Step 1: Collect all key points
    const points = [];
    const pointMap = new Map(); // To assign unique indices
    const addPoint = (x, y) => {
        const key = `${x},${y}`;
        if (!pointMap.has(key)) {
            pointMap.set(key, points.length);
            points.push([x, y]);
        }
        return pointMap.get(key);
    };
    
    // Add start and target
    const startIdx = addPoint(start[0], start[1]);
    const targetIdx = addPoint(target[0], target[1]);
    
    // Add all special road endpoints
    for (const road of specialRoads) {
        const [x1, y1, x2, y2, cost] = road;
        addPoint(x1, y1);
        addPoint(x2, y2);
    }
    
    const n = points.length;
    
    // Step 2: Build adjacency list
    const adjList = Array.from({ length: n }, () => []);
    
    // Add regular edges (Manhattan distance between all pairs)
    // To optimize, we only add edges that are relevant, such as start, target, and special road points.
    // Connecting every pair would be O(n^2), which is impractical for large n.
    // Instead, we'll consider edges from each point to all other points via regular movement.
    // This can be optimized further based on problem constraints.

    // To prevent O(n^2) complexity, we'll only connect nodes as needed during Dijkstra's traversal.
    // Thus, we'll skip adding regular edges upfront and compute them on the fly.

    // Step 3: Add special road edges
    for (const road of specialRoads) {
        const [x1, y1, x2, y2, cost] = road;
        const fromKey = `${x1},${y1}`;
        const toKey = `${x2},${y2}`;
        const fromIdx = pointMap.get(fromKey);
        const toIdx = pointMap.get(toKey);
        adjList[fromIdx].push({ node: toIdx, cost: cost });
    }
    
    // Step 4: Dijkstra's Algorithm Implementation
    // Initialize distance array
    const dist = Array(n).fill(Infinity);
    dist[startIdx] = 0;
    
    // Priority queue implemented as a min-heap
    const heap = new MinHeap();
    heap.insert({ node: startIdx, cost: 0 });
    
    while (!heap.isEmpty()) {
        const { node, cost } = heap.extractMin();
        
        if (node === targetIdx) {
            return cost; // Found the shortest path to target
        }
        
        // If we have already found a better path before
        if (cost > dist[node]) continue;
        
        // Explore neighbors via special roads
        for (const edge of adjList[node]) {
            const neighbor = edge.node;
            const newCost = cost + edge.cost;
            if (newCost < dist[neighbor]) {
                dist[neighbor] = newCost;
                heap.insert({ node: neighbor, cost: newCost });
            }
        }
        
        // Explore neighbors via regular movement
        for (let i = 0; i < n; i++) {
            if (i === node) continue; // Skip self
            const moveCost = manhattan(...points[node], ...points[i]);
            const newCost = cost + moveCost;
            if (newCost < dist[i]) {
                dist[i] = newCost;
                heap.insert({ node: i, cost: newCost });
            }
        }
    }
    
    // If target is unreachable
    return -1;
};

// MinHeap Implementation
class MinHeap {
    constructor() {
        this.heap = [];
    }
    
    insert(item) {
        this.heap.push(item);
        this.bubbleUp(this.heap.length - 1);
    }
    
    extractMin() {
        if (this.heap.length === 0) return null;
        if (this.heap.length === 1) return this.heap.pop();
        const min = this.heap[0];
        this.heap[0] = this.heap.pop();
        this.bubbleDown(0);
        return min;
    }
    
    isEmpty() {
        return this.heap.length === 0;
    }
    
    bubbleUp(index) {
        while (index > 0) {
            let parent = Math.floor((index - 1) / 2);
            if (this.heap[parent].cost <= this.heap[index].cost) break;
            [this.heap[parent], this.heap[index]] = [this.heap[index], this.heap[parent]];
            index = parent;
        }
    }
    
    bubbleDown(index) {
        const length = this.heap.length;
        while (true) {
            let smallest = index;
            let left = 2 * index + 1;
            let right = 2 * index + 2;
            
            if (left < length && this.heap[left].cost < this.heap[smallest].cost) {
                smallest = left;
            }
            if (right < length && this.heap[right].cost < this.heap[smallest].cost) {
                smallest = right;
            }
            if (smallest === index) break;
            [this.heap[smallest], this.heap[index]] = [this.heap[index], this.heap[smallest]];
            index = smallest;
        }
    }
}

```
Tine: O(N)
Space O(N)
***

### 2685. Count the Number of Complete Components

<img width="387" alt="image" src="https://github.com/user-attachments/assets/3715b21e-342b-4b07-a4fd-508d2058aaca">

```
/**
 * @param {number} n
 * @param {number[][]} edges
 * @return {number}
 */
var countCompleteComponents = function (n, edges) {
    let connComp = 0;
    let adjList = new Map();

    for (let [a, b] of edges) {
        if (!adjList.has(a)) adjList.set(a, []);

        if (!adjList.has(b)) adjList.set(b, []);

        adjList.get(a).push(b);
        adjList.get(b).push(a);
    }

    let visited = new Set();

    let bfsTraversal = (vertex) => {
        let queue = [vertex];
        visited.add(vertex);
        let nodes = 1, edgesCount = 0;
        while (queue.length > 0) {
            let node = queue.shift();

            for (let neighbour of adjList.get(node) || []) {
                edgesCount += 1;
                if (!visited.has(neighbour)) {
                    visited.add(neighbour);
                    queue.push(neighbour);
                    nodes += 1;
                }
            }
        }

        edgesCount /= 2;

        if (edgesCount == (nodes * (nodes - 1)) / 2) {
            connComp += 1;
        }
    }

    for (let i = 0; i < n; i++) {
        if (!visited.has(i)) bfsTraversal(i);
    }

    return connComp;
};
```
Time complexity: O(n + m), where n is the number of nodes and m is the number of edges in the graph. This is because we are performing a BFS traversal on each connected component in the graph, which requires visiting each node and each edge once.

Space complexity: O(n + m), where n is the number of nodes and m is the number of edges in the graph. This is because we are using a map to store the adjacency list of the graph, a set to store visited nodes, and a queue for BFS traversal, all of which can potentially store all nodes and edges in the graph.

***

### 2924. Find Champion II

<img width="376" alt="image" src="https://github.com/user-attachments/assets/2afee836-49bc-40a8-860f-4f2cb5f0c7db">

<img width="381" alt="image" src="https://github.com/user-attachments/assets/93f0639e-ffcc-45ac-a359-7e04e93ce8c6">

```
/**
 * @param {number} n
 * @param {number[][]} edges
 * @return {number}
 */
var findChampion = function(n, edges) {
    let champion = -1;
    let adjList = new Map();

    for(let i = 0; i < n; i++) {
        adjList.set(i, []);
    }

    for(let [a, b] of edges) {
        adjList.get(b).push(a);
    }

    for(let i = 0; i < n; i++) {
        if(adjList.get(i).length == 0) {
            if(champion != -1) return -1;

            champion = i;
        }
    }

    return champion;
};
```
Time complexity:
The time complexity of this solution is O(n) where n is the number of nodes in the graph. This is because we iterate through all the nodes in the graph to check for the champion node.
Space complexity:
The space complexity is also O(n) because we are storing the adjacency list of the graph in a Map data structure, which can have at most n entries (one for each node).
***

### 2976. Minimum Cost to Convert String I

<img width="384" alt="image" src="https://github.com/user-attachments/assets/769de51d-dd1b-41f2-b728-c1d6c43eaba9">

```
/**
 * @param {string} source
 * @param {string} target
 * @param {character[]} original
 * @param {character[]} changed
 * @param {number[]} cost
 * @return {number}
 */
var minimumCost = function (source, target, original, changed, cost) {
    // Edge case: If source and target are the same, no cost is needed
    if (source === target) return 0;

    // Initialize distance matrix with Infinity
    const V = 26; // Number of lowercase English letters
    const INF = Number.MAX_SAFE_INTEGER;
    let dist = Array.from({ length: V }, () => Array(V).fill(INF));

    // Set distance from each character to itself as 0
    for (let i = 0; i < V; i++) {
        dist[i][i] = 0;
    }

    // Build the initial conversion map based on the given transformations
    for (let i = 0; i < original.length; i++) {
        const from = original[i].charCodeAt(0) - 97; // 'a' -> 0, 'b' -> 1, ..., 'z' -> 25
        const to = changed[i].charCodeAt(0) - 97;
        const c = cost[i];

        // If multiple transformations exist, keep the minimum cost
        if (c < dist[from][to]) {
            dist[from][to] = c;
        }
    }

    // Apply Floyd-Warshall to compute all-pairs minimum cost
    for (let k = 0; k < V; k++) {
        for (let i = 0; i < V; i++) {
            for (let j = 0; j < V; j++) {
                if (dist[i][k] !== INF && dist[k][j] !== INF) {
                    if (dist[i][j] > dist[i][k] + dist[k][j]) {
                        dist[i][j] = dist[i][k] + dist[k][j];
                    }
                }
            }
        }
    }

    let totalMinCost = 0;

    // Iterate through each character in the source and target strings
    for (let i = 0; i < source.length; i++) {
        const srcChar = source[i];
        const tgtChar = target[i];

        // If characters are the same, no cost is needed
        if (srcChar === tgtChar) continue;

        const srcIdx = srcChar.charCodeAt(0) - 97;
        const tgtIdx = tgtChar.charCodeAt(0) - 97;

        // If there's no path to transform srcChar to tgtChar, return -1
        if (dist[srcIdx][tgtIdx] === INF) {
            return -1;
        }

        // Accumulate the minimum cost
        totalMinCost += dist[srcIdx][tgtIdx];
    }

    return totalMinCost;
};
```

***

### 3015. Count the Number of Houses at a Certain Distance I

<img width="382" alt="image" src="https://github.com/user-attachments/assets/23b0c2a8-c5b4-40ee-a5bd-9e17ba10c0d6">

```
/**
 * @param {number} n
 * @param {number} x
 * @param {number} y
 * @return {number[]}
 */
var countOfPairs = function (n, x, y) {
    const result = new Array(n).fill(0);

    for (let i = 1; i <= n; i++) {
        for (let j = i + 1; j <= n; j++) {
            const distance = Math.min(
                Math.abs(i - j),
                Math.abs(i - x) + Math.abs(j - y) + 1,
                Math.abs(i - y) + Math.abs(j - x) + 1
            );
            result[distance - 1]++;
        }
    }

    return result.map((count, index) => count * 2);
};
```
Time complexity: O(N ^2)
Space complexity: O(N)
***























## Hard

### 127. Word Ladder

Time complexity:O(N^2 * M)
    N -No of Words in the List
    M is No, of characters in each word
Space complexity:
    O(N) - Using Queue and Visisted Set
```
/**
 * @param {string} beginWord
 * @param {string} endWord
 * @param {string[]} wordList
 * @return {number}
 */
var ladderLength = function (beginWord, endWord, wordList) {
    if (wordList.indexOf(endWord) == -1) return 0;

    let visited = new Set();
    let queue = [beginWord];
    let length = 0;
    let wordSet = new Set(wordList);

    while (queue.length > 0) { // BFS Loop through all the elements in the Queue;
        let size = queue.length;
        length++;

        for (let i = 0; i < size; i++) {
            let current = queue.shift(); // Get the first Element in the queue

            for (let j = 0; j < current.length; j++) { // Check each Character in the queue item and compare each values

                let temp = current.split("");
                // comapre each values by changing each charater bit from 'a' to 'z' and check with the wordList
                for (let char = 97; char <= 122; char++) {
                    temp[j] = String.fromCharCode(char);

                    let newWord = temp.join("");
                    if (newWord == endWord) { // if the newWord is the endWord return
                        return length + 1;
                    }

                    // if the word is in WordList and not Visited then add it to the queue and visted Set
                    if (wordSet.has(newWord) && !visited.has(newWord)) {
                        queue.push(newWord);
                        visited.add(newWord);
                    }
                }
            }
        }
    }

    return 0;
};

```

[![YT Video](https://img.youtube.com/vi/2odLxQWYDi0/0.jpg)](https://www.youtube.com/watch?v=2odLxQWYDi0)

*** 

126. Word Ladder II

```

```

***

### 827. Making A Large Island

```

```

[![YT Video](https://img.youtube.com/vi/lgiz0Oup6gM/0.jpg)](https://www.youtube.com/watch?v=lgiz0Oup6gM)

***


### 778. Swim in Rising Water

Time and Space Complexity : O(N * N)

```
/**
 * @param {number[][]} grid
 * @return {number}
 */
var swimInWater = function (grid) {
    let n = grid.length;
    let minGrid = new Array(n).fill().map(() => Array(n).fill(Number.MAX_SAFE_INTEGER));// construct the N * N Grdi and default it with Max Num
    let dir = [[-1, 0], [1, 0], [0, 1], [0, -1]]; //All four Directions
    minGrid[0][0] = grid[0][0];

    let queue = [[0, 0]];

    while (queue.length > 0) {
        let [x, y] = queue.shift(); // Pop first element
        for (let [dx, dy] of dir) { // loop through all the elements
            let x1 = x + dx;
            let y1 = y + dy;

            if (x1 < 0 || x1 >= n || y1 >= n || y1 < 0) continue; // Check the Grid boundary

            // If there is a min passed value in grid check that with the minGrid
            // If there is a min value accept it and assign it to the minGrid
            if (Math.max(grid[x1][y1], minGrid[x][y]) < minGrid[x1][y1]) {

                minGrid[x1][y1] = Math.max(grid[x1][y1], minGrid[x][y]);
                queue.push([x1, y1]);
            }
        }
    }

    return minGrid[n - 1][n - 1];
}; 
```

***

### 1520. Maximum Number of Non-Overlapping Substrings

```

```

***
