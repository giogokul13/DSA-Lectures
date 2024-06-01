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


## Eement Placing Binary Tree
You can place your elements anywhere isn the nodes, no need follow a order
Similar to Linked Data Structure, but trere as additionla nodee
Class Node (){
  this.val<Number>;
  this.left <Node>;
  this.right <Node>;
}

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
2. Sequentioal Representation
  Representing ina  array Format (Not suggested widely)

 


## Element Placing Binary Search Tree
### All the smaller elements to the previous node goes left and greater elements go right
eg        10
     5          6
   3     7            20
                  15
