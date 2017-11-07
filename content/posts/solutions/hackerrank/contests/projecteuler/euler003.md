---
title: "HackerRank Contest - Project Euler - Largest Prime Factor"
date: 2017-11-06T20:56:26+05:30
tags: ["HackerRank","Solution","Java"]
---

# Solution
- Find all the factors of the given number by iterating from 1 to square root of the number.
- Sort all the factors in descending order and iterate to check if a factor is prime.

```java
/* Solution to HackerRank: Largest Prime Factor
 * URL: https://www.hackerrank.com/contests/projecteuler/challenges/euler003
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
            
            // get all the factors and sort is descending order
            List<Long> factors = getFactors(n);
            Collections.sort(factors, Collections.reverseOrder());
            
            for(Long factor: factors){
                if(isPrime(factor)){
                    System.out.println(factor);
                    break;
                }
            }
        }
    }
    
    static List<Long> getFactors(long n){
        List<Long> factors = new ArrayList<>();
        
        for(long i = 1; i <= Math.sqrt(n); i++){
            if(n%i == 0){
                factors.add(i);
                factors.add(n/i);
            }
        }
        
        return factors;
    }
    
    static boolean isPrime(long n){
        if(n%2 == 0){
            return false;
        }
        
        for(long i = 3; i <= Math.sqrt(n); i+=2){
            if(n%i == 0){
                return false;
            }
        }
        
        return true;
    }
}
```