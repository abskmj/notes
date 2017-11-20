---
title: "HackerEarth - Binary Tree"
date: 2017-11-20T20:04:29+05:30
tags: ["HackerEarth","Solution","Java","Binary Tree"]
---

# Solution
- Diameter of a binary tree is maximum of diameter of current node, its left and right child.

```java
/* Solution to HackerEarth: Binary Tree
 * URL: https://www.hackerearth.com/practice/data-structures/trees/binary-and-nary-trees/tutorial/
 */
import java.util.*;

class TestClass {
    public static void main(String args[] ) throws Exception {
        Scanner in = new Scanner(System.in);
        int T = in.nextInt();
        int X = in.nextInt();
        
        Node root = new Node(X);
        
        for(int t=0; t < T-1; t++){
            String path = in.next();
            
            Node node = new Node(in.nextInt());
            
            // add new node to the tree
            add(root, path.toCharArray(), 0, node);
        }
        
        System.out.println(diameter(root));
        
    }
    
    public static void add(Node root, char[] path, int current, Node target){
        if(path.length-1 == current){
            if(path[current] == 'L'){
                // update the value of temporary node or add the new node
                if(root.left != null){
                    root.left.value = target.value;
                }
                else{
                    root.left = target;
                }
            }
            else if(path[current] == 'R'){
                // update the value of temporary node or add the new node
                if(root.right != null){
                    root.right.value = target.value;
                }
                else{
                    root.right = target;
                }
            }
        }
        else{
            if(path[current] == 'L'){
                // add a temporary node if not added yet
                if(root.left == null){
                    root.left = new Node(0);
                }
                add(root.left, path, current+1, target);
            }
            else if(path[current] == 'R'){
                // add a temporary node if not added yet
                if(root.right == null){
                    root.right = new Node(0);
                }
                add(root.right, path, current+1, target);
            }
        }
    }
    
    public static int height(Node root){
        if(root == null){
            return 0;
        }
        else{
            return Math.max(height(root.left), height(root.right))+1;
        }
    }
    
    public static int diameter(Node root){
        if(root == null){
            return 0;
        }
        else{
            // diameter of current node
            int diameter = height(root.left)+height(root.right)+1;
            
            // return maximum of diameter of current node or left child or right child            
            return Math.max(diameter, Math.max(diameter(root.left),diameter(root.right)));
        }
    }
    
}

class Node{
    public int value;
    public Node left;
    public Node right;
    
    public Node(int value){
        this.value = value;
    }
}
```