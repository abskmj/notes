---
title: "HackerRank Contest - Project Euler - Power Digit Sum" 
date: 2017-12-08T16:03:31+05:30
tags: ["HackerRank","Solution","Java"]
---

# Solution
- 2 to the power 1000 will be a huge number hence consider using `BigInteger`.
- Recursively calculate the sum of all the digits.


```java
/* Solution to HackerRank: Power Digit Sum
 * URL: https://www.hackerrank.com/contests/projecteuler/challenges/euler016
 */

import java.io.*;
import java.util.*;
import java.math.*;

public class Solution {

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int T = in.nextInt();
        
        for(int t=0; t<T; t++){
            int N = in.nextInt();
            
            BigInteger base = new BigInteger("2");
            
            BigInteger pow = base.pow(N);
            
            System.out.println(digitSum(pow));
        }
    }
    
    public static BigInteger digitSum(BigInteger n){
        BigInteger ten = new BigInteger("10"); 
        
        if(n.compareTo(ten) == -1){
            // if number is less than 10 then it is reduced to single digit, hence return the digit
            return n;
        }
        else{            
            BigInteger r[] = n.divideAndRemainder(ten);
            
            // r[0] is the quotient and r[1] is the remainder
            return digitSum(r[0]).add(r[1]);
        }
    }
}
```