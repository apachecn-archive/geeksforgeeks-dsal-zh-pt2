# 使用给定的操作最小化无向图所有顶点的颜色成本

> 原文:[https://www . geeksforgeeks . org/使用给定操作最小化无向图的所有顶点的颜色成本/](https://www.geeksforgeeks.org/minimize-cost-to-color-all-the-vertices-of-an-undirected-graph-using-given-operation/)

给定两个整数 **V** 和 **E** 表示无向图 **G(V，E)** 的顶点和边的数量，一个边列表 **EdgeList** ，以及一个数组**A【】**表示给每个节点着色的成本，任务是使用以下操作找到给图着色的最小成本:

> 当一个**节点**被着色时，从它可以到达的所有节点都被着色，而没有任何额外的成本。

**示例:**

> **输入:** V = 6，E = 5，A[] = {12，25，8，11，10，7}，EdgeList = {{1，2}，{1，3}，{3，2}，{2，5}，{4，6}}
> **输出:** 15
> **解释:**
> 在为顶点 3 着色时，成本为 **8** ，顶点{1，2，5}被着色
> 在以 **7** 的代价对顶点 6 着色时，唯一剩余的顶点{4}也被着色。
> 因此，最小成本= 8 + 7 = 15。
> 
> **输入:** V =7，E = 6，A[] = {3，5，8，6，9，11，10}，EdgeList = {{1，4}，{2，1}，{2，7}，{3，4}，{3，5}，{5，6}}
> **输出:** 5

**方法:**
按照以下步骤解决问题:

*   所有节点都可以从一个给定的节点到达，形成一个[连接组件](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)。
*   因此，对于每个连接的组件，使用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)，找到图的连接组件中的最小成本节点。

下面是上述方法的实现:

## C++

