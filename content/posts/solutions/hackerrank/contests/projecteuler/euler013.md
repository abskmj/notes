---
title: "HackerRank Contest - Project Euler - Large Sum"
date: 2017-12-08T16:21:47+05:30
tags: ["HackerRank","Solution","Java"]
---

# Solution
- Use `BigInteger` to calculate the sum and print first 10 characters by converting to string.

```java
/* Solution to HackerRank: Large Sum
 * URL: https://www.hackerrank.com/contests/projecteuler/challenges/euler013
 */
import java.io.*;
import java.util.*;
import java.math.*;

public class Solution {

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        
        int N = in.nextInt();
        
        BigInteger sum = new BigInteger("0");
        
        for(int t=0; t<N; t++){
            sum = sum.add(new BigInteger(in.next()));
        }
        
        System.out.println(sum.toString().substring(0, 10));
    }
}
```