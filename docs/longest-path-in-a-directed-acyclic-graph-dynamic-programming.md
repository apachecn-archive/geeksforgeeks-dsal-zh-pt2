# 有向无环图中的最长路径|动态规划

> 原文:[https://www . geesforgeks . org/有向无环图中最长路径-动态编程/](https://www.geeksforgeeks.org/longest-path-in-a-directed-acyclic-graph-dynamic-programming/)

给定一个有向图 **G** ，其具有 *N 个顶点*和 *M 条边*。任务是找出图中最长有向路径的长度。
**注意:**有向路径的长度是其中的边数。
**举例:**

> **输入:** N = 4，M = 5
> 
> ![](img/ea4cbf1a86578ef8edb9e1d02a3ee707.png)
> 
> **输出:** 3
> 有向路径 1->3->2->4
> T4】输入: N = 5，M = 8
> 
> ![](img/3ab0d1f8a45f5a4bdaa8e06d1aed288d.png)
> 
> **输出:** 3

**简单方法:**一种简单的方法是使用 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 计算从每个节点开始的最长路径的长度。
这种方法的时间复杂度为 O(N <sup>2</sup> )。
**高效方法**:一种高效的方法是将[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)和 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 一起使用，找到图中最长的路径。
设 **dp[i]** 为从节点 **i** 开始的最长路径的长度。最初 dp 的所有位置都是 0。我们可以从每个节点调用 DFS 函数，并遍历它的所有子节点。递归公式为:

> **dp[node] = max(dp[node]，1 + max(dp[child1]，dp[child2]，dp[child3]..))**

最后，检查 dp[]数组中的最大值，这将是 DAG 中最长的路径。
以下是上述方法的实现:

## C++

```
// C++ program to find the longest
// path in the DAG

#include <bits/stdc++.h>
using namespace std;

// Function to traverse the DAG
// and apply Dynamic Programming
// to find the longest path
void dfs(int node, vector<int> adj[], int dp[], bool vis[])
{
    // Mark as visited
    vis[node] = true;

    // Traverse for all its children
    for (int i = 0; i < adj[node].size(); i++) {

        // If not visited
        if (!vis[adj[node][i]])
            dfs(adj[node][i], adj, dp, vis);

        // Store the max of the paths
        dp[node] = max(dp[node], 1 + dp[adj[node][i]]);
    }
}

// Function to add an edge
void addEdge(vector<int> adj[], int u, int v)
{
    adj[u].push_back(v);
}

// Function that returns the longest path
int findLongestPath(vector<int> adj[], int n)
{
    // Dp array
    int dp[n + 1];
    memset(dp, 0, sizeof dp);

    // Visited array to know if the node
    // has been visited previously or not
    bool vis[n + 1];
    memset(vis, false, sizeof vis);

    // Call DFS for every unvisited vertex
    for (int i = 1; i <= n; i++) {
        if (!vis[i])
            dfs(i, adj, dp, vis);
    }

    int ans = 0;

    // Traverse and find the maximum of all dp[i]
    for (int i = 1; i <= n; i++) {
        ans = max(ans, dp[i]);
    }
    return ans;
}

// Driver Code
int main()
{
    int n = 5;
    vector<int> adj[n + 1];

    // Example-1
    addEdge(adj, 1, 2);
    addEdge(adj, 1, 3);
    addEdge(adj, 3, 2);
    addEdge(adj, 2, 4);
    addEdge(adj, 3, 4);

    cout << findLongestPath(adj, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the longest
// path in the DAG

import java.util.ArrayList;

// graph class
class Graph
{

    int vertices;
    ArrayList<Integer> edge[];

    Graph(int vertices)
    {
        this.vertices = vertices;
        edge = new ArrayList[vertices+1];
        for (int i = 0; i <= vertices; i++)
        {
            edge[i] = new ArrayList<>();
        }
    }
    void addEdge(int a,int b)
    {
        edge[a].add(b);
    }

    void dfs(int node, ArrayList<Integer> adj[], int dp[],
                                    boolean visited[])
    {
        // Mark as visited
        visited[node] = true;

        // Traverse for all its children
        for (int i = 0; i < adj[node].size(); i++)
        {

            // If not visited
            if (!visited[adj[node].get(i)])
                dfs(adj[node].get(i), adj, dp, visited);

            // Store the max of the paths
            dp[node] = Math.max(dp[node], 1 + dp[adj[node].get(i)]);
        }
    }

    // Function that returns the longest path
    int findLongestPath( int n)
    {
        ArrayList<Integer> adj[] = edge;
        // Dp array
        int[] dp = new int[n+1];

        // Visited array to know if the node
        // has been visited previously or not
        boolean[] visited = new boolean[n + 1];

        // Call DFS for every unvisited vertex
        for (int i = 1; i <= n; i++)
        {
            if (!visited[i])
                dfs(i, adj, dp, visited);
        }

        int ans = 0;

        // Traverse and find the maximum of all dp[i]
        for (int i = 1; i <= n; i++)
        {
            ans = Math.max(ans, dp[i]);
        }
        return ans;
    }
}

public class Main
{
    // Driver code
    public static void main(String[] args)
    {
        int n = 5;
        Graph graph = new Graph(n);
        // Example-1
        graph.addEdge( 1, 2);
        graph.addEdge( 1, 3);
        graph.addEdge( 3, 2);
        graph.addEdge( 2, 4);
        graph.addEdge( 3, 4);
        graph.findLongestPath(n);
        System.out.println( graph.findLongestPath( n));

    }
}

// This code is contributed by SumanSaurav
```

## 蟒蛇 3

```
# Python3 program to find the
# longest path in the DAG

# Function to traverse the DAG
# and apply Dynamic Programming
# to find the longest path
def dfs(node, adj, dp, vis):

    # Mark as visited
    vis[node] = True

    # Traverse for all its children
    for i in range(0, len(adj[node])): 

        # If not visited
        if not vis[adj[node][i]]:
            dfs(adj[node][i], adj, dp, vis)

        # Store the max of the paths
        dp[node] = max(dp[node], 1 + dp[adj[node][i]])

# Function to add an edge
def addEdge(adj, u, v):

    adj[u].append(v)

# Function that returns the longest path
def findLongestPath(adj, n):

    # Dp array
    dp = [0] * (n + 1)

    # Visited array to know if the node
    # has been visited previously or not
    vis = [False] * (n + 1)

    # Call DFS for every unvisited vertex
    for i in range(1, n + 1): 
        if not vis[i]:
            dfs(i, adj, dp, vis)

    ans = 0

    # Traverse and find the maximum of all dp[i]
    for i in range(1, n + 1): 
        ans = max(ans, dp[i])

    return ans

# Driver Code
if __name__ == "__main__":

    n = 5
    adj = [[] for i in range(n + 1)]

    # Example-1
    addEdge(adj, 1, 2)
    addEdge(adj, 1, 3)
    addEdge(adj, 3, 2)
    addEdge(adj, 2, 4)
    addEdge(adj, 3, 4)

    print(findLongestPath(adj, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find the longest
// path in the DAG
using System;
using System.Collections.Generic;

// graph class
class Graph
{
    public int vertices;
    public List<int> []edge;

    public Graph(int vertices)
    {
        this.vertices = vertices;
        edge = new List<int>[vertices + 1];
        for (int i = 0; i <= vertices; i++)
        {
            edge[i] = new List<int>();
        }
    }
    public void addEdge(int a, int b)
    {
        edge[a].Add(b);
    }

    public void dfs(int node, List<int> []adj,
                    int []dp, Boolean []visited)
    {
        // Mark as visited
        visited[node] = true;

        // Traverse for all its children
        for (int i = 0; i < adj[node].Count; i++)
        {

            // If not visited
            if (!visited[adj[node][i]])
                dfs(adj[node][i], adj, dp, visited);

            // Store the max of the paths
            dp[node] = Math.Max(dp[node], 1 +
                                dp[adj[node][i]]);
        }
    }

    // Function that returns the longest path
    public int findLongestPath( int n)
    {
        List<int> []adj = edge;
        // Dp array
        int[] dp = new int[n + 1];

        // Visited array to know if the node
        // has been visited previously or not
        Boolean[] visited = new Boolean[n + 1];

        // Call DFS for every unvisited vertex
        for (int i = 1; i <= n; i++)
        {
            if (!visited[i])
                dfs(i, adj, dp, visited);
        }

        int ans = 0;

        // Traverse and find the maximum of all dp[i]
        for (int i = 1; i <= n; i++)
        {
            ans = Math.Max(ans, dp[i]);
        }
        return ans;
    }
}

class GFG
{
    // Driver code
    public static void Main(String[] args)
    {
        int n = 5;
        Graph graph = new Graph(n);
        // Example-1
        graph.addEdge( 1, 2);
        graph.addEdge( 1, 3);
        graph.addEdge( 3, 2);
        graph.addEdge( 2, 4);
        graph.addEdge( 3, 4);
        graph.findLongestPath(n);
        Console.WriteLine(graph.findLongestPath(n));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to find the longest
// path in the DAG

// Function to traverse the DAG
// and apply Dynamic Programming
// to find the longest path
function dfs(node, adj, dp, vis)
{
    // Mark as visited
    vis[node] = true;

    // Traverse for all its children
    for (var i = 0; i < adj[node].length; i++) {

        // If not visited
        if (!vis[adj[node][i]])
            dfs(adj[node][i], adj, dp, vis);

        // Store the max of the paths
        dp[node] = Math.max(dp[node], 1 + dp[adj[node][i]]);
    }
}

// Function to add an edge
function addEdge(adj, u, v)
{
    adj[u].push(v);
}

// Function that returns the longest path
function findLongestPath(adj, n)
{
    // Dp array
    var dp = Array(n+1).fill(0);

    // Visited array to know if the node
    // has been visited previously or not
    var vis = Array(n+1).fill(false);

    // Call DFS for every unvisited vertex
    for (var i = 1; i <= n; i++) {
        if (!vis[i])
            dfs(i, adj, dp, vis);
    }

    var ans = 0;

    // Traverse and find the maximum of all dp[i]
    for (var i = 1; i <= n; i++) {
        ans = Math.max(ans, dp[i]);
    }
    return ans;
}

// Driver Code
var n = 5;
var adj = Array.from(Array(n+1), ()=>Array());
// Example-1
addEdge(adj, 1, 2);
addEdge(adj, 1, 3);
addEdge(adj, 3, 2);
addEdge(adj, 2, 4);
addEdge(adj, 3, 4);
document.write( findLongestPath(adj, n));

</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N+M)
T3】辅助空间: O(N)

？list = plqm 7 alhxfysazgcg 7 uryjfbnimlti-NH