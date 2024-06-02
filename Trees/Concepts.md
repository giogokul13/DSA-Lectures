# Trees

## Why Trees
1. You can perform any operation is O(log n) times
2. Ordered Storage
3. Cost Efficient
4. 

## Unbalanced Binary tree
Where the nodes on left are empty and the nodes at right has values continuously - Which might take O(n) Time

<img width="656" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/75a5f37f-4704-474b-b3c7-1c4a51fb5b97">

## Self Balanced Binary Tree


## Where it is used
1. File systems
2. Databases
3. Network Routing
4. Decision Tree - Machine Learning
5. File Compressions
6. Future Data Structure


## Element Placing Binary Tree
You can place your elements anywhere isn the nodes, no need follow a order
Similar to Linked Data Structure, but trere as additionla nodee
Class Node (){
  this.val<Number>;
  this.left <Node>;
  this.right <Node>;
}


## Element Placing Binary Search Tree
### All the smaller elements to the previous node goes left and greater elements go right
eg        10
     5          6
   3     7            20
                  15

## Operations of Binary Search Tree
1. Insertion
2. Search
3. DFS & BFS
4. Deletion

## ApPlications of BST
1. Searching
2. Sorting
3. Implement high level datatypes such as Lookup tables and Priority Queues
   

### Size of the Tree - Total no, of nodes in the Tree
### Child and Parent - Parent has child nodes
### Siblings - Nodes which have same parent
### Edge - Line which is connecting the the nodes
### Height -  Max (No, of edges from the current node to leaf node in the tree)
### Leaf Nodes - Last Nodes in the Tree Branch
### Level -  Height of Root Node - Height of current Node
### Ancestores and Descendent
### Degree -  No, of childers of current Node ranges with [0, 1, 2]

## Types of Binary tree

### Complete Binary Tree
All the levels are full and The last level can be incomplete but the nodes shouldd filled from left to right with out missing any node

### Full Strict Binary tree
Every Node has either Zero or two children

### Perfect Binary Tree
All the Levels are filled

### Height Balanced BT -  Average Height O(log n)

### Skewed BT - Every node has only node child

### Ordersed BT
Everey Node has some propertie eg Binary Search Tree.


## Properties

### On the perfect BT
Nodes = 2 [^ (h + 1)] - 1 where h is the height of the binary tree

### On Perfect BT
Total no, of leaf nodees = 2[^h] - 1 , height  - tree height

### On Perfect BT

To leaves
The no of levels = log(N + 1) where N is no of leaves
levels = Log(N + 1) where N is no of leaves

To Nodes
levels = Log(N + 1) levels minimun here N is Nodes

### On Strict Binary tree
Internal Nodes  = N - 1, where N is the leaf Nodes
Leaf Nodes = N + 1, Where N is the internal Nodes

### 
No, of leaf Nodes = 1 + no, of Internal Nodes with 2 Childrens (apart from the root node)


## Binary Tree Implementation

1. Linked Representation
  Similar to Linked List
2. Sequential Representation
  Representing ina  array Format (Not suggested widely)
 

## DFS -  Depth First Search
<img width="885" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/6bd4dd7c-8689-47d0-9b93-13840da324e5">

### Preorder Traversal
<img width="378" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/c41edc04-d04e-4273-8119-917de5f23058">

<img width="913" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/a0c6abe0-506d-4b25-829f-2128fd392afd">

### Inorder Traversal
<img width="402" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/98de104d-e99d-4ad4-a231-a436dcbd89b5">

<img width="920" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/97951941-a3d9-4458-92ad-6da70ab5c2a8">

### Post Order Traversal
<img width="395" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/13120209-b030-4670-9a6f-2d32ab253e17">

<img width="922" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/62d94d32-87f7-46ab-9103-79a7e4797ad9">

## BFS -  Breadth First Search
<img width="905" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/d6a8f59d-2110-4201-9790-d9f51ae2fef6">

<img width="916" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/5a77f9c0-50dd-4481-8f0a-bba478bb8f48">

### BFS Traversal Approaches
  <img width="508" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/be25d062-1dfd-4349-8117-84e7333b1a12">

  <img width="920" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/c153014c-8502-4594-87ee-c4c92b41b1eb">


## Delete the Node

### Remove Node - No Child or Remove leaf Node
<img width="617" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/ef5fcdea-1134-4d1b-844b-bc0581983f92">

### Node to be deleted as one child Node
<img width="615" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/5dc50f6b-d2e8-4137-a643-cafc115a2bbc">

### Node to be deleted has two child Nodes
<img width="627" alt="image" src="https://github.com/giogokul13/DSA-Lectures/assets/63816836/2a081a6c-8ded-4852-92b3-7da3c8e73679">


# Sudo Code BST

```
class Node (){
  constructor(value){
    this.value = value
    this.left = null;
    this.right = null;
  }
}

class BinarySearchTree(){
  constructor(){
    this.root = null;  
  }

  this.isEmpty = function(){  // check whethe rthe roor is null or not
    return (this.root == null);
  }

  this.insert = function(value){
    let node = new Node(value);
    if(this.isEmpty()){
      this.root = node;
    } else {
      this.insertNode(this.root, node);
    }
  }

  this.insertNode = function (root, node){

    if(node.value < root.value){

      if(root.left == null) {
        root.left = node;
      } else {
        this.insertNode(root.left, neweNode);
      }

    } else {
      if(root.right == null) {
        root.right = node;
      } else {
        this.insertNode(root.right, neweNode);
      }
    }

  }

  this.search = function(root, value){
    if(!root) return false;

    if(root.value == value) return true;

    if(value < root.value) {
      return this.search(root.left, value);
    } else {
       return this.search(root.right, value);
    }
  }

  /**
  * DFS Methods
  */
  this.preOrder = function(root){
    if(root){
      console.log(root.value);
      this.preOrder(root.left)
      this.preOrder(root.right);
    }    
  }

  this.inOrder = function(root){
    if(root){
      this.Inorder(root.left);
      console.log(root.value);
      this.Inorder(root.right);
      console.log(root.value);
    }
  }

  this.postOrder = function(root){
    if(root){
      this.postOrder(root.left);
      this.postOrder(root.right);
      console.log(root.value);
    }
  }

  /* * END DFS  */

  /**
  *  BFS Methos
  */

    this.levelOrder = function(){
      let queue = []; // use a Optimized Key from Code Evolution Videos
      queue.push(this.root);
      while(queue.length){
        let curr = queue.shift();
        console.log(curr.value);
        if(curr.left){
          queue.push(curr.left);
        }
        if(curr.right){
          queue.push(curr.right);
        }
      }
    }

    /** END BFS  */

    this.getMinValue = function(root){
      if(!root.left) {
        return this.root.value;
      } else {
        return this.getMinValue(root.left)
      }     
    }

    this.getMaxValue = function(root){
      if(!root.right) {
        return this.root.value;
      } else {
        return this.getMaxValue(root.right)
      }     
    }

    this.delete = function(value){
      this.root = this.deleteNode(this.root, value);
    }

    this.deleteNode = function(root, value){
      if(!root) return root;

      if(value < root.value){
        root.left = this.deleteNode(root.left, value);
      } else {
        root.right = this.deleteNode(root.right, value);
      } else {
        if(!root.left && !root.right) {
          return null;
        }
        if(!root.left){
          return root.right;
        } else if(!root.right) {
          return root.left;
        }

        root.value = this.getMinValue(root.right);
        root.right = this.deleteNode(root.right, root.value);
      }

      return root;
    }

}

let BST = new BinarySearhTree() // Invoke the BST Class

```


