---
title: "HackerRank - Hackerland Radio Transmitters"
date: 2017-11-08T21:50:01+05:30
tags: ["HackerRank","Solution","Java"]
---

# Solution
- Iterate through each house in a sorted order.
- Check if current house is in range of last transmitter.
- If not, find a house to put transmitter on so that current house is in range.

```java
/* Solution to HackerRank: Hackerland Radio Transmitters
 * URL: https://www.hackerrank.com/challenges/hackerland-radio-transmitters
 */
import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;

public class Solution {

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int n = in.nextInt();
        int k = in.nextInt();
        int[] x = new int[n];
        for(int x_i=0; x_i < n; x_i++){
            x[x_i] = in.nextInt();
        }
        
        Arrays.sort(x);
        
        int i = 0;
        int range = 0;
        int count = 0;
        
        while(i < n){
            
            if(x[i] < range){
                // current house is already in range of last transmitter
            }
            else{
                count++;

                // check where can the transmitter be placed
                int j = x[i] + k;
                int l = i;

                // transmitter can not be placed farther than j to cover current house,
                // check for the last house within j
                while(l < n && x[l] <= j){
                    l++;
                }
                
                // transmitter is placed at l-1 house
                range = x[--l] + k + 1;
                
                // move counter to l as houses till l are already in range of new transmitter
                i = l;
            }
            
            i++;
        }
        
        System.out.println(count);
    }
}
```