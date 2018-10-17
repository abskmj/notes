---
title: "HackerRank - The Time in Words"
date: 2018-09-10T07:16:41Z
tags: ["HackerRank","Solution","Java"]
---

# Solution

```java
/* Solution to HackerRank: The Time in Words
 * URL: https://www.hackerrank.com/challenges/the-time-in-words
 */
import java.io.*;
import java.math.*;
import java.security.*;
import java.text.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.regex.*;

public class Solution {

    // Complete the timeInWords function below.
    static String timeInWords(int h, int m) {
        String[] words = {"zero", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten", "eleven", "twelve", "thirteen", "fourteen", "fifteen", "sixteen", "seventeen", "eighteen", "nineteen", "twenty"};
        
        if (m == 0){
            return words[h] + " o' clock";
        } else if (m == 15){
            return "quarter past " + words[h];
        } else if (m == 30){
            return "half past " + words[h];
        } else if (m == 45){
            return "quarter to " + words[h+1];
        } else if (m == 1){
            return "one minute past " + words[h];
        } else if (m == 59){
            return "one minute to " + words[h+1];
        } else if (m < 21){
            return words[m] + " minutes past " + words[h];
        } else if (m > 39){
            return words[60-m] + " minutes to " + words[h+1];
        } else if (m > 30){
            return "twenty " + words[(60-m)%20] + " minutes to " + words[h+1];
        }
        else{            
            return "twenty " + words[m%20] + " minutes past " + words[h];
        }

    }

    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) throws IOException {
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int h = scanner.nextInt();
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");

        int m = scanner.nextInt();
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");

        String result = timeInWords(h, m);

        bufferedWriter.write(result);
        bufferedWriter.newLine();

        bufferedWriter.close();

        scanner.close();
    }
}
```