---
title: "HackerRank Contest - HourRank 24 - Mutual Indivisibility"
date: 2017-11-08T20:54:03+05:30
tags: ["HackerRank","Solution","Java"]
---

# Solution #1
- Iterate through each combination of two and check if smaller is factor of bigger number.
- A given number is potential answer if number of times it is a factor is 0.

Test case 11 to 25 timed out for below solution.

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
            int a = in.nextInt();
            int b = in.nextInt();
            int x = in.nextInt();
            
            int offset = b-a;
            
            int[] check = new int[offset+1];
            
            // calculate the number of times i is factor of j
            for(int i = a; i < b; i++){
                for(int j = i+1; j <=b; j++){
                    if(j%i == 0){
                        check[i-a]++;
                    }
                }
            }
            
            List<Integer> answer = new ArrayList<>();
            
            // add to the answer list if value is zero
            for(int i=0; i < check.length; i++){
                if(check[i] == 0){
                    answer.add(i+a);
                }
            }
            
            if(answer.size() >= x){
                for(int i=0; i < x; i++){
                    System.out.print(answer.get(i)+" ");
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

# Solution #2
- Iterate through each number one by one.
- If current number is divisible by any of the potential answer list, then remove it.
- Add current number to the potential answer list.
- Break the loop if size of potential answer list is equal to the expected size.

Test case 11 to 25 timed out for below solution as well.

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
            int a = in.nextInt();
            int b = in.nextInt();
            int x = in.nextInt();
            
            boolean noAns = true;
            
            List<Integer> list = new ArrayList<>();
            
            list.add(a);
            
            while(a++ <= b){
                List<Integer> list1 = new ArrayList<>();
                for(int num: list){
                    if(a%num == 0){

                    }
                    else{
                        list1.add(num);
                    }
                }
                
                list = list1;
                
                list.add(a);
                
                if(list.size() == x){
                    noAns = false;
                    
                    for(int num: list){
                        System.out.print(num+" ");
                    }
                    
                    System.out.println("");
                    break;
                }
            }
            
            if(noAns){
                System.out.println(-1);
            }
            
        }
        in.close();
    }
}
```