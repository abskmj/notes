---
title: "HackerRank Contest - Project Euler - Sum Square Difference"
date: 2017-11-07T07:19:29+05:30
tags: ["HackerRank","Solution","Java"]
---

# Solution
- Iterate from 1 to given number.
- Add each iteration to sum and square of it to another sum.
- Print absolute difference.

```java
/* Solution to HackerRank: Sum Square Difference
 * URL: https://www.hackerrank.com/contests/projecteuler/challenges/euler006
 */
import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;

public class Solution {

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int t = in.nextInt();
        for(int a0 = 0; a0 < t; a0++){
            int n = in.nextInt();
            
            long squareSum = 0;
            long sum = 0;
            
            for(int i = 1; i <= n; i++){
                squareSum+=(i*i);
                sum+=i;
            }
            
            System.out.println(Math.abs(sum*sum-squareSum));
        }
    }
}
```