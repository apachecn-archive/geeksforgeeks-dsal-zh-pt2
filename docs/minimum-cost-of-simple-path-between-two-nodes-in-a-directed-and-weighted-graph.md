# 有向加权图中两个节点间简单路径的最小代价

> 原文:[https://www . geesforgeks . org/有向加权图中两个节点之间简单路径的最小成本/](https://www.geeksforgeeks.org/minimum-cost-of-simple-path-between-two-nodes-in-a-directed-and-weighted-graph/)

给定一个可能包含循环的**有向图**，其中**每条边都有权重**，任务是找到从给定源顶点到给定目的顶点的任何简单路径的最小代价。简单路径是从一个顶点到另一个顶点的路径，这样顶点不会被访问超过一次。如果没有简单的路径，那么返回 INF(无限)。

该图被给出为[邻接矩阵表示](https://www.geeksforgeeks.org/graph-and-its-representations/)，其中图[i][j]的值指示从顶点 I 到顶点 j 的边的权重，值 INF(无穷大)指示从 I 到 j 没有边。

**示例:**

```
Input : V = 5, E = 6
        s = 0, t = 2
    graph[][] =      0   1   2   3   4  
                 0  INF -1  INF  1  INF
                 1  INF INF -2  INF INF
                 2  -3  INF INF INF INF
                 3  INF INF -1  INF INF
                 4  INF INF INF  2  INF

Output : -3 
Explanation : 
The minimum cost simple path between 0 and 2 is given by:
0 -----> 1 ------> 2 whose cost is (-1) + (-2) = (-3). 

Input : V = 5, E = 6
        s = 0, t = 4
    graph[][] =      0   1   2   3   4  
                 0  INF -7  INF -2  INF
                 1  INF INF -11 INF INF
                 2  INF INF INF INF INF
                 3  INF INF INF  3  -4
                 4  INF INF INF INF INF

Output : -6
Explanation : 
The minimum cost simple path between 0 and 2 is given by:
0 -----> 3 ------> 4 whose cost is (-2) + (-4) = (-6). 
```

**方法:**
解决上述问题的主要思想是使用**深度优先搜索**的修改版本遍历从 s 到 t 的所有简单路径，并在其中找到最小成本路径。关于 DFS 的一个重要观察是，它一次遍历一条路径，因此我们可以使用 DFS 通过在离开节点之前将它们标记为未访问来独立遍历单独的路径。
一个简单的解决方法是从 s 开始，到所有相邻的顶点，对进一步相邻的顶点进行递归，直到我们到达目的地。即使图中存在负权重循环或自边，该算法也能工作。

以下是上述方法的实施情况:

## C++

```
// C++ code for printing Minimum Cost
// Simple Path between two given nodes
// in a directed and weighted graph
#include <bits/stdc++.h>
using namespace std;

// Define number of vertices in
// the graph and infinite value
#define V 5
#define INF INT_MAX

// Function to do DFS through the nodes
int minimumCostSimplePath(int u, int destination,
                    bool visited[], int graph[][V])
{

    // check if we find the destination
    // then further cost will be 0
    if (u == destination)
        return 0;

    // marking the current node as visited
    visited[u] = 1;

    int ans = INF;

    // traverse through all
    // the adjacent nodes
    for (int i = 0; i < V; i++) {
        if (graph[u][i] != INF && !visited[i]) {

            // cost of the further path
            int curr = minimumCostSimplePath(i,
                        destination, visited, graph);

            // check if we have reached the destination
            if (curr < INF) {

                // Taking the minimum cost path
                ans = min(ans, graph[u][i] + curr);
            }
        }
    }

    // unmarking the current node
    // to make it available for other
    // simple paths
    visited[u] = 0;

    // returning the minimum cost
    return ans;
}

// driver code
int main()
{

    // initialising the graph
    int graph[V][V];
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            graph[i][j] = INF;
        }
    }

    // marking all nodes as unvisited
    bool visited[V] = { 0 };

    // initialising the edges;
    graph[0][1] = -1;
    graph[0][3] = 1;
    graph[1][2] = -2;
    graph[2][0] = -3;
    graph[3][2] = -1;
    graph[4][3] = 2;

    // source and destination
    int s = 0, t = 2;

    // marking the source as visited
    visited[s] = 1;

    cout << minimumCostSimplePath(s, t,
                            visited, graph);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for printing Minimum Cost
// Simple Path between two given nodes
// in a directed and weighted graph
import java.util.*;
import java.lang.*;

class GFG{

// Define number of vertices in
// the graph and infinite value
static int V = 5;
static int INF = Integer.MAX_VALUE;

// Function to do DFS through the nodes
static int minimumCostSimplePath(int u, int destination,
                                 boolean visited[],
                                 int graph[][])
{

    // Check if we find the destination
    // then further cost will be 0
    if (u == destination)
        return 0;

    // Marking the current node as visited
    visited[u] = true;

    int ans = INF;

    // Traverse through all
    // the adjacent nodes
    for(int i = 0; i < V; i++)
    {
        if (graph[u][i] != INF && !visited[i])
        {

            // Cost of the further path
            int curr = minimumCostSimplePath(i,
                        destination, visited, graph);

            // Check if we have reached the
            // destination
            if (curr < INF)
            {

                // Taking the minimum cost path
                ans = Math.min(ans, graph[u][i] + curr);
            }
        }
    }

    // Unmarking the current node
    // to make it available for other
    // simple paths
    visited[u] = false;

    // Returning the minimum cost
    return ans;
}  

// Driver code
public static void main(String[] args)
{

    // Initialising the graph
    int graph[][] = new int[V][V];
    for(int i = 0; i < V; i++)
    {
        for(int j = 0; j < V; j++)
        {
            graph[i][j] = INF;
        }
    }

    // Marking all nodes as unvisited
    boolean visited[] = new boolean[V];

    // Initialising the edges;
    graph[0][1] = -1;
    graph[0][3] = 1;
    graph[1][2] = -2;
    graph[2][0] = -3;
    graph[3][2] = -1;
    graph[4][3] = 2;

    // Source and destination
    int s = 0, t = 2;

    // Marking the source as visited
    visited[s] = true;

    System.out.println(minimumCostSimplePath(s, t,
                            visited, graph));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 code for printing Minimum Cost
# Simple Path between two given nodes
# in a directed and weighted graph
import sys

V = 5
INF = sys.maxsize

# Function to do DFS through the nodes
def minimumCostSimplePath(u, destination,
                          visited, graph):

    # Check if we find the destination
    # then further cost will be 0
    if (u == destination):
        return 0

    # Marking the current node as visited
    visited[u] = 1

    ans = INF

    # Traverse through all
    # the adjacent nodes
    for i in range(V):
        if (graph[u][i] != INF and not visited[i]):

            # Cost of the further path
            curr = minimumCostSimplePath(i, destination,
                                         visited, graph)

            # Check if we have reached the destination
            if (curr < INF):

                # Taking the minimum cost path
                ans = min(ans, graph[u][i] + curr)

    # Unmarking the current node
    # to make it available for other
    # simple paths
    visited[u] = 0

    # Returning the minimum cost
    return ans

# Driver code
if __name__=="__main__":

    # Initialising the graph
    graph = [[INF for j in range(V)]
                  for i in range(V)]

    # Marking all nodes as unvisited
    visited = [0 for i in range(V)]

    # Initialising the edges
    graph[0][1] = -1
    graph[0][3] = 1
    graph[1][2] = -2
    graph[2][0] = -3
    graph[3][2] = -1
    graph[4][3] = 2

    # Source and destination
    s = 0
    t = 2

    # Marking the source as visited
    visited[s] = 1

    print(minimumCostSimplePath(s, t, visited, graph))

# This code is contributed by rutvik_56
```

## C#

```
// C# code for printing Minimum Cost
// Simple Path between two given nodes
// in a directed and weighted graph
using System;
using System.Collections;
using System.Collections.Generic;
class GFG
{

    // Define number of vertices in
    // the graph and infinite value
    static int V = 5;
    static int INF = int.MaxValue;

    // Function to do DFS through the nodes
    static int minimumCostSimplePath(int u, int destination,
                                     bool[] visited, int[, ] graph)
    {

        // Check if we find the destination
        // then further cost will be 0
        if (u == destination)
            return 0;

        // Marking the current node as visited
        visited[u] = true;
        int ans = INF;

        // Traverse through all
        // the adjacent nodes
        for (int i = 0; i < V; i++)
        {
            if (graph[u, i] != INF && !visited[i])
            {

                // Cost of the further path
                int curr = minimumCostSimplePath(i, destination,
                                                 visited, graph);

                // Check if we have reached the
                // destination
                if (curr < INF)
                {

                    // Taking the minimum cost path
                    ans = Math.Min(ans, graph[u, i] + curr);
                }
            }
        }

        // Unmarking the current node
        // to make it available for other
        // simple paths
        visited[u] = false;

        // Returning the minimum cost
        return ans;
    }

    // Driver code
    public static void Main(string[] args)
    {

        // Initialising the graph
        int[, ] graph = new int[V, V];
        for (int i = 0; i < V; i++)
        {
            for (int j = 0; j < V; j++)
            {
                graph[i, j] = INF;
            }
        }

        // Marking all nodes as unvisited
        bool[] visited = new bool[V];

        // Initialising the edges;
        graph[0, 1] = -1;
        graph[0, 3] = 1;
        graph[1, 2] = -2;
        graph[2, 0] = -3;
        graph[3, 2] = -1;
        graph[4, 3] = 2;

        // Source and destination
        int s = 0, t = 2;

        // Marking the source as visited
        visited[s] = true;
        Console.WriteLine(minimumCostSimplePath(s, t, visited, graph));
    }
}

// This code is contributed by sanjeev2552
```

## java 描述语言

```
<script>

// JavaScript code for printing Minimum Cost
// Simple Path between two given nodes
// in a directed and weighted graph

// Define number of vertices in
// the graph and infinite value
let V = 5
let INF =  Number.MAX_SAFE_INTEGER

// Function to do DFS through the nodes
function minimumCostSimplePath(u, destination, visited, graph)
{

    // check if we find the destination
    // then further cost will be 0
    if (u == destination)
        return 0;

    // marking the current node as visited
    visited[u] = 1;

    let ans = INF;

    // traverse through all
    // the adjacent nodes
    for (let i = 0; i < V; i++) {
        if (graph[u][i] != INF && !visited[i]) {

            // cost of the further path
            let curr = minimumCostSimplePath(i,
                        destination, visited, graph);

            // check if we have reached the destination
            if (curr < INF) {

                // Taking the minimum cost path
                ans = Math.min(ans, graph[u][i] + curr);
            }
        }
    }

    // unmarking the current node
    // to make it available for other
    // simple paths
    visited[u] = 0;

    // returning the minimum cost
    return ans;
}

// driver code

    // initialising the graph
    let graph = new Array();
    for(let i = 0;  i< V; i++){
        graph.push([])
    }

    for (let i = 0; i < V; i++) {
        for (let j = 0; j < V; j++) {
            graph[i][j] = INF;
        }
    }

    // marking all nodes as unvisited
    let visited = new Array(V).fill(0);

    // initialising the edges;
    graph[0][1] = -1;
    graph[0][3] = 1;
    graph[1][2] = -2;
    graph[2][0] = -3;
    graph[3][2] = -1;
    graph[4][3] = 2;

    // source and destination
    let s = 0, t = 2;

    // marking the source as visited
    visited[s] = 1;

    document.write(minimumCostSimplePath(s, t, visited, graph));

    // This code is contributed by _saurabh_jaiswal

    </script>
```

**Output:** 

```
-3
```