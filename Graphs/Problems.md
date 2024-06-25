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

## 207. Course Schedule

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

