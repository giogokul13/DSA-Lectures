# Easy Problems

## 1. 94. Binary Tree Inorder Traversal

### Solution 1
Time - O(n)
Space -  O(n)

```
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var inorderTraversal = function (root) {
    let answer = [];

    function inOrder(root) {
        if (root) {
            inOrder(root.left);
            answer.push(root.val);
            inOrder(root.right);
        }
    }

    inOrder(root);

    return answer;
};
```

### Solution 2
Time - O(n)
Space -  O(n)

```
var inorderTraversal = function (root) {
    let stack = [], result = [];

    while(root || stack.length){
        if(root){
            stack.push(root);
            root = root.left;
        } else {
            root = stack.pop();
            result.push(root.val);
            root = root.right;
        }
    }

    return result;
};
```

***


## 2. 100. Same Tree
Time - O(n)
Space - O(h) where h is the height of the tree, all the function callas are stored in the Stack.

```
/**
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {boolean}
 */
var isSameTree = function (p, q) {
    
    if(!p && !q) return true;

    if(!p || !q) return false;

    if(p.val !== q.val) return false;

    return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);

};
```

***

## 3. 101. Symmetric Tree
Time - O(n)
Space - O(h) where h is the height of the tree, all the function callas are stored in the Stack.


```
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
var isSymmetric = function (root) {

    function checkSymetric(left, right) {
        if (!left && !right) return true;

        if (!left || !right) return false


        if (left.val != right.val) return false;

        if (!checkSymetric(left.left, right.right))
            return false;
        if (!checkSymetric(left.right, right.left))
            return false;
        return true;

    }

    return checkSymetric(root.left, root.right)
};
```

***


## 4. 104. Maximum Depth of Binary Tree
Time - O(n)
Space - O(h) h, height of the tree in Stack.

```
/**
 * @param {TreeNode} root
 * @return {number}
 */
var maxDepth = function(root) {
    
    if(!root) return 0;
    

    return Math.max(maxDepth(root.right), maxDepth(root.left)) + 1;
};
```

***

## 5. 108. Convert Sorted Array to Binary Search Tree
Time - O(n)
Space - O(n) we are creating a new TreeNode for each element in the input array, and the recursion stack can grow up to O(n) in the worst case scenario.

