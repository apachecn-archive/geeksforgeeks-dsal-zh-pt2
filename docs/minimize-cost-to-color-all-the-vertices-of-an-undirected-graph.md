# 最小化为无向图的所有顶点着色的成本

> 原文:[https://www . geeksforgeeks . org/最小化无向图的所有顶点的颜色成本/](https://www.geeksforgeeks.org/minimize-cost-to-color-all-the-vertices-of-an-undirected-graph/)

给定一个由 **N** 顶点和 **M** 边组成的[无向图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)，其中节点值在**【1，N】**范围内，由数组**着色的【】**指定的顶点被着色，任务是找到给定图的所有顶点的最小颜色。给顶点着色的成本由 **vCost** 给出，在两个顶点之间添加新边的成本由 **eCost** 给出。如果一个顶点是有颜色的，那么从那个顶点可以到达的所有顶点也变成有颜色的。

**示例:**

> **输入:** N = 3，M = 1，vCost = 3，eCost = 2，有色[] = {1}，源[] = {1}目的地[] = {2}
> **输出:** 2
> **解释:**
> 顶点 1 是有色的，它有一条带 2 的边。
> 所以，顶点 2 也是有颜色的。
> 在 2 到 3 之间增加一条边，代价是 eCost。< vCost。
> 因此，输出为 2。
> 
> **输入:** N = 4，M = 2，vCost = 3，eCost = 7，有色[] = {1，3}，源[] = {1，2}目的地[] = {4，3}
> **输出:** 0
> **解释:**
> 顶点 1 是有色的，它有一条边带 4。因此，顶点 4 也被着色。
> 顶点 2 是彩色的，它有一条边是 3。因此，顶点 3 也被着色。
> 由于所有顶点都已经着色，因此，成本为 0。

**方法:**
想法是**使用 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)计算未着色顶点的子图**的数量。
要最小化未着色的**子图**[](https://www.geeksforgeeks.org/find-all-cliques-of-size-k-in-an-undirected-graph/)**的着色成本，需要执行以下操作之一:**

*   **给子图着色**
*   **在任何有颜色和无颜色的顶点之间添加一条边。**

**基于 ***eCost** 和**vCost**T5】的最小值，需要选择以上两个步骤中的一个。
如果未着色子图的数量由 **X** 给出，那么着色所有顶点的总成本由 ***X×min(eCost，vCost)*** 给出。***

**按照以下步骤查找未着色子图的数量:**

1.  **对所有有颜色的顶点执行 DFS 遍历，并将它们标记为已访问，以将它们标识为有颜色的。**
2.  **在第 1 步 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 之后未被访问的顶点是未着色的顶点。**
3.  **对于每个未着色的顶点，使用 [DFS 将从该顶点可到达的所有顶点标记为已访问。](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)**
4.  **步骤 3 中出现的 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 的未着色顶点的数量是子图**x**的数量**
5.  **用公式 ***X×min(eCost，vCost)计算所有顶点着色的总成本。**T3】***

**下面是上述方法的实现:**

## **C++**

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to implement DFS Traversal
// to marks all the vertices visited
// from vertex U
void DFS(int U, int* vis, vector<int> adj[])
{
    // Mark U as visited
    vis[U] = 1;

    // Traverse the adjacency list of U
    for (int V : adj[U]) {
        if (vis[V] == 0)
            DFS(V, vis, adj);
    }
}

// Function to find the minimum cost
// to color all the vertices of graph
void minCost(int N, int M, int vCost,
             int eCost, int sorc[],
             vector<int> colored,
             int destination[])
{
    // To store adjacency list
    vector<int> adj[N + 1];

    // Loop through the edges to
    // create adjacency list
    for (int i = 0; i < M; i++) {

        adj[sorc[i]].push_back(destination[i]);
        adj[destination[i]].push_back(sorc[i]);
    }

    // To check if a vertex of the
    // graph is visited
    int vis[N + 1] = { 0 };

    // Mark visited to all the vertices
    // that can be reached by
    // colored vertices
    for (int i = 0; i < colored.size(); i++) {

        // Perform DFS
        DFS(colored[i], vis, adj);
    }

    // To store count of uncolored
    // sub-graphs
    int X = 0;

    // Loop through vertex to count
    // uncolored sub-graphs
    for (int i = 1; i <= N; i++) {

        // If vertex not visited
        if (vis[i] == 0) {

            // Increase count of
            // uncolored sub-graphs
            X++;

            // Perform DFS to mark
            // visited to all vertices
            // of current sub-graphs
            DFS(i, vis, adj);
        }
    }

    // Calculate minimum cost to color
    // all vertices
    int mincost = X * min(vCost, eCost);

    // Print the result
    cout << mincost << endl;
}

// Driver Code
int main()
{

    // Given number of
    // vertices and edges
    int N = 3, M = 1;

    // Given edges
    int sorc[] = { 1 };
    int destination[] = { 2 };

    // Given cost of coloring
    // and adding an edge
    int vCost = 3, eCost = 2;

    // Given array of
    // colored vertices
    vector<int> colored = { 1};

    minCost(N, M, vCost, eCost,
            sorc, colored, destination);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to implement DFS Traversal
// to marks all the vertices visited
// from vertex U
static void DFS(int U, int[] vis,
                ArrayList<ArrayList<Integer>> adj)
{

    // Mark U as visited
    vis[U] = 1;

    // Traverse the adjacency list of U
    for(Integer V : adj.get(U))
    {
        if (vis[V] == 0)
            DFS(V, vis, adj);
    }
}

// Function to find the minimum cost
// to color all the vertices of graph
static void minCost(int N, int M, int vCost,
                    int eCost, int sorc[],
                    ArrayList<Integer> colored,
                    int destination[])
{

    // To store adjacency list
    ArrayList<ArrayList<Integer>> adj = new ArrayList<>();

    for(int i = 0; i < N + 1; i++)
        adj.add(new ArrayList<Integer>());

    // Loop through the edges to
    // create adjacency list
    for(int i = 0; i < M; i++)
    {
        adj.get(sorc[i]).add(destination[i]);
        adj.get(destination[i]).add(sorc[i]);
    }

    // To check if a vertex of the
    // graph is visited
    int[] vis = new int[N + 1];

    // Mark visited to all the vertices
    // that can be reached by
    // colored vertices
    for(int i = 0; i < colored.size(); i++)
    {

        // Perform DFS
        DFS(colored.get(i), vis, adj);
    }

    // To store count of uncolored
    // sub-graphs
    int X = 0;

    // Loop through vertex to count
    // uncolored sub-graphs
    for(int i = 1; i <= N; i++)
    {

        // If vertex not visited
        if (vis[i] == 0)
        {

            // Increase count of
            // uncolored sub-graphs
            X++;

            // Perform DFS to mark
            // visited to all vertices
            // of current sub-graphs
            DFS(i, vis, adj);
        }
    }

    // Calculate minimum cost to color
    // all vertices
    int mincost = X * Math.min(vCost, eCost);

    // Print the result
    System.out.println(mincost);
}

// Driver code
public static void main(String[] args)
{

    // Given number of
    // vertices and edges
    int N = 3, M = 1;

    // Given edges
    int sorc[] = {1};
    int destination[] = {2};

    // Given cost of coloring
    // and adding an edge
    int vCost = 3, eCost = 2;

    // Given array of
    // colored vertices
    ArrayList<Integer> colored = new ArrayList<>();
    colored.add(1);

    minCost(N, M, vCost, eCost, sorc,
            colored, destination);
}
}

// This code is contributed by offbeat
```

## **蟒蛇 3**

```
# Python3 program to implement
# the above approach

# Function to implement DFS Traversal
# to marks all the vertices visited
# from vertex U
def DFS(U, vis, adj):

    # Mark U as visited
    vis[U] = 1

    # Traverse the adjacency list of U
    for V in adj[U]:
        if (vis[V] == 0):
            DFS(V, vis, adj)

# Function to find the minimum cost
# to color all the vertices of graph
def minCost(N, M, vCost, eCost, sorc,
            colored, destination):

    # To store adjacency list
    adj = [[] for i in range(N + 1)]

    # Loop through the edges to
    # create adjacency list
    for i in range(M):
        adj[sorc[i]].append(destination[i])
        adj[destination[i]].append(sorc[i])

    # To check if a vertex of the
    # graph is visited
    vis = [0] * (N + 1)

    # Mark visited to all the vertices
    # that can be reached by
    # colored vertices
    for i in range(len(colored)):

        # Perform DFS
        DFS(colored[i], vis, adj)

    # To store count of uncolored
    # sub-graphs
    X = 0

    # Loop through vertex to count
    # uncolored sub-graphs
    for i in range(1, N + 1):

        # If vertex not visited
        if (vis[i] == 0):

            # Increase count of
            # uncolored sub-graphs
            X += 1

            # Perform DFS to mark
            # visited to all vertices
            # of current sub-graphs
            DFS(i, vis, adj)

    # Calculate minimum cost to color
    # all vertices
    mincost = X * min(vCost, eCost)

    # Print the result
    print(mincost)

# Driver Code
if __name__ == '__main__':

    # Given number of
    # vertices and edges
    N = 3
    M = 1

    # Given edges
    sorc = [1]
    destination = [2]

    # Given cost of coloring
    # and adding an edge
    vCost = 3
    eCost = 2

    # Given array of
    # colored vertices
    colored = [1]

    minCost(N, M, vCost, eCost,
            sorc, colored, destination)

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program to implement
// the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to implement DFS Traversal
// to marks all the vertices visited
// from vertex U
static void DFS(int U, int[] vis, ArrayList adj)
{

    // Mark U as visited
    vis[U] = 1;

    // Traverse the adjacency list of U
    foreach(int V in (ArrayList)adj[U])
    {
        if (vis[V] == 0)
            DFS(V, vis, adj);
    }
}

// Function to find the minimum cost
// to color all the vertices of graph
static void minCost(int N, int M, int vCost,
                    int eCost, int []sorc,
                    ArrayList colored,
                    int []destination)
{

    // To store adjacency list
    ArrayList adj = new ArrayList();

    for(int i = 0; i < N + 1; i++)
        adj.Add(new ArrayList());

    // Loop through the edges to
    // create adjacency list
    for(int i = 0; i < M; i++)
    {
        ((ArrayList)adj[sorc[i]]).Add(destination[i]);
        ((ArrayList)adj[destination[i]]).Add(sorc[i]);
    }

    // To check if a vertex of the
    // graph is visited
    int[] vis = new int[N + 1];

    // Mark visited to all the vertices
    // that can be reached by
    // colored vertices
    for(int i = 0; i < colored.Count; i++)
    {

        // Perform DFS
        DFS((int)colored[i], vis, adj);
    }

    // To store count of uncolored
    // sub-graphs
    int X = 0;

    // Loop through vertex to count
    // uncolored sub-graphs
    for(int i = 1; i <= N; i++)
    {

        // If vertex not visited
        if (vis[i] == 0)
        {

            // Increase count of
            // uncolored sub-graphs
            X++;

            // Perform DFS to mark
            // visited to all vertices
            // of current sub-graphs
            DFS(i, vis, adj);
        }
    }

    // Calculate minimum cost to color
    // all vertices
    int mincost = X * Math.Min(vCost, eCost);

    // Print the result
    Console.Write(mincost);
}

// Driver code
public static void Main(string[] args)
{

    // Given number of
    // vertices and edges
    int N = 3, M = 1;

    // Given edges
    int []sorc = {1};
    int []destination = {2};

    // Given cost of coloring
    // and adding an edge
    int vCost = 3, eCost = 2;

    // Given array of
    // colored vertices
    ArrayList colored = new ArrayList();
    colored.Add(1);

    minCost(N, M, vCost, eCost,
            sorc, colored,
            destination);
}
}

