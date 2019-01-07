---
title: "HackerRank Contest - Project Euler - Largest product in a series"
date: 2019-01-07T12:50:58Z
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
        Scanner scan = new Scanner(System.in);
        int T = scan.nextInt();
        
        for(int j=0;j<T;j++){
            int N = scan.nextInt();
            int K = scan.nextInt();
            scan.nextLine();
        
            char[] data = scan.nextLine().toCharArray();
        
            int max = 0;
        
            for(int i=0;i<N-K;i++){
                int prod = getProduct(data,i,K);
            
                if(prod>max){
                    max = prod;
                }
            }
        
            System.out.println(max);
        }
        
    }
    
    static int getProduct(char[] data, int start, int length){
        int product = 1;
        
        for(int i=start;i<start+length;i++){
            product = product * Character.getNumericValue(data[i]);
        }
        
        return product;
    }
}
```