```
// C++ Program to find the minimum
// cost to color all vertices of an
// Undirected Graph
#include <bits/stdc++.h>
using namespace std;

#define MAX 10

vector<int> adj[MAX];

// Function to add edge in the
// given graph
void addEdge(int u, int v)
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

// Function to perform DFS traversal and
// find the node with minimum cost
void dfs(int v, int cost[], bool vis[],
         int& min_cost_node)
{
    vis[v] = true;

    // Update the minimum cost
    min_cost_node
        = min(min_cost_node, cost[v - 1]);

    for (int i = 0; i < adj[v].size(); i++) {

        // Recur for all connected nodes
        if (vis[adj[v][i]] == false) {
            dfs(adj[v][i], cost, vis,
                min_cost_node);
        }
    }
}

// Function to calculate and return
// the minimum cost of coloring all
// vertices of the Undirected Graph
int minimumCost(int V, int cost[])
{

    // Marks if a vertex is
    // visited or not
    bool vis[V + 1];

    // Initialize all vertices as unvisited
    memset(vis, false, sizeof(vis));
    int min_cost = 0;

    // Perform DFS traversal
    for (int i = 1; i <= V; i++) {

        // If vertex is not visited
        if (!vis[i]) {
            int min_cost_node = INT_MAX;
            dfs(i, cost, vis, min_cost_node);

            // Update minimum cost
            min_cost += min_cost_node;
        }
    }

    // Return the final cost
    return min_cost;
}
// Driver Code
int main()
{
    int V = 6, E = 5;
    int cost[] = { 12, 25, 8, 11, 10, 7 };
    addEdge(1, 2);
    addEdge(1, 3);
    addEdge(3, 2);
    addEdge(2, 5);
    addEdge(4, 6);

    int min_cost = minimumCost(V, cost);

    cout << min_cost << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum
// cost to color all vertices of an
// Undirected Graph
import java.util.*;

class GFG{

static final int MAX = 10;

@SuppressWarnings("unchecked")
static Vector<Integer> []adj = new Vector[MAX];

static int min_cost_node;

// Function to add edge in the
// given graph
static void addEdge(int u, int v)
{
    adj[u].add(v);
    adj[v].add(u);
}

// Function to perform DFS traversal and
// find the node with minimum cost
static void dfs(int v, int cost[], boolean vis[])
{
    vis[v] = true;

    // Update the minimum cost
    min_cost_node = Math.min(min_cost_node,
                             cost[v - 1]);

    for(int i = 0; i < adj[v].size(); i++)
    {

        // Recur for all connected nodes
        if (vis[adj[v].get(i)] == false)
        {
            dfs(adj[v].get(i), cost, vis);
        }
    }
}

// Function to calculate and return
// the minimum cost of coloring all
// vertices of the Undirected Graph
static int minimumCost(int V, int cost[])
{

    // Marks if a vertex is
    // visited or not
    boolean []vis = new boolean[V + 1];

    // Initialize all vertices as unvisited
    Arrays.fill(vis, false);
    int min_cost = 0;

    // Perform DFS traversal
    for(int i = 1; i <= V; i++)
    {

        // If vertex is not visited
        if (!vis[i])
        {
            min_cost_node = Integer.MAX_VALUE;
            dfs(i, cost, vis);

            // Update minimum cost
            min_cost += min_cost_node;
        }
    }

    // Return the final cost
    return min_cost;
}

// Driver Code
public static void main(String[] args)
{
    int V = 6, E = 5;
    int cost[] = { 12, 25, 8, 11, 10, 7 };

    for(int i = 0; i < adj.length; i++)
        adj[i] = new Vector<Integer>();

    addEdge(1, 2);
    addEdge(1, 3);
    addEdge(3, 2);
    addEdge(2, 5);
    addEdge(4, 6);

    int min_cost = minimumCost(V, cost);

    System.out.print(min_cost + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# cost to color all vertices of an
# Undirected Graph
import sys

MAX = 10

adj = [[] for i in range(MAX)]

# Function to add edge in the
# given graph
def addEdge(u, v):

    adj[u].append(v)
    adj[v].append(u)

# Function to perform DFS traversal and
# find the node with minimum cost
def dfs(v, cost, vis, min_cost_node):

    vis[v] = True

    # Update the minimum cost
    min_cost_node = min(min_cost_node,
                        cost[v - 1])

    for i in range(len(adj[v])):

        # Recur for all connected nodes
        if (vis[adj[v][i]] == False):
            min_cost_node = dfs(adj[v][i],
                                cost, vis,
                                min_cost_node)

    return min_cost_node

# Function to calculate and return
# the minimum cost of coloring all
# vertices of the Undirected Graph
def minimumCost(V, cost):

    # Marks if a vertex is
    # visited or not
    vis = [False for i in range(V + 1)]

    min_cost = 0

    # Perform DFS traversal
    for i in range(1, V + 1):

        # If vertex is not visited
        if (not vis[i]):
            min_cost_node = sys.maxsize
            min_cost_node = dfs(i, cost, vis,
                                min_cost_node)

            # Update minimum cost
            min_cost += min_cost_node

    # Return the final cost
    return min_cost

# Driver Code
if __name__=="__main__":

    V = 6
    E = 5
    cost = [ 12, 25, 8, 11, 10, 7 ]

    addEdge(1, 2)
    addEdge(1, 3)
    addEdge(3, 2)
    addEdge(2, 5)
    addEdge(4, 6)

    min_cost = minimumCost(V, cost)

    print(min_cost)

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find the minimum
// cost to color all vertices of an
// Undirected Graph
using System;
using System.Collections.Generic;

class GFG{

static readonly int MAX = 10;
static List<int> []adj = new List<int>[MAX];
static int min_cost_node;

// Function to add edge in the
// given graph
static void addEdge(int u, int v)
{
    adj[u].Add(v);
    adj[v].Add(u);
}

// Function to perform DFS traversal and
// find the node with minimum cost
static void dfs(int v, int []cost, bool []vis)
{
    vis[v] = true;

    // Update the minimum cost
    min_cost_node = Math.Min(min_cost_node,
                             cost[v - 1]);

    for(int i = 0; i < adj[v].Count; i++)
    {

        // Recur for all connected nodes
        if (vis[adj[v][i]] == false)
        {
            dfs(adj[v][i], cost, vis);
        }
    }
}

// Function to calculate and return
// the minimum cost of coloring all
// vertices of the Undirected Graph
static int minimumCost(int V, int []cost)
{

    // Marks if a vertex is
    // visited or not
    bool []vis = new bool[V + 1];

    int min_cost = 0;

    // Perform DFS traversal
    for(int i = 1; i <= V; i++)
    {

        // If vertex is not visited
        if (!vis[i])
        {
            min_cost_node = int.MaxValue;
            dfs(i, cost, vis);

            // Update minimum cost
            min_cost += min_cost_node;
        }
    }

    // Return the readonly cost
    return min_cost;
}

// Driver Code
public static void Main(String[] args)
{
    int V = 6;
    int []cost = { 12, 25, 8, 11, 10, 7 };

    for(int i = 0; i < adj.Length; i++)
        adj[i] = new List<int>();

    addEdge(1, 2);
    addEdge(1, 3);
    addEdge(3, 2);
    addEdge(2, 5);
    addEdge(4, 6);

    int min_cost = minimumCost(V, cost);

    Console.Write(min_cost + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript Program to find the minimum
// cost to color all vertices of an
// Undirected Graph

var MAX = 10

var adj = Array.from(Array(MAX), ()=> Array());

// Function to add edge in the
// given graph
function addEdge(u, v)
{
    adj[u].push(v);
    adj[v].push(u);
}

// Function to perform DFS traversal and
// find the node with minimum cost
function dfs(v, cost, vis, min_cost_node)
{
    vis[v] = true;

    // Update the minimum cost
    min_cost_node
        = Math.min(min_cost_node, cost[v - 1]);

    for (var i = 0; i < adj[v].length; i++) {

        // Recur for all connected nodes
        if (vis[adj[v][i]] == false) {
            min_cost_node = dfs(adj[v][i], cost, vis,
                min_cost_node);
        }
    }
    return min_cost_node;
}

// Function to calculate and return
// the minimum cost of coloring all
// vertices of the Undirected Graph
function minimumCost(V, cost)
{

    // Marks if a vertex is
    // visited or not
    var vis = Array(V + 1).fill(false);

    var min_cost = 0;

    // Perform DFS traversal
    for (var i = 1; i <= V; i++) {

        // If vertex is not visited
        if (!vis[i]) {
            var min_cost_node = 1000000000;
            min_cost_node = dfs(i, cost, vis, min_cost_node);

            // Update minimum cost
            min_cost += min_cost_node;
        }
    }

    // Return the final cost
    return min_cost;
}
// Driver Code

var V = 6, E = 5;
var cost = [12, 25, 8, 11, 10, 7];
addEdge(1, 2);
addEdge(1, 3);
addEdge(3, 2);
addEdge(2, 5);
addEdge(4, 6);
var min_cost = minimumCost(V, cost);
document.write( min_cost );

</script>
```

**输出:**

```
15
```

***时间复杂度:** O(V+E)*
***辅助空间:** O(V)*