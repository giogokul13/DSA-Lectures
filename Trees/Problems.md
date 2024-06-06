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
Video Reference https://www.youtube.com/watch?v=0K0uCMYq5ng
***

## 6. 110. Balanced Binary Tree
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


## 10. 94. Binary Tree Inorder Traversal
Time -
Space - 

```

```

***

## 11. 94. Binary Tree Inorder Traversal
Time -
Space - 

```

```

***

## 12. 94. Binary Tree Inorder Traversal
Time -
Space - 

```

```

***
