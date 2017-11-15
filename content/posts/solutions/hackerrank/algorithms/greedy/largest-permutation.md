---
title: "HackerRank - Largest Permutation"
date: 2017-11-09T22:02:51+05:30
tags: ["HackerRank","Solution","Java"]
---

# Solution #1
- Keep indexes of all numbers in a `HashMap`.
- Check if current maximum number is already at desired index i.e highest at index 0, second highest at index 1 and so on.
- If not, keep on swapping them till all the swaps are exhausted.

```java
/* Solution to HackerRank: Largest Permutation
 * URL: https://www.hackerrank.com/challenges/largest-permutation
 */
import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        
        int N = in.nextInt();
        int K = in.nextInt();
        
        int[] n = new int[N];
        
        Map<Integer,Integer> index = new HashMap<>();
        
        for(int i = 0; i < N; i++){
            n[i] = in.nextInt();
            
            index.put(n[i],i);
        }
        
        int max = N;
        
        for(int j = 0; j < N ; j++){
            
            int maxIndex = index.get(max);
            
            if(maxIndex != j){
                // make a swap
                K--;
                
                int temp = n[j];
                n[j] = max;
                n[maxIndex] = temp;
                
                // update indexes
                index.put(max,j);
                index.put(temp,maxIndex);
            }
            
            max--;
            
            // break the loop if swaps are exhausted
            if(K == 0){
                break;
            }
        }
        
        for(int i = 0; i < N; i++){
            System.out.print(n[i] + " ");
        }
        
    }
}
```

# Solution #2
- Find the maximum number in each iteration.
- Swap them in order of decreasing value till all the swaps are exhausted.

Test cases 13 to 15 timed out for this solution.

```java
import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        
        int N = in.nextInt();
        int K = in.nextInt();
        
        int[] n = new int[N];
        
        for(int i = 0; i < N; i++){
            n[i] = in.nextInt();
        }
        
        for(int j = 0; j < N ; j++){
            int max = n[j];
            int maxIndex = j;
            for(int i = j; i < N; i++){
                if(n[i] > max){
                    max = n[i];
                    maxIndex = i;
                }
            }
            
            if(maxIndex != j){
                // make a swap
                n[maxIndex] = n[j];
                n[j] = max;
                K--;
            }
            
            if(K == 0){
                break;
            }
        }
        
        for(int i = 0; i < N; i++){
            System.out.print(n[i] + " ");
        }
        
    }
}
 ```