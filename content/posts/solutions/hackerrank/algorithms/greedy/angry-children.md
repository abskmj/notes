---
title: "HackerRank - Max Min"
date: 2017-11-18T17:20:41+05:30
tags: ["HackerRank","Solution","Java"]
---

# Solution
- Sort the array of numbers
- Find the minimum difference between ith and (i+K-1)th element in each iteration.

```java
/* Solution to HackerRank: Max Min
 * URL: https://www.hackerrank.com/challenges/angry-children
 */
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;

public class Solution {
    
   public static void main(String[] args) throws NumberFormatException, IOException {

    BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
    int N = Integer.parseInt(in.readLine());
    int K = Integer.parseInt(in.readLine());
    int[] list = new int[N];

    for(int i = 0; i < N; i ++)
        list[i] = Integer.parseInt(in.readLine());
      
    int unfairness = Integer.MAX_VALUE;
      
    Arrays.sort(list);

    // find minimum difference between ith and (i+K-1)th element in a sorted array
    for(int i = 0; i < N-K+1; i++){
        int diff = list[i+K-1] - list[i];
            
        unfairness = Math.min(unfairness, diff);
    }
      
    System.out.println(unfairness);
   }
}
``` 