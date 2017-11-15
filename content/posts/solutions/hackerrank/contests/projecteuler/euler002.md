---
title: "HackerRank Contest - Project Euler - Even Fibonacci Numbers"
date: 2017-11-04T20:36:33+05:30
tags: ["Mathematics","HackerRank","Solution","Java"]
---

# Solution #1

Test cases 2,3 timed out for below solution.

```java
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
            long n = in.nextLong();
            
            int f1 = 0;
            int f2 = 1;
            
            long sum = 0;

            while(f2 <= n){                
                // check if even
                if(f2%2 == 0){
                    sum += f2;
                }
                
                // compute next in series
                int f = f2 + f1;
                
                // set values for next iteration
                f1 = f2;
                f2 = f;
            }
            
            System.out.println(sum);
        }
    }
}
```

# Solution #2

- Every 3rd number in the fibonacci series is even. This is based on the fact that sum of a odd and an even number is always odd and sum of 2 odd numbers is always even.
- This fact results in a formula `F(n) = 4(n-1) + F(n-2)`, where F(n) represents the even numbered fibonacci series.

```
0 1 1 2 3 5 8 13 21 34 55 89 
      ^     ^        ^
0 1 2 3 4 5 6  7  8  9 10 11 ===> f(n), fibonacci series

0     1     2        3       ===> F(n) = f(3n), even numbered fibonacci series

F(2)
= f(6)
= f(5) + f(4)
= f(4) + f(3) + f(4)
= 2f(4) + f(3) => f(n) = 2f(n-2) + f(n-3) => f(3) = 2f(1) + f(0) ===> eq1
= 2f(3) + 2f(2) + f(3)
= 3f(3) + 2f(1) + 2f(0)    
using values from eq1
= 3f(3) + f(3) + f(0)
= 4f(3) + f(0)
= 4F(1) + F(0) => F(n) = 4F(n-1) + 4F(n-2)
```
Using the above formula

```java
/* Solution to HackerRank: Even Fibonacci Numbers
 * URL: https://www.hackerrank.com/contests/projecteuler/challenges/euler002
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
            long n = in.nextLong();
            
            long f1 = 0;
            long f2 = 2;
            
            long sum = 0;

            while(f2 <= n){
                sum += f2;
                
                // compute next even number in series
                long f = 4*f2 + f1;
                
                // set values for next iteration
                f1 = f2;
                f2 = f;
            }
            
            System.out.println(sum);
        }
    }
}
```