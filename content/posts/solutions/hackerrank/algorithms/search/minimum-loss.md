---
title: "HackerRank - Minimum Loss"
date: 2017-11-08T21:06:31+05:30
tags: ["HackerRank","Solution","Java"]
---

# Solution #1
- Keep prices and corresponding index in a `HashMap`.
- Sort the prices array in ascending order so that combination of minimum difference can be found by comparing adjacent prices.
- Check that the indexes buying and selling are in correct order so that year of buying is less than year of selling.

```java
/* Solution to HackerRank: Minimum Loss
 * URL: https://www.hackerrank.com/challenges/minimum-loss
 */
import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        
        int n = in.nextInt();
        long[] p = new long[n];
        
        Map<Long,Integer> index = new HashMap<>();
        
        for(int i=0; i < n; i++){
            p[i] = in.nextLong();
            index.put(p[i], i);
        }
        
        Arrays.sort(p);
        
        long min = Long.MAX_VALUE;
        
        for(int i=0; i < n-1; i++){
            if(p[i+1] - p[i] < min && index.get(p[i+1]) < index.get(p[i])){
                min = p[i+1] - p[i];
            }
        }
        
        System.out.println(min);
    }
}
```

# Solution #2
- Compare each possible combination to determine the minimum difference.

Test cases 11 to 15 timed out for below solution.

```java
import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        
        int n = in.nextInt();
        long[] p = new long[n];
        
        for(int i=0; i < n; i++){
            p[i] = in.nextLong();
        }
        
        long min = Long.MAX_VALUE;
        
        for(int i=0; i < n-1; i++){
            for(int j=i; j < n; j++){
                if(p[j]-p[i] < 0){
                    min = Math.min(min,p[i]-p[j]);
                }
            }
        }
        
        System.out.println(min);
    }
}
```