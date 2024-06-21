# Graph Problems

## Easy

T.C = O(1) 
S.T = O(1)
1. 1791. Find Center of Star Graph

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
