---
title: "Data Structure - Binary Tree"
date: 2017-11-08T19:15:05+05:30
draft: true
---

# Binary Tree
 A binary tree is a tree data structure in which each node has at most two children, which are referred to as the left child and the right child. [Wikipedia](https://en.wikipedia.org/wiki/Binary_tree)

```
    O
   / \
  O   O
 / \
O   O
```

A java class representing a binary tree.

```java
class Node {
    private Node left;
    private Node right;
    
    private int value;
    
    public Node(int value){
        this.value = value;
    }
    
    public void setLeftChild(Node node){
        this.left = node;
    }
    
    public void setRightChild(Node node){
        this.right = node;
    }
    
    public Node getLeftChild(){
        return this.left;
    }
    
    public Node getRightChild(){
        return this.right;
    }

    public int getValue(){
        return this.value;
    }
}
```

```
    1
   / \
  2   3
 / \
4   5
```

# Traversals
Binary trees can be traversed in 3 ways:

- Level-Order
- Pre-Order
- Post-Order

# Height of a Binary Tree


## Recursive Method

# Balanced Binary Tree