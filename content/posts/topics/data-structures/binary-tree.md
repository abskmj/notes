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

## Level Order
In level order, the traversal progresses level by level. Each iteration will visit every node in a level. Nodes at same level are traversed from left most to right most.

```
    1     => level 1
   / \
  2   3   => level 2
 / \
4   5     => level 3
```

Consider the above binary tree where node `1` is at level 1, nodes `2` & `3` are at level 2 and nodes `4` & `5` are at level 3. So, traversing it level by level results in sequence `1 2 3 4 5`.
```
Nodes:  1 2 3 4 5
Levels: 1 2 2 3 3
```

### Implementation using a Queue
```java
public static void levelOrderTraversal(Node root){
    Queue<Node> queue = new LinkedList<>();
    
    // add root to get started
    queue.add(root);
    
    while(queue.size() > 0){
        // get first element from the queue and remove it
        Node current = queue.remove();
        System.out.print(current.getValue() + " ");
        
        // check if current node has left and/or right child and add them to the queue
        if(current.getLeftChild() != null){
            queue.add(current.getLeftChild());
        }
        
        if(current.getRightChild() != null){
            queue.add(current.getRightChild());
        }
    }
    
    System.out.println("");
}
```

Sample code to test

```java
public class Test {
    public static void main(String args[]) {
        Node node1 = new Node(1);
        Node node2 = new Node(2);
        Node node3 = new Node(3);
        Node node4 = new Node(4);
        Node node5 = new Node(5);
        
        node1.setLeftChild(node2);
        node1.setRightChild(node3);
        node2.setLeftChild(node4);
        node2.setRightChild(node5);
        
        Node.levelOrderTraversal(node1);
    }
}

/* Output

1 2 3 4 5

*/
```

Step by Step analysis
```java
public static void levelOrderTraversal(Node root){
    Queue<Node> queue = new LinkedList<>();
    
    // add root to get started
    queue.add(root);
    
    while(queue.size() > 0){
        // get first element from the queue and remove it
        Node current = queue.remove();
        System.out.println("Current node is "+current.getValue());
        
        // check if current node has left and/or right child and add them to the queue
        if(current.getLeftChild() != null){
            queue.add(current.getLeftChild());
            System.out.println("Add left child "+current.getLeftChild().getValue()+" to queue");
        }
        
        if(current.getRightChild() != null){
            queue.add(current.getRightChild());
            System.out.println("Add right child "+current.getRightChild().getValue()+" to queue");
        }
    }
}

/* Output

Current node is 1
Add left child 2 to queue
Add right child 3 to queue
Current node is 2
Add left child 4 to queue
Add right child 5 to queue
Current node is 3
Current node is 4
Current node is 5

*/

```

# Height of a Binary Tree


## Recursive Method

# Balanced Binary Tree