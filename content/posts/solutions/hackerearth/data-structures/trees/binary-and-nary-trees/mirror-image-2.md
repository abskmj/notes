---
title: "HackerEarth - Mirror Image"
date: 2017-11-18T11:36:52+05:30
tags: ["HackerEarth","Solution","Java"]
---

# Solution
- Parse input and build the tree by maintaining an index `HashMap`.
- Traverse tree and mirror tree simultaneously to find the mirror node.

```java
/* Solution to HackerEarth: Mirror Image
 * URL: https://www.hackerearth.com/practice/data-structures/trees/binary-and-nary-trees/practice-problems/algorithm/mirror-image-2/
 */
import java.util.*;

class TestClass {
    public static void main(String args[] ) throws Exception {
        //Scanner
        Scanner in = new Scanner(System.in);
        int N = in.nextInt();
        int Q = in.nextInt();
        
        Map<Integer, Node> index = new HashMap<>();
        
        // initialize root node
        Node root = new Node(1);
        
        index.put(1, root);
        
        // build tree
        for(int i=0; i < N-1; i++){
            int parent = in.nextInt();
            int child = in.nextInt();
            char side = in.next().charAt(0);
            
            // get parent node from index
            Node node = index.get(parent);
            
            // create a new child node and add to index
            Node childNode = new Node(child);
            index.put(child, childNode);
            
            if(side == 'L'){
                node.left = childNode;
            }
            else if (side == 'R'){
                node.right = childNode;
            }
        }
        
        // process queries
        for(int i=0; i < Q; i++){
            int target = in.nextInt();
            
            System.out.println(findMirror(root, target));
        }

    }
    
    public static int findMirror(Node root, int target){
        if(root.value == target){
            return target;
        }
        else{
            return recurse(target, root.left, root.right);
        }
    }
    
    public static int recurse(int target, Node left, Node right){

        // no need to further traverse because either current node or mirror node is null
        if(left == null || right == null){
            return -1;
        }
        
        // if target found return mirror node
        if(left.value == target){
            return right.value;
        }
        
        if(right.value == target){
            return left.value;
        }
        
        int mirror = recurse(target, left.left, right.right);
        
        // return mirror if found
        if(mirror > 0){
            return mirror;
        }
        
        return recurse(target, left.right, right.left);
    }
    
    
}

class Node {
    public int value;
    public Node left;
    public Node right;
    
    public Node(int value){
        this.value = value;
    }
}
```