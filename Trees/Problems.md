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


## 2. 94. Binary Tree Inorder Traversal
Time -
Space - 

```

```

***

## 3. 94. Binary Tree Inorder Traversal
Time -
Space - 

```

```

***