// This code is contributed by rutvik_56
```

## **java 描述语言**

```
<script>

// Javascript program to implement
// the above approach

// Function to implement DFS Traversal
// to marks all the vertices visited
// from vertex U
function DFS(U, vis, adj)
{

    // Mark U as visited
    vis[U] = 1;

    // Traverse the adjacency list of U
    for(var V of adj[U])
    {
        if (vis[V] == 0)
            DFS(V, vis, adj);
    }
}

// Function to find the minimum cost
// to color all the vertices of graph
function minCost( N, M, vCost, eCost, sorc, colored, destination)
{

    // To store adjacency list
    var adj = [];

    for(var i = 0; i < N + 1; i++)
        adj.push(new Array());

    // Loop through the edges to
    // create adjacency list
    for(var i = 0; i < M; i++)
    {
        (adj[sorc[i]]).push(destination[i]);
        (adj[destination[i]]).push(sorc[i]);
    }

    // To check if a vertex of the
    // graph is visited
    var vis = Array(N+1).fill(0);

    // Mark visited to all the vertices
    // that can be reached by
    // colored vertices
    for(var i = 0; i < colored.length; i++)
    {

        // Perform DFS
        DFS(colored[i], vis, adj);
    }

    // To store count of uncolored
    // sub-graphs
    var X = 0;

    // Loop through vertex to count
    // uncolored sub-graphs
    for(var i = 1; i <= N; i++)
    {

        // If vertex not visited
        if (vis[i] == 0)
        {

            // Increase count of
            // uncolored sub-graphs
            X++;

            // Perform DFS to mark
            // visited to all vertices
            // of current sub-graphs
            DFS(i, vis, adj);
        }
    }

    // Calculate minimum cost to color
    // all vertices
    var mincost = X * Math.min(vCost, eCost);

    // Print the result
    document.write(mincost);
}

// Driver code

// Given number of
// vertices and edges
var N = 3, M = 1;

// Given edges
var sorc = [1];
var destination = [2];

// Given cost of coloring
// and adding an edge
var vCost = 3, eCost = 2;

// Given array of
// colored vertices
var colored = [];
colored.push(1);

minCost(N, M, vCost, eCost,
        sorc, colored,
        destination);

</script>
```

****Output:** 

```
2
```** 

*****时间复杂度:** O(N + M)*
***辅助空间:** O(N)***