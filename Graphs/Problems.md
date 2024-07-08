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

