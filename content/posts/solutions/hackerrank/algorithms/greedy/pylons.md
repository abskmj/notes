---
title: "HackerRank - Goodland Electricity"
date: 2017-11-18T20:30:35+05:30
tags: ["HackerRank","Solution","Java"]
---

# Solution
- Iterate through each city and check if it is already under range of previous tower.
- If not, find a tower within the range to switch on.

```java
/* Solution to HackerRank: Goodland Electricity
 * URL: https://www.hackerrank.com/challenges/pylons
 */
import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        
        int N = in.nextInt();
        int K = in.nextInt();
        
        int[] cities = new int[N];
        
        for(int i=0; i < N; i++){
            cities[i] = in.nextInt();
        }
        
        int index = 0;
        int range = 0;
        int changes = 0;
        
        while(index < N){
            
            if(index < range){
                // city is already in range                
            }
            else{
                // find a tower to switch on
                
                int towerEnd = index+K;
                int towerStart = index-K+1;
                if(towerStart < 0){
                    towerStart = 0;
                }
                int tower = -1;
                
                for(int j=towerStart; j<towerEnd && j<N; j++){
                    if(cities[j] == 1){
                        tower = j;
                    }
                }
                
                // no way to handle current city
                if(tower == -1){
                    System.out.println(-1);
                    return;
                }
                else{
                    changes++;
                    index = tower;
                    range = index + K;
                }
            }
            
            index++;
        }
        
        System.out.println(changes);
    }
}
```