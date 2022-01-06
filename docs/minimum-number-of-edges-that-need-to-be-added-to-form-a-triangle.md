# 形成三角形需要添加的最小边数

> 原文:[https://www . geesforgeks . org/需要添加最小边数以形成三角形/](https://www.geeksforgeeks.org/minimum-number-of-edges-that-need-to-be-added-to-form-a-triangle/)

给定一个有 **N** 个顶点和 **N** 条边的无向图。没有两条边连接同一对顶点。三角形是一组三个不同的顶点，这样每对顶点由一条边连接，即三个不同的顶点 **u** 、 **v** 和 **w** 是一个三角形，如果图形包含边 **(u，v)** 、 **(v，w)** 和 **(v，u)** 。
任务是找到需要添加到给定图中的最小边数，使得该图至少包含一个三角形。

**示例:**

```
Input:
  1
 / \
2   3
Output: 1

Input:
  1     3
 /     /
2     4
Output: 2

```

**方法:**初始化 **ans = 3** ，这是形成三角形所需的最大边数。现在，对于每个可能的顶点三元组，有四种情况:

1.  **情况 1:** 如果存在节点 **i** 、 **j** 和 **k** 使得存在从 **(i，j)** 、 **(j，k)** 和 **(k，i)** 的边缘，则答案为 **0** 。
2.  **情况 2:** 如果存在节点 **i** 、 **j** 和 **k** 使得只有两对顶点连接，那么需要单个边来形成三角形。所以更新 **ans = min(ans，1)** 。
3.  **情况 3:** 否则，如果只有一对顶点相连，则 **ans = min(ans，2)** 。
4.  **情况 4:** 当没有边缘时，则 **ans = min(ans，3)** 。

最后打印**和**。

下面是上述方法的实现。

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number
// of edges that need to be added to
// the given graph such that it
// contains at least one triangle
int minEdges(vector<pair<int, int> > v, int n)
{

    // adj is the adjacency matrix such that
    // adj[i][j] = 1 when there is an
    // edge between i and j
    vector<vector<int> > adj;
    adj.resize(n + 1);
    for (int i = 0; i < adj.size(); i++)
        adj[i].resize(n + 1, 0);

    // As the graph is undirected
    // so there will be an edge
    // between (i, j) and (j, i)
    for (int i = 0; i < v.size(); i++) {
        adj[v[i].first][v[i].second] = 1;
        adj[v[i].second][v[i].first] = 1;
    }

    // To store the required
    // count of edges
    int edgesNeeded = 3;

    // For every possible vertex triplet
    for (int i = 1; i <= n; i++) {
        for (int j = i + 1; j <= n; j++) {
            for (int k = j + 1; k <= n; k++) {

                // If the vertices form a triangle
                if (adj[i][j] && adj[j][k] && adj[k][i])
                    return 0;

                // If no edges are present
                if (!(adj[i][j] || adj[j][k] || adj[k][i]))
                    edgesNeeded = min(edgesNeeded, 3);

                else {

                    // If only 1 edge is required
                    if ((adj[i][j] && adj[j][k])
                        || (adj[j][k] && adj[k][i])
                        || (adj[k][i] && adj[i][j])) {
                        edgesNeeded = 1;
                    }

                    // Two edges are required
                    else
                        edgesNeeded = min(edgesNeeded, 2);
                }
            }
        }
    }
    return edgesNeeded;
}

// Driver code
int main()
{

    // Number of nodes
    int n = 3;

    // Storing the edges in a vector of pairs
    vector<pair<int, int> > v = { { 1, 2 }, { 1, 3 } };

    cout << minEdges(v, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;

class Pair<V, E> 
{
    V first;
    E second;

    Pair(V first, E second) 
    {
        this.first = first;
        this.second = second;
    }
}

class GFG 
{

    // Function to return the minimum number
    // of edges that need to be added to
    // the given graph such that it
    // contains at least one triangle
    static int minEdges(Vector<Pair<Integer, 
                                    Integer>> v, int n) 
    {

        // adj is the adjacency matrix such that
        // adj[i][j] = 1 when there is an
        // edge between i and j
        int[][] adj = new int[n + 1][n + 1];

        // As the graph is undirected
        // so there will be an edge
        // between (i, j) and (j, i)
        for (int i = 0; i < v.size(); i++) 
        {
            adj[v.elementAt(i).first]
               [v.elementAt(i).second] = 1;
            adj[v.elementAt(i).second]
               [v.elementAt(i).first] = 1;
        }

        // To store the required
        // count of edges
        int edgesNeeded = 0;

        // For every possible vertex triplet
        for (int i = 1; i <= n; i++)
        {
            for (int j = i + 1; j <= n; j++) 
            {
                for (int k = j + 1; k <= n; k++) 
                {

                    // If the vertices form a triangle
                    if (adj[i][j] == 1 && 
                        adj[j][k] == 1 && adj[k][i] == 1)
                        return 0;

                    // If no edges are present
                    if (!(adj[i][j] == 1 || 
                          adj[j][k] == 1 || adj[k][i] == 1))
                        edgesNeeded = Math.min(edgesNeeded, 3);

                    else 
                    {

                        // If only 1 edge is required
                        if ((adj[i][j] == 1 && adj[j][k] == 1) || 
                            (adj[j][k] == 1 && adj[k][i] == 1) || 
                            (adj[k][i] == 1 && adj[i][j] == 1)) 
                        {
                            edgesNeeded = 1;
                        }

                        // Two edges are required
                        else
                            edgesNeeded = Math.min(edgesNeeded, 2);
                    }
                }
            }
        }
        return edgesNeeded;
    }

    // Driver Code
    public static void main(String[] args) 
    {

        // Number of nodes
        int n = 3;

        // Storing the edges in a vector of pairs
        Vector<Pair<Integer, 
                    Integer>> v = new Vector<>(Arrays.asList(new Pair<>(1, 2), 
                                                             new Pair<>(1, 3)));

        System.out.println(minEdges(v, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach 

# Function to return the minimum number 
# of edges that need to be added to 
# the given graph such that it 
# contains at least one triangle 
def minEdges(v, n) : 

    # adj is the adjacency matrix such that 
    # adj[i][j] = 1 when there is an 
    # edge between i and j 
    adj = dict.fromkeys(range(n + 1)); 

    # adj.resize(n + 1); 
    for i in range(n + 1) :
        adj[i] = [0] * (n + 1); 

    # As the graph is undirected 
    # so there will be an edge 
    # between (i, j) and (j, i) 
    for i in range(len(v)) :
        adj[v[i][0]][v[i][1]] = 1; 
        adj[v[i][1]][v[i][0]] = 1; 

    # To store the required 
    # count of edges 
    edgesNeeded = 3; 

    # For every possible vertex triplet 
    for i in range(1, n + 1) : 
        for j in range(i + 1, n + 1) :
            for k in range(j + 1, n + 1) :

                # If the vertices form a triangle 
                if (adj[i][j] and adj[j][k] and adj[k][i]) :
                    return 0; 

                # If no edges are present 
                if (not (adj[i][j] or adj[j][k] or adj[k][i])) :
                    edgesNeeded = min(edgesNeeded, 3); 

                else :

                    # If only 1 edge is required 
                    if ((adj[i][j] and adj[j][k])
                        or (adj[j][k] and adj[k][i]) 
                        or (adj[k][i] and adj[i][j])) : 
                        edgesNeeded = 1; 

                    # Two edges are required 
                    else :
                        edgesNeeded = min(edgesNeeded, 2); 

    return edgesNeeded; 

# Driver code 
if __name__ == "__main__" : 

    # Number of nodes 
    n = 3; 

    # Storing the edges in a vector of pairs 
    v = [ [ 1, 2 ], [ 1, 3 ] ]; 

    print(minEdges(v, n)); 

# This code is contributed by kanugargng
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class Pair 
{
    public int first;
    public int second;

    public Pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }
}

class GFG 
{

    // Function to return the minimum number
    // of edges that need to be added to
    // the given graph such that it
    // contains at least one triangle
    static int minEdges(List<Pair> v, int n) 
    {

        // adj is the adjacency matrix such that
        // adj[i,j] = 1 when there is an
        // edge between i and j
        int[,] adj = new int[n + 1, n + 1];

        // As the graph is undirected
        // so there will be an edge
        // between (i, j) and (j, i)
        for (int i = 0; i < v.Count; i++) 
        {
            adj[v[i].first,v[i].second] = 1;
            adj[v[i].second,v[i].first] = 1;
        }

        // To store the required
        // count of edges
        int edgesNeeded = 0;

        // For every possible vertex triplet
        for (int i = 1; i <= n; i++)
        {
            for (int j = i + 1; j <= n; j++) 
            {
                for (int k = j + 1; k <= n; k++) 
                {

                    // If the vertices form a triangle
                    if (adj[i, j] == 1 && 
                        adj[j, k] == 1 && adj[k, i] == 1)
                        return 0;

                    // If no edges are present
                    if (!(adj[i, j] == 1 || 
                        adj[j, k] == 1 || adj[k, i] == 1))
                        edgesNeeded = Math.Min(edgesNeeded, 3);

                    else
                    {

                        // If only 1 edge is required
                        if ((adj[i, j] == 1 && adj[j, k] == 1) || 
                            (adj[j, k] == 1 && adj[k, i] == 1) || 
                            (adj[k, i] == 1 && adj[i, j] == 1)) 
                        {
                            edgesNeeded = 1;
                        }

                        // Two edges are required
                        else
                            edgesNeeded = Math.Min(edgesNeeded, 2);
                    }
                }
            }
        }
        return edgesNeeded;
    }

    // Driver Code
    public static void Main(String[] args) 
    {

        // Number of nodes
        int n = 3;

        // Storing the edges in a vector of pairs

        List<Pair> v = new List<Pair>();
        v.Add(new Pair(1, 2));
        v.Add(new Pair(1, 3));
        Console.WriteLine(minEdges(v, n));
    }
}

// This code is contributed by PrinciRaj1992
```

**Output:**

```
1

```