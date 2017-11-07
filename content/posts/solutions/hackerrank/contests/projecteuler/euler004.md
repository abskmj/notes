---
title: "HackerRank Contest - Project Euler - Largest Palindrome"
date: 2017-11-06T22:01:58+05:30
tags: ["HackerRank","Solution","Java"]
---

# Solution
- Iterate from the given number to zero.
- Check if current iteration is a palindrome by using `reverse()` of `StringBuilder` class.
- Check if current iteration is a product of two 3-digit numbers.

```java
/* Solution to HackerRank: Largest Palindrome
 * URL: https://www.hackerrank.com/contests/projecteuler/challenges/euler004
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
            
            // decrease n by 1 for first iteration, this will handle test case #3
            while(n-- > 0){
                if(isPalindrome(n) && isProduct(n)){
                    System.out.println(n);
                    break;
                }
            }
        }
    }
    
    static boolean isPalindrome(int n){
        String forward = Integer.toString(n);
        
        return new StringBuilder(forward).reverse().toString().equals(forward);
    }
    
    static boolean isProduct(int n){
        // set boundary value for a 3-digit number
        for(int i = 100; i < 1000; i++){
            // check if the other factor is a 3-digit number
            if(n%i == 0 && n/i > 99 && n/i < 1000){
                return true;
            }
        }
        
        return false;
    }
}
```