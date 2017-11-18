---
title: "HackerRank - Maximum Perimeter Triangle"
date: 2017-11-18T17:01:27+05:30
tags: ["HackerRank","Solution","Java"]
---

# Solution
- Iterate the sides in descending order
- Check if [sides make a triangle](https://www.wikihow.com/Determine-if-Three-Side-Lengths-Are-a-Triangle) by checking if sum of two sides is greater than third side .

```java
/* Solution to HackerRank: Maximum Perimeter Triangle
 * URL: https://www.hackerrank.com/challenges/maximum-perimeter-triangle
 */
import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        
        int N = in.nextInt();
        
        int[] l = new int[N];
        
        for(int i=0; i < N; i++){
            l[i] = in.nextInt();
        }
        
        Arrays.sort(l);
        
        // iterate in descending order
        for(int a = l.length-1; a > 1; a--){
            for(int b = a-1; b > 0; b--){
                for(int c = b-1; c > -1; c--){
                    // check if sum of two sides is greater than the third side
                    if(l[a] + l[b] > l[c] && l[a] + l[c] > l[b] && l[b] + l[c] > l[a]){
                        System.out.println(l[c]+" "+l[b]+" "+l[a]);
                        return;
                    }
                }
            }
        }
        
        System.out.println(-1);
        
    }
}
```