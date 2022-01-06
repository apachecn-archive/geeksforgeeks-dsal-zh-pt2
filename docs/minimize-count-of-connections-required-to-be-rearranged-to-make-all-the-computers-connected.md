# 最小化需要重新排列的连接数量，以使所有计算机连接起来

> 原文:[https://www . geeksforgeeks . org/最小化连接数量-需要重新排列才能连接所有计算机/](https://www.geeksforgeeks.org/minimize-count-of-connections-required-to-be-rearranged-to-make-all-the-computers-connected/)

给定一个整数 **N** ，表示通过形成网络的电缆连接的计算机数量和一个 [2D 阵列](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **连接【】【】**，每行 **(i，j)** 表示**I<sup>th</sup>T11】和**j<sup>th</sup>T15】计算机之间的连接，任务是通过移除任何给定的连接并连接两台断开的计算机来直接或间接连接所有计算机。
如果无法连接所有电脑，打印 **-1** 。
否则，打印所需的最小操作次数。****

**示例:**

> **输入:** N = 4，连接[][] = {{0，1}，{0，2}，{1，2}}
> **输出:** 1
> **说明:**解除计算机 1 和 2 之间的连接，连接计算机 1 和 3。
> 
> **输入:** N = 5，连接[][] = {{0，1}，{0，2}，{3，4}，{2，3}}
> **输出:** 0

**方法:**想法是使用类似于[最小生成树](https://www.geeksforgeeks.org/tag/minimum-spanning-tree/)的概念，如在具有 **N 个**节点的[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)中，仅需要**N–1 个**边来连接所有节点。

> **冗余边=总边–[(节点数–1)–(组件数–1)]**
> 
> **如果冗余边>(组件数量–1):**很明显，有足够的电线可以用来连接断开的计算机。否则，打印-1。

按照以下步骤解决问题:

1.  初始化一个[无序图](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)，比如**调整**来存储给定边信息的邻接表。
2.  初始化[布尔数据类型](https://www.geeksforgeeks.org/bool-data-type-in-c/)的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如**访问了**，以存储节点是否被访问。
3.  [生成邻接表](https://www.geeksforgeeks.org/graph-implementation-using-stl-for-competitive-programming-set-1-dfs-of-unweighted-and-undirected/)，同时计算边数。
4.  初始化一个变量，比如说**组件**，来存储连接组件的[计数。](https://www.geeksforgeeks.org/program-to-count-number-of-connected-components-in-an-undirected-graph/)
5.  [使用](https://www.geeksforgeeks.org/tag/algorithms-graph-traversals/) [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 遍历图的节点，统计连接的组件数量，并将其存储在变量**组件**中。
6.  初始化一个变量，说**冗余**，用上面的公式存储冗余边数。
7.  如果**冗余边>组件–1**，则所需操作的最小数量等于**组件–1**。否则，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to visit the nodes of a graph
void DFS(unordered_map<int, vector<int> >& adj,
         int node, vector<bool>& visited)
{
    // If current node is already visited
    if (visited[node])
        return;

    // If current node is not visited
    visited[node] = true;

    // Recurse for neighbouring nodes
    for (auto x : adj[node]) {

        // If the node is not visited
        if (visited[x] == false)
            DFS(adj, x, visited);
    }
}

// Utility function to check if it is
// possible to connect all computers or not
int makeConnectedUtil(int N,
                      int connections[][2],
                      int M)
{
    // Stores whether a
    // node is visited or not
    vector<bool> visited(N, false);

    // Build the adjacency list
    unordered_map<int, vector<int> > adj;

    // Stores count of edges
    int edges = 0;

    // Building adjacency list
    // from the given edges
    for (int i = 0; i < M; ++i) {

        // Add edges
        adj[connections[i][0]].push_back(
            connections[i][1]);
        adj[connections[i][1]].push_back(
            connections[i][0]);

        // Increment count of edges
        edges += 1;
    }

    // Stores count of components
    int components = 0;

    for (int i = 0; i < N; ++i) {

        // If node is not visited
        if (visited[i] == false) {

            // Increment components
            components += 1;

            // Perform DFS
            DFS(adj, i, visited);
        }
    }

    // At least N - 1 edges are required
    if (edges < N - 1)
        return -1;

    // Count redundant edges
    int redundant = edges - ((N - 1)
                             - (components - 1));

    // Check if components can be
    // rearranged using redundant edges
    if (redundant >= (components - 1))
        return components - 1;

    return -1;
}

// Function to check if it is possible
// to connect all the computers or not
void makeConnected(int N, int connections[][2], int M)
{
    // Stores counmt of minimum
    // operations required
    int minOps = makeConnectedUtil(
        N, connections, M);

    // Print the minimum number
    // of operations required
    cout << minOps;
}

// Driver Code
int main()
{
    // Given number of computers
    int N = 4;

    // Given set of connections
    int connections[][2] = {
        { 0, 1 }, { 0, 2 }, { 1, 2 }
    };
    int M = sizeof(connections)
            / sizeof(connections[0]);

    // Function call to check if it is
    // possible to connect all computers or not
    makeConnected(N, connections, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to visit the nodes of a graph
    public static void DFS(HashMap<Integer, ArrayList<Integer> > adj,
                           int node, boolean visited[])
    {
        // If current node is already visited
        if (visited[node])
            return;

        // If current node is not visited
        visited[node] = true;

        // Recurse for neighbouring nodes
        for (int x : adj.get(node)) {

            // If the node is not visited
            if (visited[x] == false)
                DFS(adj, x, visited);
        }
    }

    // Utility function to check if it is
    // possible to connect all computers or not
    public static int
    makeConnectedUtil(int N, int connections[][], int M)
    {
        // Stores whether a
        // node is visited or not
        boolean visited[] = new boolean[N];

        // Build the adjacency list
        HashMap<Integer, ArrayList<Integer> > adj
            = new HashMap<>();

        // Initialize the adjacency list
        for (int i = 0; i < N; i++) {
            adj.put(i, new ArrayList<Integer>());
        }

        // Stores count of edges
        int edges = 0;

        // Building adjacency list
        // from the given edges
        for (int i = 0; i < M; ++i) {

            // Get neighbours list
            ArrayList<Integer> l1
                = adj.get(connections[i][0]);
            ArrayList<Integer> l2
                = adj.get(connections[i][0]);

            // Add edges
            l1.add(connections[i][1]);
            l2.add(connections[i][0]);

            // Increment count of edges
            edges += 1;
        }

        // Stores count of components
        int components = 0;

        for (int i = 0; i < N; ++i) {

            // If node is not visited
            if (visited[i] == false) {

                // Increment components
                components += 1;

                // Perform DFS
                DFS(adj, i, visited);
            }
        }

        // At least N - 1 edges are required
        if (edges < N - 1)
            return -1;

        // Count redundant edges
        int redundant
            = edges - ((N - 1) - (components - 1));

        // Check if components can be
        // rearranged using redundant edges
        if (redundant >= (components - 1))
            return components - 1;

        return -1;
    }

    // Function to check if it is possible
    // to connect all the computers or not
    public static void
    makeConnected(int N, int connections[][], int M)
    {
        // Stores counmt of minimum
        // operations required
        int minOps = makeConnectedUtil(N, connections, M);

        // Print the minimum number
        // of operations required
        System.out.println(minOps);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given number of computers
        int N = 4;

        // Given set of connections
        int connections[][]
            = { { 0, 1 }, { 0, 2 }, { 1, 2 } };
        int M = connections.length;

        // Function call to check if it is
        // possible to connect all computers or not
        makeConnected(N, connections, M);
    }
}

// This code is contributed by kingash.
```

## 蟒蛇 3

```
# Python3 code for the above approach

# Function to visit the nodes of a graph
def DFS(adj, node, visited):

    # If current node is already visited
    if (visited[node]):
        return

    # If current node is not visited
    visited[node] = True

    # Recurse for neighbouring nodes
    if(node in adj):
        for x in adj[node]:

            # If the node is not visited
            if (visited[x] == False):
              DFS(adj, x, visited)

# Utility function to check if it is
# possible to connect all computers or not
def makeConnectedUtil(N, connections, M):

    # Stores whether a
    # node is visited or not
    visited = [False for i in range(N)]

    # Build the adjacency list
    adj = {}

    # Stores count of edges
    edges = 0

    # Building adjacency list
    # from the given edges
    for i in range(M):

        # Add edges
        if (connections[i][0] in adj):
            adj[connections[i][0]].append(
                connections[i][1])
        else:
            adj[connections[i][0]] = []
        if (connections[i][1] in adj):
            adj[connections[i][1]].append(
                connections[i][0])
        else:
            adj[connections[i][1]] = []

        # Increment count of edges
        edges += 1

    # Stores count of components
    components = 0

    for i in range(N):

        # If node is not visited
        if (visited[i] == False):

            # Increment components
            components += 1

            # Perform DFS
            DFS(adj, i, visited)

    # At least N - 1 edges are required
    if (edges < N - 1):
        return -1

    # Count redundant edges
    redundant = edges - ((N - 1) - (components - 1))

    # Check if components can be
    # rearranged using redundant edges
    if (redundant >= (components - 1)):
        return components - 1

    return -1

# Function to check if it is possible
# to connect all the computers or not
def makeConnected(N, connections, M):

    # Stores counmt of minimum
    # operations required
    minOps = makeConnectedUtil(N, connections, M)

    # Print the minimum number
    # of operations required
    print(minOps)

# Driver Code
if __name__ == '__main__':

    # Given number of computers
    N = 4

    # Given set of connections
    connections = [ [ 0, 1 ], [ 0, 2 ], [ 1, 2 ] ]
    M = len(connections)

    # Function call to check if it is
    # possible to connect all computers or not
    makeConnected(N, connections, M)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to visit the nodes of a graph
    public static void DFS(Dictionary<int, List<int>> adj, int node, bool[] visited)
    {
        // If current node is already visited
        if (visited[node])
            return;

        // If current node is not visited
        visited[node] = true;

        // Recurse for neighbouring nodes
        foreach(int x in adj[node]) {

            // If the node is not visited
            if (visited[x] == false)
                DFS(adj, x, visited);
        }
    }

    // Utility function to check if it is
    // possible to connect all computers or not
    public static int makeConnectedUtil(int N, int[,] connections, int M)
    {
        // Stores whether a
        // node is visited or not
        bool[] visited = new bool[N];

        // Build the adjacency list
        Dictionary<int, List<int>> adj = new Dictionary<int, List<int>>();

        // Initialize the adjacency list
        for (int i = 0; i < N; i++) {
            adj[i] = new List<int>();
        }

        // Stores count of edges
        int edges = 0;

        // Building adjacency list
        // from the given edges
        for (int i = 0; i < M; ++i) {

            // Get neighbours list
            List<int> l1 = adj[connections[i,0]];
            List<int> l2 = adj[connections[i,0]];

            // Add edges
            l1.Add(connections[i,1]);
            l2.Add(connections[i,0]);

            // Increment count of edges
            edges += 1;
        }

        // Stores count of components
        int components = 0;

        for (int i = 0; i < N; ++i) {

            // If node is not visited
            if (visited[i] == false) {

                // Increment components
                components += 1;

                // Perform DFS
                DFS(adj, i, visited);
            }
        }

        // At least N - 1 edges are required
        if (edges < N - 1)
            return -1;

        // Count redundant edges
        int redundant = edges - ((N - 1) - (components - 1));

        // Check if components can be
        // rearranged using redundant edges
        if (redundant >= (components - 1))
            return components - 1;

        return -1;
    }

    // Function to check if it is possible
    // to connect all the computers or not
    public static void makeConnected(int N, int[,] connections, int M)
    {
        // Stores counmt of minimum
        // operations required
        int minOps = makeConnectedUtil(N, connections, M);

        // Print the minimum number
        // of operations required
        Console.WriteLine(minOps);
    }

  static void Main() {
    // Given number of computers
    int N = 4;

    // Given set of connections
    int[,] connections
        = { { 0, 1 }, { 0, 2 }, { 1, 2 } };
    int M = connections.GetLength(0);

    // Function call to check if it is
    // possible to connect all computers or not
    makeConnected(N, connections, M);
  }
}

// This code is contributed by decode2207.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to visit the nodes of a graph
    function DFS(adj, node, visited)
    {
        // If current node is already visited
        if (visited[node])
            return;

        // If current node is not visited
        visited[node] = true;

        // Recurse for neighbouring nodes
        for(let x = 0; x < adj[node].length; x++) {

            // If the node is not visited
            if (visited[adj[node][x]] == false)
                DFS(adj, adj[node][x], visited);
        }
    }

    // Utility function to check if it is
    // possible to connect all computers or not
    function makeConnectedUtil(N, connections, M)
    {
        // Stores whether a
        // node is visited or not
        let visited = new Array(N);
        visited.fill(false);

        // Build the adjacency list
        let adj = new Map();

        // Initialize the adjacency list
        for (let i = 0; i < N; i++) {
            adj[i] = [];
        }

        // Stores count of edges
        let edges = 0;

        // Building adjacency list
        // from the given edges
        for (let i = 0; i < M; ++i) {

            // Get neighbours list
            let l1 = adj[connections[i][0]];
            let l2 = adj[connections[i][0]];

            // Add edges
            l1.push(connections[i][1]);
            l2.push(connections[i][0]);

            // Increment count of edges
            edges += 1;
        }

        // Stores count of components
        let components = 0;

        for (let i = 0; i < N; ++i) {

            // If node is not visited
            if (visited[i] == false) {

                // Increment components
                components += 1;

                // Perform DFS
                DFS(adj, i, visited);
            }
        }

        // At least N - 1 edges are required
        if (edges < N - 1)
            return -1;

        // Count redundant edges
        let redundant = edges - ((N - 1) - (components - 1));

        // Check if components can be
        // rearranged using redundant edges
        if (redundant >= (components - 1))
            return components - 1;

        return -1;
    }

    // Function to check if it is possible
    // to connect all the computers or not
    function makeConnected(N, connections, M)
    {
        // Stores counmt of minimum
        // operations required
        let minOps = makeConnectedUtil(N, connections, M);

        // Print the minimum number
        // of operations required
        document.write(minOps);
    }

    // Given number of computers
    let N = 4;

    // Given set of connections
    let connections = [ [0, 1], [0, 2], [1, 2] ];
    let M = connections.length;

    // Function call to check if it is
    // possible to connect all computers or not
    makeConnected(N, connections, M);

 // This code is contributed by sureh07.
</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(N)*