```
/**
 * @param {number[]} nums
 * @return {TreeNode}
 */
var sortedArrayToBST = function (nums) {

    let constructNodes = function (left, right) {
        if (left > right) return null;

        let middle = Math.floor((left + right) / 2);
        let tree = new TreeNode(nums[middle]);
        tree.left = constructNodes(left, middle - 1);
        tree.right = constructNodes(middle + 1, right);

        return tree;
    }

    return constructNodes(0, nums.length - 1);

};
```
### Video Reference
[![YT Video](https://img.youtube.com/vi/0K0uCMYq5ng/0.jpg)](https://www.youtube.com/watch?v=0K0uCMYq5ng)

***

## 6. 110. Balanced Binary Tree

* Solution 1

Time - O(n)
Space - O(n)


```
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
var isBalanced = function (root) {
    return dfs(root)[0];

};

function dfs(root) {
    if (!root) return [true, 0]; // Base condition for no root or only one root.

    let [left, right] = [dfs(root.left), dfs(root.right)];
    let isBalanced = left[0] && right[0] && Math.abs(left[1] - right[1]) <= 1;

    return [isBalanced, ( 1 + Math.max(left[1], right[1]))];
}
```

* Solution 2
    
Time O(N) space O(H)

```

/**
 * @param {TreeNode} root
 * @return {boolean}
 */
var isBalanced = function (root) {
    return (postOrderTraverse(root) !== -1);
};

let postOrderTraverse = (node) => {
    if (!node) return 0;

    let leftHeight = postOrderTraverse(node.left);

    if(leftHeight == -1) return -1;

    let rightHeight = postOrderTraverse(node.right);

    if(rightHeight == -1) return -1;

    if (Math.abs(leftHeight - rightHeight) > 1) return -1;

    return Math.max(leftHeight, rightHeight) + 1;
}
```


***


### Video reference 
[![YT Video](https://img.youtube.com/vi/QfJsau0ItOY/0.jpg)](https://www.youtube.com/watch?v=QfJsau0ItOY)

***

## 7. 111. Minimum Depth of Binary Tree
Time - O(n)
Space - O(n)

```
/**
 * @param {TreeNode} root
 * @return {number}
 */
var minDepth = function (root) {
    if (!root) return 0;

    let depth = 1;

    let queue = [];
    queue.push(root);
     while (queue.length) {
        let levelSize = queue.length; // Number of nodes at the current level

        for (let i = 0; i < levelSize; i++) {
            let curr = queue.shift();

            // Check if we have reached a leaf node
            if (!curr.left && !curr.right) return depth;

            if (curr.left) {
                queue.push(curr.left);
            }
            if (curr.right) {
                queue.push(curr.right);
            }
        }

        depth++; // Increment depth after processing all nodes at the current level
    }

    return depth;
};
```
### Video reference 
[![YT Video](https://img.youtube.com/vi/tZS4VHtbYoo/0.jpg)](https://www.youtube.com/watch?v=tZS4VHtbYoo)

***

## 8. 144. Binary Tree Preorder Traversal
Time - O(n)
Space - O(n)

```
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var preorderTraversal = function (root) {
    if (!root) return [];

    let nodes = [];

    let preOrder = function (root) {
        if (root) {
            nodes.push(root.val);
            preOrder(root.left);
            preOrder(root.right);
        }

        return nodes;
    }

    return preOrder(root);
};
```

***

## 9. 145. Binary Tree Postorder Traversal
Time - O(n)
Space - O(n)

```
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var postorderTraversal = function (root) {

    let nodes = [];

    if (!root) return nodes;

    let postTraverse = function (root) {
        if (root) {
            postTraverse(root.left);
            postTraverse(root.right);

            nodes.push(root.val);
        }

        return nodes;
    }

    return postTraverse(root);
};
```

***


## 10. 112. Path Sum
Time - O(n)
Space - O(n)

```
/**
 * @param {TreeNode} root
 * @param {number} targetSum
 * @return {boolean}
 */
var hasPathSum = function (root, targetSum) {

    if (!root) return false; // when no nodes present

    // check leaf nodes && current value is TargetSum :: success we found the sum
    if(root.val == targetSum && (!root.left && !root.right)) return true; 

    return hasPathSum(root.left, targetSum - root.val) || hasPathSum(root.right, targetSum - root.val);

}
```
### Video reference 
[![YT Video](https://img.youtube.com/vi/_FVbQCXeGy8/0.jpg)](https://www.youtube.com/watch?v=_FVbQCXeGy8)

***

## 11. 226. Invert Binary Tree
Time - O(n)
Space - O(n)

```
/**
 * @param {TreeNode} root
 * @return {TreeNode}
 */
var invertTree = function (root) {

    if(!root) return root;

    function invert(root) {
        if (root) {
            let temp = root.left;
            root.left = root.right;
            root.right = temp;
            invert(root.left);
            invert(root.right);
        }
    }

    invert(root);

    return root;
};
```

***

## 12. 257. Binary Tree Paths
Time - O(n)
Space - O(n)

```
/**
 * @param {TreeNode} root
 * @return {string[]}
 */
var binaryTreePaths = function (root) {
    let paths = [];
    if (!root) return paths;

    function leafPath(root, path) {
        if (root) {
            path += root.val;
            if(!root.left && !root.right){
                paths.push(path);
            } else {
                path += "->";
                leafPath(root.left, path);
                leafPath(root.right, path);
            }

        }
    }

    leafPath(root, "");
    console.log(paths);

    return paths;
};
```

***

## 13. 404. Sum of Left Leaves
Time - O(n)
Space - O(h), height of the Tree on Recursion Stack

```
/**
 * @param {TreeNode} root
 * @return {number}
 */
var sumOfLeftLeaves = function(root) {
    let sum = 0;

    if(!root) return sum;

    let leftLeavesSum = function(node, isLeft){
        if(node){
            if(!node.left && !node.right && isLeft) sum += node.val;

            leftLeavesSum(node.left, true);
            leftLeavesSum(node.right, false);
        }
    }

    leftLeavesSum(root, false);

    return sum;
};
```

***

## 14. 501. Find Mode in Binary Search Tree

Time - O(n)
Space - O(n)

```
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var findMode = function (root) {
    let modes = [];
    let count = 0;
    let maxCount = 0
    let currVal = null;

    if (!root) return modes;

    let inOrderTraverse = function (node) {
        if (node) {
            inOrderTraverse(node.left);
            count = (node.val == currVal) ? count + 1 : 1;
            if (count == maxCount) {
                modes.push(node.val)
            } else if (count > maxCount) {
                maxCount = count;
                modes = [node.val]
            }
            currVal = node.val;

            inOrderTraverse(node.right);
        }
    }

    inOrderTraverse(root);

    return modes;
};
```

***

## 15. 530. Minimum Absolute Difference in BST
Time - O(n)
Space -  O(n)

```
/**
 * @param {TreeNode} root
 * @return {number}
 */
var getMinimumDifference = function (root) {
    let min = Infinity;
    let prev = null;

    function inOrderTraversal(node) {
        if (node) {
            inOrderTraversal(node.left);

            if (prev !== null) {
                min = Math.min(Math.abs(prev - node.val), min);
            }
            prev = node.val;

            inOrderTraversal(node.right);
        }
    }

    inOrderTraversal(root);

    return min;
};
```

***

## 16. 543. Diameter of Binary Tree
Time - O(n)
Space - O(n)

```
/**
 * @param {TreeNode} root
 * @return {number}
 */
var diameterOfBinaryTree = function (root) {
    let diameter = 0;

    let postOrderTraversal = function (node) {
        if (!node) return 0;

        let leftDepth = postOrderTraversal(node.left);
        let rightDepth = postOrderTraversal(node.right);

        diameter = Math.max(diameter, (leftDepth + rightDepth));

        return Math.max(leftDepth, rightDepth) + 1;
    }

    postOrderTraversal(root);

    return diameter;
};
```

***

# Medium Problems

## 1. 98. Validate Binary Search Tree
Time - O(n)
Space -  O(n)

```
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
var isValidBST = function (root) {
    let prev = null;
    let traverse = function (node) { // Inorder Traversal
        if (node == null) return true;

        if (!traverse(node.left)) return false;

        if (prev !== null && node.val <= prev.val) return false;

        prev = node;
        return traverse(node.right);
    }

    return traverse(root);
};
```

***

## 2. 863. All Nodes Distance K in Binary Tree
Time - O(n)
Space -  O(n)

```
/**
 * @param {TreeNode} root
 * @param {TreeNode} target
 * @param {number} k
 * @return {number[]}
 */
var distanceK = function (root, target, k) {

    // when k is Zero, which means zero distance we should return the graph itself
    if (k === 0) return [target.val];

    let parentMap = new Map();

    let traverse = function(root){
        if(!root) return;

        if(root.left){
            parentMap.set(root.left, root);
            traverse(root.left);
        }

        if(root.right){
            parentMap.set(root.right, root);
            traverse(root.right);
        }
    };

    let output = [];
    let visited = new Set();

    let findNode = function(root, dist) {
        if(!root) return;

        if(visited.has(root)) return;

        if(dist == k) output.push(root.val);

        visited.add(root);

        findNode(root.left, dist + 1);
        findNode(root.right, dist + 1);
        findNode(parentMap.get(root), dist + 1);
    }

    traverse(root);
    findNode(target, 0);

    return output;

};  
```

***

## 3. 1361. Validate Binary Tree Nodes
Time - O(n)
Space - O(n)  

```
/**
 * @param {number} n
 * @param {number[]} leftChild
 * @param {number[]} rightChild
 * @return {boolean}
 */


const findRoot = (leftChildren, rightChildren) => {
    let root = 0;
    for(let i = 0; i < leftChildren.length; i++) {
        const left = leftChildren[i];
        const right = rightChildren[i];    
        if(left === root || right == root) root = i;
    }
    return root;
}

var validateBinaryTreeNodes = function(n, leftChild, rightChild) {
    const visited = {};
    const dfs = (i, leftChild, rightChild) => {
        if( visited[i] ) return false;
        visited[i] = true;
        const left = leftChild[i];
        const right = rightChild[i];
        if(left > -1) {
            if(!dfs(left, leftChild, rightChild)) return false;
        }
        if(right > -1) {
            if(!dfs(right, leftChild, rightChild)) return false;
        }
        
        return true;
}
    const root = findRoot(leftChild, rightChild);
    return dfs(root, leftChild, rightChild) && Object.keys(visited).length === n;
};
```
### Video reference 
[![YT Video](https://img.youtube.com/vi/Mw67DTgUEqk/0.jpg)](https://www.youtube.com/watch?v=Mw67DTgUEqk)

***

## 4. 687. Longest Univalue Path
Time - O(n)
Space -  O(h) height of the tree

```
/**
 * @param {TreeNode} root
 * @return {number}
 */
var longestUnivaluePath = function (root) {

    if(!root) return 0;

    let max = 0;

    let postOrderTraversal = function (node) {
        if (!node) return 0;

        let left = postOrderTraversal(node.left);
        let right = postOrderTraversal(node.right);

        if(!node.left || node.left.val !== node.val) left = 0;

        if(!node.right || node.right.val !== node.val) right = 0;

        max = Math.max(max, left + right);
        return Math.max(left, right) + 1;
    }

    postOrderTraversal(root);

    return max;
};
```

***

## 5. 2476. Closest Nodes Queries in a Binary Search Tree
Time - O(N log N)
Space - O(N) 

### Solution 1

```
/**
 * @param {TreeNode} root
 * @param {number[]} queries
 * @return {number[][]}
 */
var closestNodes = function (root, queries) {
    let nodes = [];

    let preOrderTraversal = function (node) { // get all the elements from the tree
        if (node) {
            nodes.push(node.val);
            preOrderTraversal(node.left);
            preOrderTraversal(node.right);
        }
    }

    preOrderTraversal(root);

    let answer = [];

    nodes = nodes.sort((a, b) => a - b) // sort the Array of node values inascending order
    let arr = [];
    for (let i = 0; i < queries.length; i++) {
        arr = [];
        let min, max;
        for (let j = 0; j < nodes.length; j++) {
            if (nodes[j] <= queries[i]) min = nodes[j];

            if (max == null && nodes[j] >= queries[i]) max = nodes[j];
        }

        min = (min == null) ? -1 : min;
        max = (max == null) ? -1 : max;

        arr = [min, max]
        answer.push(arr);
    }

    return answer;

};
```

### Solution 2 - Optimal
Time - O(n logn)
Space - O(n)
```
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number[]} queries
 * @return {number[][]}
 */
var closestNodes = function (root, queries) {
    let nodes = [];

    let inOrderTraversal = function (node) { // get all the elements from the tree in Ascending order
        if (node) {
            inOrderTraversal(node.left);
            nodes.push(node.val);
            inOrderTraversal(node.right);
        }
    }

    inOrderTraversal(root);
    
    let answer = [];

    for(let i = 0; i < queries.length; i++){
        answer.push(findClosestValues(queries[i], nodes));
    }
   
    return answer;

};


function findClosestValues(target, nodeArr){
    let [left, right] = [-1, -1];

    let low = 0;
    let high = nodeArr.length - 1;

    while(low <= high){
        let mid = Math.floor(low + (high - low) / 2);
        if(nodeArr[mid] == target){
            left = right = nodeArr[mid];
            break;
        } else if(nodeArr[mid] < target){
            left = nodeArr[mid];
            low = mid + 1;
        } else {
            right = nodeArr[mid];
            high = mid - 1;
        }
    }

    return [left, right];
}   
```
***

## 6. 662. Maximum Width of Binary Tree

### Solution 1 
Time - O(n)
Space - O(n)

```
var widthOfBinaryTree = function(root) {
    if (root == null) return 0;

    let res = 0;
    let queue = [[root, 0]]; // [Node, index]
    
    while (queue.length) {
        let levelSize = queue.length;
        let levelMinIndex = queue[0][1]; // Get the index of the first node at the current level
        let firstIndex = 0, lastIndex = 0;
        
        for (let i = 0; i < levelSize; i++) {
            let [node, index] = queue.shift();
            index -= levelMinIndex; // Normalize index to prevent overflow
            
            if (i === 0) firstIndex = index; // First index at this level
            if (i === levelSize - 1) lastIndex = index; // Last index at this level
            
            if (node.left) queue.push([node.left, 2 * index]);
            if (node.right) queue.push([node.right, 2 * index + 1]);
        }
        
        res = Math.max(res, lastIndex - firstIndex + 1);
    }
    
    return res;
};
```

### Solution 2  
Time - O(n)
Space - O(n)  

```
/**
 * @param {TreeNode} root
 * @return {number}
 */
var widthOfBinaryTree = function(root) {
    let res = 0;

    let queue = [[root, 1, 0]]; // [Node, num, level]
    let [prevLevel, prevNum] = [0, 1];
    
    while (queue.length){
        let curr = queue.shift();
        let [node, num, level] = curr;

        if(level > prevLevel) {
            preLevel = level;
            preNum = num;
        }

        res = Math.max(res, num - prevNum + 1);

        if(node.left) queue.push([node.left, num * 2 , level + 1]);
        if(node.right) queue.push([node.right, (num * 2) + 1, level + 1]);

    }

    return res;
};
```
### Video Reference 
[![YT Video](https://img.youtube.com/vi/FPzLE2L7uHs/0.jpg)](https://www.youtube.com/watch?v=FPzLE2L7uHs)

***

## 7. 1367. Linked List in Binary Tree
Time - O(m * n) m, no of nodes in tree; n, no of nodes in linked list 
Space -  O(h), h, height of the tree

```
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {ListNode} head
 * @param {TreeNode} root
 * @return {boolean}
 */
var isSubPath = function (head, root) {
    if (!root) return false;

    if (root.val == head.val) {
        if (checkEquality(root, head)) return true;
    }

    return isSubPath(head, root.left,) || isSubPath(head, root.right);
};

function checkEquality(root, list) {
    if (!list) return true;

    if (!root) return false;

    if (list.val !== root.val) return false;

    return checkEquality(root.left, list.next) || checkEquality(root.right, list.next);
}
```

***

## 8. 331. Verify Preorder Serialization of a Binary Tree
Time - O(n)
Space -  O(1)

```
/**
 * @param {string} preorder
 * @return {boolean}
 */
var isValidSerialization = function (preorder) {

    let preOrderArr = preorder.split(",");
    let slots = 1;

    for(let node of preOrderArr){
        // console.log(node);
        if(slots <= 0 ) return false;

        if(node == "#"){
            slots += -1 
        } else {
            slots += 1;
        }
    }

    return slots == 0;
};
```
### Video Reference
[![YT Video](https://img.youtube.com/vi/25WFGyeNbg0/0.jpg)](https://www.youtube.com/watch?v=25WFGyeNbg0)

***

## 9. 2583. Kth Largest Sum in a Binary Tree
**Time complexity**:
The time complexity of this solution is O(n) where n is the number of nodes in the binary tree. This is because we are traversing each node once to calculate the level sums and then sorting the level sums array, which takes O(nlogn) time complexity. However, since we are only interested in the kth largest level sum, the overall time complexity is O(n).

**Space complexity**:
The space complexity is also O(n) because we are using a queue to perform level order traversal of the binary tree and storing the level sums in an array. The size of the queue can be at most the number of nodes in the binary tree, which is O(n).

```
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} k
 * @return {number}
 */
var kthLargestLevelSum = function (root, k) {

    let levelSum = [];

    let queue = [root];

    let sum = 0
    while (queue.length) {
        sum = 0;
        let queueLen = queue.length;
        for (let i = 0; i < queueLen; i++) {
            let node = queue.shift();
            sum += node.val;
            if (node.left) {
                queue.push(node.left);
            }

            if (node.right) {
                queue.push(node.right);
            }
        }
        levelSum.push(sum);
    }

    return levelSum.sort((a, b) => b - a)[k - 1] || -1;
};
```

***

## 10. 2049. Count Nodes With the Highest Score
Time - 
Space -  

```

```

***

## 11. 113. Path Sum II
Time - O(N)
Space -  O(N)

```
/**
 * @param {TreeNode} root
 * @param {number} targetSum
 * @return {number[][]}
 */
var pathSum = function (root, targetSum) {
    let fullPath = [];

    function dfs(root, targetSum, list) {
        if (root == null) return; // when no nodes present

        list.push(root.val)

        // check leaf nodes && current value is TargetSum :: success we found the sum
        if (root.val == targetSum && (root.left == null && root.right == null)) {
            fullPath.push(list.slice());
            list.pop();
            return;
        }

        dfs(root.left, targetSum - root.val, list);
        dfs(root.right, targetSum - root.val, list);
        list.pop();
        return;
    }

    dfs(root, targetSum, []);
    return fullPath;
};
```

***

## 12. 437. Path Sum III
Time - O(N)
Space -  O(N)

```
/**
 * @param {TreeNode} root
 * @param {number} targetSum
 * @return {number}
 */
var pathSum = function (root, targetSum) {
    let fullPathCounter = 0;
    let map = {};

    function dfs(node, pathSum) {
        if (node == null) return null; // when no nodes present

        pathSum += node.val;
        // check leaf nodes && current value is TargetSum :: success we found the sum
        if (pathSum == targetSum) {
            fullPathCounter += 1;
        }

        if (map[pathSum - targetSum]) fullPathCounter += map[pathSum - targetSum];

        if (map[pathSum]) map[pathSum]++;
        else map[pathSum] = 1;

        if(node.left) dfs(node.left, pathSum);
        if(node.right) dfs(node.right, pathSum);

        map[pathSum]--;
    }

    dfs(root, 0);
    return fullPathCounter;
};
```
### Video Reference
[![YT Video](https://img.youtube.com/vi/ofMqFAFVcKY/0.jpg)](https://www.youtube.com/watch?v=ofMqFAFVcKY)

***

## 13. 1339. Maximum Product of Splitted Binary Tree
Time - O(N)
Space - O(N)

```
/**
 * @param {TreeNode} root
 * @return {number}
 */
var maxProduct = function (root) {

    let sum = [];

    function postOrderTraverse(node) {
        if (node == null) return 0;

        let leftSum = postOrderTraverse(node.left);
        let rightSum = postOrderTraverse(node.right);
        sum.push(leftSum, rightSum); // sum.push(leftSum).push(rightSum);
        return leftSum + rightSum + node.val;
    }

    let totalSum = postOrderTraverse(root);
    // console.log(sum);
    // console.log(totalSum);

    let max = 0;

    for (let num of sum) {
        let curr = num * (totalSum - num);
        max = Math.max(max, curr);
    }

    return max % (10 ** 9 + 7) ;

};
```
### Video Reference
[![YT Video](https://img.youtube.com/vi/ZGmvcUtXKxU/0.jpg)](https://www.youtube.com/watch?v=ZGmvcUtXKxU)

***

## 14. 2467. Most Profitable Path in a Tree
Time - 
Space -  

```
NOT ATTEMPTED
```

***

## 15. 2096. Step-By-Step Directions From a Binary Tree Node to Another
Time - O(N)
Space -  O(N)

```
/**
 * @param {TreeNode} root
 * @param {number} startValue
 * @param {number} destValue
 * @return {string}
 */
var getDirections = function (root, startValue, destValue) {
    let start = "", end = "";

    function traverse(node, path) {

        if (node == null) return "";

        if (startValue == node.val) start = path;
        if (destValue == node.val) end = path;

        traverse(node.left, path + "L");
        traverse(node.right, path + "R");
    }

    traverse(root, "");
    let index = 0;
    
    while(start[index] == end[index]){
        index += 1;
    }
    
    return start.slice(index).split('').map(_ => "U").join("") + end.slice(index);
};
```

***


## 16. 558. Logical OR of Two Binary Grids Represented as Quad-Trees
Time - O(N)
Space -  O(N)

```
/**
 * @param {Node} quadTree1
 * @param {Node} quadTree2
 * @return {Node}
 */
var intersect = function (quadTree1, quadTree2) {

    if (quadTree1.isLeaf) return quadTree1.val ? quadTree1 : quadTree2;

    if (quadTree2.isLeaf) return quadTree2.val ? quadTree2 : quadTree1;


    let nodes = [
        intersect(quadTree1.topLeft, quadTree2.topLeft),
        intersect(quadTree1.topRight, quadTree2.topRight),
        intersect(quadTree1.bottomLeft, quadTree2.bottomLeft),
        intersect(quadTree1.bottomRight, quadTree2.bottomRight),
    ]

    let areSame = nodes.every(({ isLeaf, val }) => isLeaf && val);

    let [topLeft, topRight, bottomLeft, bottomRight] = nodes;

    if (areSame) return topLeft;

    return new Node(true, false, topLeft, topRight, bottomLeft, bottomRight);
};
```

***


## 17. 971. Flip Binary Tree To Match Preorder Traversal
Time - O(N)
Space -  O(N)

```
/**
 * @param {TreeNode} root
 * @param {number[]} voyage
 * @return {number[]}
 */
var flipMatchVoyage = function (root, voyage) {
    let flips = [];
    let index = 0;

    let preOrder = function (node) {
        if (node == null || flips[0] == -1) return;

        if (node.val !== voyage[index++]) {
            flips = [-1];
        } else if (node.left && node.left.val !== voyage[index]) {
            flips.push(node.val);
            preOrder(node.right);
            preOrder(node.left);
        } else {
            preOrder(node.left);
            preOrder(node.right);
        }
    }

    preOrder(root);
    return flips;
};

```
***

### 102. Binary Tree Level Order Traversal

Time O(N)
Space O(N)

```

/**
 * @param {TreeNode} root
 * @return {number[][]}
 */
var levelOrder = function (root) {
    if(!root) return [];
    let queue = [root]; // enqueue
    let values = [];
    while (queue.length) {
        let queueLen = queue.length;
        let currLevel = [];
        for (let i = 0; i < queueLen; i++) {
            let node = queue.shift(); // dequeue
            if (node) {
                if (node.left) queue.push(node.left);
                if (node.right) queue.push(node.right);

                currLevel.push(node.val);
            }
        }
        values.push(currLevel);
    }

    return values;

};

```

***

### 236. Lowest Common Ancestor of a Binary Tree

Time O(N)
Space O(N)

```
/**
 * @param {TreeNode} root
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {TreeNode}
 */
var lowestCommonAncestor = function (root, p, q) {
    if (!root) return null;

    // If the current node is either p or q, return it
    if (root === p || root === q) return root;

    // Recur for left and right subtrees
    let left = lowestCommonAncestor(root.left, p, q);
    let right = lowestCommonAncestor(root.right, p, q);

    // If p and q are found in left and right subtrees, root is the LCA
    if (left && right) return root;

    // Otherwise, return the non-null child (left or right)
    return left ? left : right;
};
```

***

### 103. Binary Tree Zigzag Level Order Traversal

Time O(N)
Space O(N)

```
/**
 * @param {TreeNode} root
 * @return {number[][]}
 */
var zigzagLevelOrder = function (root) {
    if (!root) return [];

    let queue = [root];
    let values = [];
    let reverse = 0;
    while (queue.length) {
        let queueLen = queue.length;
        let levels = [];
        for (let i = 0; i < queueLen; i++) {
            let node = queue.shift();
            if (node) {
                if (node.left) queue.push(node.left);

                if (node.right) queue.push(node.right);

                if (reverse % 2 == 0) levels.push(node.val);
                else levels.unshift(node.val);
            }
        }

        values.push(levels);
        reverse++;
    }

    return values;
};

```
***

### 105. Construct Binary Tree from Preorder and Inorder Traversal

Time and Space: O(N)

```
/**
 * @param {number[]} preorder
 * @param {number[]} inorder
 * @return {TreeNode}
 */
var buildTree = function (preorder, inorder) {

    if (preorder.length == 0) return null;

    let mid = inorder.indexOf(preorder[0]);
    let root = new TreeNode(preorder[0]);

    root.left = buildTree(preorder.slice(1, mid + 1), inorder.slice(0, mid));
    root.right = buildTree(preorder.slice(mid + 1), inorder.slice(mid + 1));
    return root;
};

```
***

###  106. Construct Binary Tree from Inorder and Postorder Traversal

Time and Space is O(N)

```
/**
 * @param {number[]} inorder
 * @param {number[]} postorder
 * @return {TreeNode}
 */
var buildTree = function (inorder, postorder) {
    if (inorder.length == 0) null;

    let map = new Map();

    for (let i = 0; i < inorder.length; i++) { map.set(inorder[i], i) };

    let recurse = function (start, end) {
        if (start > end) return null;

        let val = postorder.pop();
        let root = new TreeNode(val);
        root.right = recurse(map.get(val) + 1, end);
        root.left = recurse(start, map.get(val) - 1);
        return root;
    }

    return recurse(0, inorder.length - 1);
};
```

### 114. Flatten Binary Tree to Linked List 

Time O(N)  Space O(1)

```
/**
 * @param {TreeNode} root
 * @return {void} Do not return anything, modify root in-place instead.
 */
var flatten = function (root) {

    if (!root) return null;

    while (root) {
        if (root.left) { // loop through all the left nodes 
            let left = root.left;
            let curr = left;

            while (curr.right) curr = curr.right; // move to the right most node

            curr.right = root.right; // connect the right most node with root's right
            root.left = null; // mark the root's left as null
            root.right = left; // poin tthe root's right to new left node
        }

        root = root.right; // point and start the right from the root's next node.
    }
};
```

***

***

## Hard Problems

### 987. Vertical Order Traversal of a Binary Tree

Time O(N log N)
Space O(N)

```
/**
 * @param {TreeNode} root
 * @return {number[][]}
 */

var verticalTraversal = function (root) {
    let indexes = [];
    let result = []

    let preOrderTraversal = (node, row, col) => {
        if (!node) return;
        indexes.push([col, row, node.val]);

        preOrderTraversal(node.left, row + 1, col - 1);
        preOrderTraversal(node.right, row + 1, col + 1);
    }

    preOrderTraversal(root, 0, 0);

    // Sort by column first, then by row, and then by value
    indexes.sort((a, b) => {
        if (a[0] !== b[0]) return a[0] - b[0];
        if (a[1] !== b[1]) return a[1] - b[1];
        return a[2] - b[2];
    });

    let visitedMap = new Map();

    for (let [col, row, value] of indexes) {
        if (!visitedMap.has(col)) {
            result.push([value]);
            visitedMap.set(col, result.length - 1);
        } else {
            result[visitedMap.get(col)].push(value);
        }
    }

    return result;
};

```

***

### 124. Binary Tree Maximum Path Sum

Time and Space : O(N)

```
var maxPathSum = function (root) {
    if (!root) return 0;

    let max = -Infinity;
    let preorderTraversal = (node) => {

        if (!node) return 0;

        let value = node.val;

        let leftSum = preorderTraversal(node.left);
        let rightSum = preorderTraversal(node.right);

        let allSum = value + leftSum + rightSum;
        leftSum += value;
        rightSum += value;

        max = Math.max(max, value, leftSum, rightSum, allSum);
        return Math.max(leftSum, rightSum, value);
    }

    preorderTraversal(root);

    return max;
};
```

***
