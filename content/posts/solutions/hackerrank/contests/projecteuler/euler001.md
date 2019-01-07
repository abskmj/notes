---
title: "HackerRank Contest - Project Euler - Multiples of 3 and 5"
date: 2019-01-07T12:45:33Z
tags: ["HackerRank","Solution","Java"]
---

# Solution

```java
import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;

public class Solution {

    public static void main(String[] args) {
        
        Scanner scan  = new Scanner(System.in);
        int numCases = scan.nextInt();
        
        for(int index=0;index<numCases;index++){
            long num = scan.nextInt()-1;
            
            System.out.println(sumOfMultiples(num/3,3)+sumOfMultiples(num/5,5)-sumOfMultiples(num/15,15));
        }
    }
    
    public static long sumOfMultiples(long num, long multiple){
        return (multiple*num*(num+1))/2;
    }
}
```