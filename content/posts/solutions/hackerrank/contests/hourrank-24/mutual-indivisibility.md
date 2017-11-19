---
title: "HackerRank Contest - HourRank 24 - Mutual Indivisibility"
date: 2017-11-08T20:54:03+05:30
tags: ["HackerRank","Solution","Java"]
---

# Solution
- Start iterating numbers from b to a because combination of larger numbers are more likely to be indivisible.
- Keep an array representing all numbers including a and b.
- Strike out multiples of current number from array in each iteration.

```java
/* Solution to HackerRank: Mutual Indivisibility
 * URL: https://www.hackerrank.com/contests/hourrank-24/challenges/mutual-indivisibility
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
            int a = in.nextInt();
            int b = in.nextInt();
            int x = in.nextInt();
            
            int[] skills =  new int[b-a+1];
            
            int teamSize = 0;
            
            for(int i=b; i>=a; i--){
                teamSize++;
                    
                int multiple = i*2;
                int count = 2;

                while(multiple <= b){
                    // strike out the multiple, hence decrease team size
                    skills[multiple-a] = 1;
                    teamSize--;

                    count++;
                    multiple = i*count;
                }
                
                // break as needed team size is reached
                if(teamSize == x){
                    break;
                }
            }        
            
            
            if(teamSize >= x){
                int i = skills.length-1;
                
                while(i >= 0 && x > 0){
                   if(skills[i] == 0){
                       System.out.print(i+a);
                       System.out.print(" ");
                       x--;
                   }
                   i--;
                }
                
                System.out.println("");
            }
            else{
                System.out.println(-1);
            }
            
        }
        in.close();
    }
}

```