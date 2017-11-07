---
title: "HackerRank - Roads and Libraries"
date: 2017-10-26T11:05:14+05:30
tags: ["Graph Theory","HackerRank","Solution","Java"]
---

# Minimum Cost
- If the number of roads is zero or cost of building a road is more than cost of building a library, then building libraries in each of the cities will result in minimum cost.
- If the cost of building a library is less than cost of building a road, then building a single library and building roads to connected cities will result in minimum cost.

# Clusters
There can be few set of cities that are not connected to each other and are clusters. Minimum cost is summation of minimum cost for all clusters.

# Solution
- Each city is a vertex and each road is an undirected edge in a graph.
- DFS (Depth First Search) algorithm is used to traverse all cities in each cluster.
- Number of roads in each cluster is one less than the number of cities traversed.

```java
/* Solution to HackerRank: Roads and Libraries
 * URL: https://www.hackerrank.com/challenges/torque-and-development
 */

import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;

public class Solution {

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int q = in.nextInt();
        for(int a0 = 0; a0 < q; a0++){
            int c = in.nextInt();
            int r = in.nextInt();
            long cl = in.nextLong();
            long cr = in.nextLong();
            
            Graph graph = new Graph(c);

            for(int a1 = 0; a1 < r; a1++){
                int city_1 = in.nextInt();
                int city_2 = in.nextInt();
                
                // start index from 0
                graph.addEdge(city_1-1,city_2-1);
            }
            
            // if number of roads is 0 or cost of building a library is less than or equal to cost of building a road
            // minimum cost will be building libraries in all the cities
            if(cl <= cr || r == 0){
                System.out.println(cl*c);
            }
            else{
                boolean[] visited = new boolean[c];
                long cost = 0;
                
                // there may be more than one unconnected cluster
                for(int i = 0; i < c; i++){
                    if(!visited[i]){
                        
                        //System.out.print("Cluster: ");
                        
                        // number of roads will be one less than the vertices traversed during DFS
                        int roads = graph.dfs(i, visited)-1;
                        
                        //System.out.println("");
                        //System.out.println("Roads: "+roads);
                        
                        // cost will be building all the roads in the cluster and a library
                        cost += roads*cr;
                        cost += cl;
                    }
                }            

                System.out.println(cost); 
            }            
        }
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
    
    public int dfs(int source, boolean[] visited){
        visited[source] = true;
        int roads = 1;
        
        //System.out.print(source+" ");
        
        for(Integer vertex: vertices[source]){
            if(!visited[vertex]){
                roads += dfs(vertex, visited);
            }
        }
        
        return roads;
    }
}

```