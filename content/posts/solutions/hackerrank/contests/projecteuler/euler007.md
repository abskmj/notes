---
title: "HackerRank Contest - Project Euler - 10001st Prime"
date: 2017-11-07T07:41:06+05:30
tags: ["HackerRank","Solution","Java"]
---

# Solution
- Iterate from 2 to the given number. Consider odd numbers only except 2.
- Check each iteration for prime number.

However, below solution resulted in test case #4 to timeout.

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
            int n = in.nextInt();
            
            if(n == 1){
                System.out.println(2);
            }
            else{
                int i = 2;
                int curr = 1;
                
                while(i <= n){
                    curr += 2;
                    if(isPrime(curr)){
                        i++;
                    }
                }
                
                System.out.println(curr);
            }
        }
    }
    
    static boolean isPrime(int n){
        for(int i = 3; i <= Math.sqrt(n); i+=2){
            if(n%i == 0){
                return false;
            }
        }
        
        return true;
    }
}
```

Caching if a number is prime in a `HashMap`.

```java
/* Solution to HackerRank: 10001st Prime
 * URL: https://www.hackerrank.com/contests/projecteuler/challenges/euler007
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
            
            if(n == 1){
                System.out.println(2);
            }
            else{
                int i = 2;
                int curr = 1;
                
                while(i <= n){
                    curr += 2;
                    if(isPrime(curr)){
                        i++;
                    }
                }
                
                System.out.println(curr);
            }
        }
    }
    
    static Map<Integer,Boolean> primes = new HashMap<>();
    
    static boolean isPrime(int n){        
        if(primes.get(n) != null){
            return primes.get(n);
        }
        else{
        
            for(int i = 3; i <= Math.sqrt(n); i+=2){
                if(n%i == 0){
                    primes.put(n,false);
                    return false;
                }
            }
            
            primes.put(n,true);
            return true;
        }
    }
}
```