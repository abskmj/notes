---
title: "HackerRank - Journey to the Moon"
date: 2017-10-29T23:20:35+05:30
tags: ["Graph Theory","HackerRank","Solution","Java"]
---

# Solution
- Graph is used to connect all astronauts to a country.
- Each cluster of graph represents a country.
- Each cluster is traversed to find the count of astronauts.
- Number of possible combinations are calculated based on sizes of these countries.

```java
/* Solution to HackerRank: Journey to the Moon
 * URL: https://www.hackerrank.com/challenges/journey-to-the-moon
 */

import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        
        int N = in.nextInt();
        
        Graph graph = new Graph(N);
        
        int P = in.nextInt();
        
        for(int i = 0; i < P; i++){
            int source = in.nextInt();
            int destination = in.nextInt();
            
            graph.addEdge(source,destination);
        }
        
        
        boolean[] visited = new boolean[N];
        List<Integer> countries = new ArrayList<Integer>();
        long combinations = 0;

        // store size of each country by traversing each cluster
        for(int i = 0; i < N; i++){
            if(!visited[i]){
                countries.add(graph.dfs(i, visited));
            }
        }

        // calculating combinations with double caused test case #11 to timeout
        /*for(int i = 0; i < clusters.size()-1; i++){
            for (int j = i + 1; j < clusters.size(); j++){
                combinations += clusters.get(i) * clusters.get(j);
            }
        }*/
        
        /* Let size of each country be A, B, C, D ...
         * Combinations: AB + AC + AD + BC + BD + CD + ...
         * => AB + (A+B)C + (A+B+C)D
         */
        int sum = 0;
        for(int country : countries){
            combinations += sum*country;
            sum += country;    
        } 

        System.out.println(combinations);
    }
}
    
class Graph{
    List<Integer>[] vertices;
    
    public Graph(int count){
        vertices = new ArrayList[count];
        
        for(int i = 0; i < count; i++){
            vertices[i] = new ArrayList<Integer>();
        }
    }
    
    public void addEdge(int source, int destination){
        vertices[source].add(destination);
        vertices[destination].add(source);
    }
    
    // modified DFS to return number of vertices traversed
    public int dfs(int source, boolean[] visited){
        visited[source] = true;
        int count = 1;
        
        for(Integer vertex: vertices[source]){
            if(!visited[vertex]){
                count += dfs(vertex, visited);
            }
        }
        
        return count;
    }
}
```