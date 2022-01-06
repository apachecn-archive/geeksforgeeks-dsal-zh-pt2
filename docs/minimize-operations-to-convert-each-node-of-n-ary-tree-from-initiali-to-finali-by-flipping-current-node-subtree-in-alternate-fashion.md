# 通过以交替方式翻转当前节点子树，最小化将 N 元树的每个节点从初始[i]转换到最终[i]的操作

> 原文:[https://www . geesforgeks . org/minimum-operations-to-convert-n 元树的每个节点-从初始化到最终-通过以交替方式翻转当前节点-子树/](https://www.geeksforgeeks.org/minimize-operations-to-convert-each-node-of-n-ary-tree-from-initiali-to-finali-by-flipping-current-node-subtree-in-alternate-fashion/)

给定一个由来自**【0，N–1】**的 **N** 节点和大小为 **N** 的两个二进制[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **初始[]** 和**最终[]** 组成的 [N 元树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)，使得**初始[i]** 代表分配给节点 **i** 的值，任务是找到转换每个节点值所需的最小操作数

**示例:**

> **输入:** N = 3，边= {{1，2}，{1，3}}，初始[] = {1，1，0}，最终[] = {0，1，1 }
> 1(1)
> /\
> 2(1)3(0)
> **输出:** 2
> **解释:**
> **操作 1:** 拾取节点 1 并翻转其初始值。此操作后，初始[] = {0，1，0}和最终[] = {0，1，1}。
> **操作 2:** 拾取节点 3 并翻转其初始值。此操作后，初始[] = {0，1，1}和最终[] = {0，1，1}。
> 因此，打印 2 作为最小操作次数。
> 
> **输入:** N = 1，边= []，初始[] = {0}，最终[] = {1}
> **输出:** 1

**方法:**给定的问题可以通过对给定的树执行 [DFS 遍历并以交替的方式更新数组**初始值【】**中的节点值来解决。按照以下步骤解决此问题:](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)

*   初始化一个变量，将**总计**设为 **0** 来存储所需的操作数。
*   执行 [DFS 遍历](https://www.geeksforgeeks.org/graph-implementation-using-stl-for-competitive-programming-set-1-dfs-of-unweighted-and-undirected/)，同时跟踪两个布尔变量(最初为**假**，只有在翻转发生时才会改变)，并执行以下步骤:
    *   将当前节点标记为受访节点。
    *   如果当前节点的初始值、当前节点的最终值和当前布尔变量的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的值为非零，则翻转当前布尔变量并将**总数**的值增加 **1** 。
    *   遍历当前节点所有未访问的子节点，[递归调用](https://www.geeksforgeeks.org/recursion/)进行子节点的 [DFS 遍历。](https://www.geeksforgeeks.org/dfs-traversal-of-a-tree-using-recursion/)
*   完成以上步骤后，打印**合计**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// Function to add an edges in graph
void addEdges(vector<int> adj[],
              int u, int v)
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

// Function to perform the DFS of graph
// recursively from a given vertex u
void DFSUtil(int u, vector<int> adj[],
             vector<bool>& visited,
             bool foo, bool foo1,
             int initial[], int final[],
             int& ans)
{
    visited[u] = true;

    // Check for the condition for the
    // flipping of node's initial value
    if ((initial[u - 1] ^ foo)
        ^ final[u - 1]
              == true) {
        ans++;
        foo ^= 1;
    }

    // Traverse all the children of the
    // current source node u
    for (int i = 0;
         i < adj[u].size(); i++) {

        // Swap foo and foo1 signifies
        // there is change of level
        if (visited[adj[u][i]] == false)

            DFSUtil(adj[u][i], adj,
                    visited, foo1, foo,
                    initial, final, ans);
    }
}

// Function to perform the DFSUtil()
// for all the unvisited vertices
int DFS(vector<int> adj[], int V,
        int initial[], int final[])
{
    int total = 0;
    vector<bool> visited(V, false);

    // Traverse the given set of nodes
    for (int u = 1; u <= 1; u++) {

        // If the current node is
        // unvisited
        if (visited[u] == false)
            DFSUtil(u, adj, visited,
                    0, 0, initial,
                    final, total);
    }

    // Print the number of operations
    cout << total;
}

// Function to count the number of
// flips required to change initial
// node values to final node value
void countOperations(int N, int initial[],
                     int final[],
                     int Edges[][2])
{
    // Create adjacency list
    vector<int> adj[N + 1];

    // Add the given edges
    for (int i = 0; i < N - 1; i++) {
        addEdges(adj, Edges[i][0],
                 Edges[i][1]);
    }

    // DFS Traversal
    DFS(adj, N + 1, initial, final);
}

// Driver Code
int main()
{
    int N = 3;
    int Edges[][2] = { { 1, 2 }, { 1, 3 } };
    int initial[] = { 1, 1, 0 };
    int final[] = { 0, 1, 1 };
    countOperations(N, initial, final,
                    Edges);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    // Create adjacency list
    static int N = 3;
    static Vector<Vector<Integer>> adj = new Vector<Vector<Integer>>();

    static Vector<Boolean> visited;
    static int ans;

    // Function to add an edges in graph
    static void addEdges(int u, int v)
    {
        adj.get(u).add(v);
        adj.get(v).add(u);
    }

    // Function to perform the DFS of graph
    // recursively from a given vertex u
    static void DFSUtil(int u, boolean foo, boolean foo1, boolean[] initial, boolean[] finall)
    {
        visited.set(u, true);

        // Check for the condition for the
        // flipping of node's initial value
        if ((initial[u - 1] ^ foo)
            ^ finall[u - 1]
                  == true) {
            ans+=1;
            foo ^= true;
        }

        // Traverse all the children of the
        // current source node u
        for (int i = 0;
             i < adj.get(u).size(); i++) {

            // Swap foo and foo1 signifies
            // there is change of level
            if (visited.get(adj.get(u).get(i)) == false)

                DFSUtil(adj.get(u).get(i), foo1, foo,
                        initial, finall);
        }
    }

    // Function to perform the DFSUtil()
    // for all the unvisited vertices
    static void DFS(int V, boolean[] initial, boolean[] finall)
    {
        ans = 0;
        visited = new Vector<Boolean>();
        for(int i = 0; i < V; i++)
        {
            visited.add(false);
        }

        // Traverse the given set of nodes
        for (int u = 1; u <= 1; u++) {

            // If the current node is
            // unvisited
            if (visited.get(u) == false)
                DFSUtil(u, false, false, initial, finall);
        }

        // Print the number of operations
        System.out.print(ans);
    }

    // Function to count the number of
    // flips required to change initial
    // node values to final node value
    static void countOperations(int N, boolean[] initial, boolean[] finall, int[][] Edges)
    {
        // Add the given edges
        for (int i = 0; i < N - 1; i++) {
            addEdges(Edges[i][0], Edges[i][1]);
        }

        // DFS Traversal
        DFS(N + 1, initial, finall);
    }

  // Driver code
    public static void main(String[] args) {
        for(int i = 0; i < N + 1; i++)
        {
            adj.add(new Vector<Integer>());
        }
        int[][] Edges = { {1, 2}, {1, 3} };
        boolean[] initial = { true, true, false };
        boolean[] finall = { false, true, true};
        countOperations(N, initial, finall, Edges);
    }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Create adjacency list
N = 3
adj = []
for i in range(N + 1):
    adj.append([])

visited = []
ans = 0

# Function to add an edges in graph
def addEdges(u, v):
    global adj
    adj[u].append(v)
    adj[v].append(u)

# Function to perform the DFS of graph
# recursively from a given vertex u
def DFSUtil(u, foo, foo1, initial, finall):
    global visited, ans, adj
    visited[u] = True

    # Check for the condition for the
    # flipping of node's initial value
    if ((initial[u - 1] ^ foo) ^ finall[u - 1] == True):
        ans+=1
        foo ^= True

    # Traverse all the children of the
    # current source node u
    for i in range(len(adj[u])):
        # Swap foo and foo1 signifies
        # there is change of level
        if (visited[adj[u][i]] == False):
            DFSUtil(adj[u][i], foo1, foo, initial, finall)

# Function to perform the DFSUtil()
# for all the unvisited vertices
def DFS(V, initial, finall):
    global ans, visited
    ans = 0
    visited = [False]*V

    # Traverse the given set of nodes
    for u in range(1, 2):
        # If the current node is
        # unvisited
        if (visited[u] == False):
            DFSUtil(u, 0, 0, initial, finall)

    # Print the number of operations
    print(ans)

# Function to count the number of
# flips required to change initial
# node values to final node value
def countOperations(N, initial, finall, Edges):
    # Add the given edges
    for i in range(N - 1):
        addEdges(Edges[i][0], Edges[i][1])

    # DFS Traversal
    DFS(N + 1, initial, finall)

Edges = [ [ 1, 2 ], [ 1, 3 ] ]
initial = [ True, True, False ]
finall = [ False, True, True]
countOperations(N, initial, finall, Edges)

# This code is contributed by rameshtravel07.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;
class GFG {

    // Create adjacency list
    static int N = 3;
    static List<List<int>> adj = new List<List<int>>();

    static List<bool> visited;
    static int ans;

    // Function to add an edges in graph
    static void addEdges(int u, int v)
    {
        adj[u].Add(v);
        adj[v].Add(u);
    }

    // Function to perform the DFS of graph
    // recursively from a given vertex u
    static void DFSUtil(int u, bool foo, bool foo1, bool[] initial, bool[] finall)
    {
        visited[u] = true;

        // Check for the condition for the
        // flipping of node's initial value
        if ((initial[u - 1] ^ foo)
            ^ finall[u - 1]
                  == true) {
            ans+=1;
            foo ^= true;
        }

        // Traverse all the children of the
        // current source node u
        for (int i = 0;
             i < adj[u].Count; i++) {

            // Swap foo and foo1 signifies
            // there is change of level
            if (visited[adj[u][i]] == false)

                DFSUtil(adj[u][i], foo1, foo,
                        initial, finall);
        }
    }

    // Function to perform the DFSUtil()
    // for all the unvisited vertices
    static void DFS(int V, bool[] initial, bool[] finall)
    {
        ans = 0;
        visited = new List<bool>();
        for(int i = 0; i < V; i++)
        {
            visited.Add(false);
        }

        // Traverse the given set of nodes
        for (int u = 1; u <= 1; u++) {

            // If the current node is
            // unvisited
            if (visited[u] == false)
                DFSUtil(u, false, false, initial, finall);
        }

        // Print the number of operations
        Console.Write(ans);
    }

    // Function to count the number of
    // flips required to change initial
    // node values to final node value
    static void countOperations(int N, bool[] initial, bool[] finall, int[,] Edges)
    {
        // Add the given edges
        for (int i = 0; i < N - 1; i++) {
            addEdges(Edges[i,0], Edges[i,1]);
        }

        // DFS Traversal
        DFS(N + 1, initial, finall);
    }

  static void Main() {
    for(int i = 0; i < N + 1; i++)
    {
        adj.Add(new List<int>());
    }
    int[,] Edges = { {1, 2}, {1, 3} };
    bool[] initial = { true, true, false };
    bool[] finall = { false, true, true};
    countOperations(N, initial, finall, Edges);
  }
}

// This code is contributed by mukesh07.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Create adjacency list
    let N = 3;
    let adj = [];
    for(let i = 0; i < N + 1; i++)
    {
        adj.push([]);
    }

    let visited;
    let ans;

    // Function to add an edges in graph
    function addEdges(u, v)
    {
        adj[u].push(v);
        adj[v].push(u);
    }

    // Function to perform the DFS of graph
    // recursively from a given vertex u
    function DFSUtil(u, foo, foo1, initial, finall)
    {
        visited[u] = true;

        // Check for the condition for the
        // flipping of node's initial value
        if ((initial[u - 1] ^ foo)
            ^ finall[u - 1]
                  == true) {
            ans+=1;
            foo ^= true;
        }

        // Traverse all the children of the
        // current source node u
        for (let i = 0;
             i < adj[u].length; i++) {

            // Swap foo and foo1 signifies
            // there is change of level
            if (visited[adj[u][i]] == false)

                DFSUtil(adj[u][i], foo1, foo,
                        initial, finall);
        }
    }

    // Function to perform the DFSUtil()
    // for all the unvisited vertices
    function DFS(V, initial, finall)
    {
        ans = 0;
        visited = new Array(V);
        visited.fill(false);

        // Traverse the given set of nodes
        for (let u = 1; u <= 1; u++) {

            // If the current node is
            // unvisited
            if (visited[u] == false)
                DFSUtil(u, 0, 0, initial, finall);
        }

        // Print the number of operations
        document.write(ans);
    }

    // Function to count the number of
    // flips required to change initial
    // node values to final node value
    function countOperations(N, initial, finall, Edges)
    {
        // Add the given edges
        for (let i = 0; i < N - 1; i++) {
            addEdges(Edges[i][0], Edges[i][1]);
        }

        // DFS Traversal
        DFS(N + 1, initial, finall);
    }

    let Edges = [ [ 1, 2 ], [ 1, 3 ] ];
    let initial = [ true, true, false ];
    let finall = [ false, true, true];
    countOperations(N, initial, finall, Edges);

// This code iscontributed by decode2207.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)