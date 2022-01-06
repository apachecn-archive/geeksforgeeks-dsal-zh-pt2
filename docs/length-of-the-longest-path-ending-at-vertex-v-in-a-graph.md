# 终止于图中顶点 V 的最长路径的长度

> 原文:[https://www . geeksforgeeks . org/最长路径长度-以图形中的顶点 v 结尾/](https://www.geeksforgeeks.org/length-of-the-longest-path-ending-at-vertex-v-in-a-graph/)

给定一个[二进制矩阵](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-binary-matrix-or-not/)**mat【】【】**表示图的[邻接矩阵表示，其中**mat【I】【j】**作为 **1** 表示顶点 **i** 和 **j** 与一个顶点 **V** 之间有一条边，任务是找到从任意节点到顶点 **X** 的最长路径，使得图中的每个顶点](https://www.geeksforgeeks.org/c-program-to-implement-adjacency-matrix-of-a-given-graph/)

**示例:**

> **输入:**图形[][] = {{0，1，0，0}，{1，0，1，1，1}，{0，1，0，0}，{0，1，0，0}}，V = 2
> **输出:** 2
> **解释:**
> 给定图形如下:
> 0
> |
> 1
> /\
> 2 3
> 终止于顶点 2 的最长路径因此，该路径的长度为 2。
> 
> **输入:**图形[][] = {{0，1，1，1}，{1，0，0，0}，{1，0，0，0}，{1，0，0，0，0}}，V = 1
> **输出:** 2

**方法:**从源节点作为 **V** 对给定的图执行 [DFS 遍历，并从节点 **V** 找到具有最深节点的路径的最大长度，可以解决给定的问题。](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)

按照以下步骤解决问题:

*   [初始化邻接表](https://www.geeksforgeeks.org/convert-adjacency-matrix-to-adjacency-list-representation-of-graph/)，比如说 **Adj[]，**来自矩阵 **mat[][]** 中给定的[图形表示](https://www.geeksforgeeks.org/graph-and-its-representations/)。
*   初始化一个辅助[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如**访问了[]，**来跟踪是否有顶点被访问。
*   初始化一个变量，将**距离**设为 **0** ，以存储从任意源节点到给定顶点 **V** 的合成路径的最大长度。
*   从节点 **V** 对给定的图执行 [DFS 遍历，并执行以下步骤:](https://www.geeksforgeeks.org/iterative-depth-first-traversal/)
    *   将当前节点 **V** 标记为已访问，即**已访问【V】=真**。
    *   将**距离**的值更新为**距离**和**等级**的最大值。
    *   遍历当前源节点 **V** 的[邻接表](https://www.geeksforgeeks.org/graph-and-its-representations/)。如果子节点与父节点不同且尚未被访问，则[递归执行 DFS 遍历](https://www.geeksforgeeks.org/dfs-traversal-of-a-tree-using-recursion/)作为 **dfs(子，可调，已访问，级别+ 1，距离)**。
    *   完成上述步骤后，如果给定图形中存在循环，则将当前节点 **V** 标记为未访问，以包括路径[。](https://www.geeksforgeeks.org/detect-cycle-in-a-graph/)
*   完成上述步骤后，将**距离**的值打印为任意源节点与给定节点 **V** 之间的合成最大距离。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform DFS Traversal from
// source node to the deepest node and
// update maximum distance to the deepest node
void dfs(int src, vector<int> Adj[],
         vector<bool>& visited, int level,
         int& distance)
{

    // Mark source as visited
    visited[src] = true;

    // Update the maximum distance
    distance = max(distance, level);

    // Traverse the adjacency list
    // of the current source node
    for (auto& child : Adj[src]) {

        // Recursively call
        // for the child node
        if (child != src
            and visited[child] == false) {
            dfs(child, Adj, visited,
                level + 1, distance);
        }
    }

    // Backtracking step
    visited[src] = false;
}

// Function to calculate maximum length
// of the path ending at vertex V from
// any source node
int maximumLength(vector<vector<int> >& mat,
                  int V)
{

    // Stores the maximum length of
    // the path ending at vertex V
    int distance = 0;

    // Stores the size of the matrix
    int N = (int)mat.size();

    // Stores the adjacency list
    // of the given graph
    vector<int> Adj[N];

    vector<bool> visited(N, false);

    // Traverse the matrix to
    // create adjacency list
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            if (mat[i][j] == 1) {
                Adj[i].push_back(j);
            }
        }
    }

    // Perform DFS Traversal to
    // update the maximum distance
    dfs(V, Adj, visited, 0, distance);

    return distance;
}

// Driver Code
int main()
{
    vector<vector<int> > mat = { { 0, 1, 0, 0 },
                                 { 1, 0, 1, 1 },
                                 { 0, 1, 0, 0 },
                                 { 0, 1, 0, 0 } };
    int V = 2;

    cout << maximumLength(mat, V);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;

class GFG{

static int distance;

// Function to perform DFS Traversal from source node to
// the deepest node and update maximum distance to the
// deepest node
private static void dfs(int src, ArrayList<ArrayList<Integer>> Adj,
                                 ArrayList<Boolean> visited, int level)
{

    // Mark source as visited
    visited.set(src, true);

    // Update the maximum distance
    distance = Math.max(distance, level);

    // Traverse the adjacency list of the current
    // source node
    for(int child : Adj.get(src))
    {

        // Recursively call for the child node
        if ((child != src) &&
            (visited.get(child) == false))
        {
            dfs(child, Adj, visited, level + 1);
        }
    }

    // Backtracking step
    visited.set(src, false);
}

// Function to calculate maximum length of the path
// ending at vertex v from any source node
private static int maximumLength(int[][] mat, int v)
{

    // Stores the maximum length of the path ending at
    // vertex v
    distance = 0;

    // Stores the size of the matrix
    int N = mat[0].length;

    ArrayList<Boolean> visited = new ArrayList<Boolean>();

    for(int i = 0; i < N; i++)
    {
        visited.add(false);
    }

    // Stores the adjacency list of the given graph
    ArrayList<
    ArrayList<Integer>> Adj = new ArrayList<
                                  ArrayList<Integer>>(N);

    for(int i = 0; i < N; i++)
    {
        Adj.add(new ArrayList<Integer>());
    }

    int i, j;

    // Traverse the matrix to create adjacency list
    for(i = 0; i < mat[0].length; i++)
    {
        for(j = 0; j < mat.length; j++)
        {
            if (mat[i][j] == 1)
            {
                Adj.get(i).add(j);
            }
        }
    }

    // Perform DFS Traversal to update
    // the maximum distance
    dfs(v, Adj, visited, 0);
    return distance;
}

// Driver code
public static void main(String[] args)
{
    int[][] mat = { { 0, 1, 0, 0 },
                    { 1, 0, 1, 1 },
                    { 0, 1, 0, 0 },
                    { 0, 1, 0, 0 } };
    int v = 2;

    System.out.print(maximumLength(mat, v));
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach
visited = [False for i in range(4)]

# Function to perform DFS Traversal from
# source node to the deepest node and
# update maximum distance to the deepest node
def dfs(src, Adj, level, distance):

    global visited

    # Mark source as visited
    visited[src] = True

    # Update the maximum distance
    distance = max(distance, level)

    # Traverse the adjacency list
    # of the current source node
    for child in Adj[src]:

        # Recursively call
        # for the child node
        if (child != src and visited[child] == False):
            dfs(child, Adj, level + 1, distance)

    # Backtracking step
    visited[src] = False

# Function to calculate maximum length
# of the path ending at vertex V from
# any source node
def maximumLength(mat, V):

    # Stores the maximum length of
    # the path ending at vertex V
    distance = 0

    # Stores the size of the matrix
    N = len(mat)

    # Stores the adjacency list
    # of the given graph
    Adj = [[] for i in range(N)]

    # Traverse the matrix to
    # create adjacency list
    for i in range(N):
        for j in range(N):
            if (mat[i][j] == 1):
                Adj[i].append(j)

    # Perform DFS Traversal to
    # update the maximum distance
    dfs(V, Adj, 0, distance)

    return distance + 2

# Driver Code
if __name__ == '__main__':

    mat = [ [ 0, 1, 0, 0 ],
            [ 1, 0, 1, 1 ],
            [ 0, 1, 0, 0 ],
            [ 0, 1, 0, 0 ] ]

    V = 2

    print(maximumLength(mat, V))

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

static int distance;

// Function to perform DFS Traversal from
// source node to the deepest node and
// update maximum distance to the deepest node
static void dfs(int src, List<List<int>> Adj,
                List<bool> visited, int level)
{

    // Mark source as visited
    visited[src] = true;

    // Update the maximum distance
    distance = Math.Max(distance, level);

    // Traverse the adjacency list of
    // the current source node
    foreach(int child in Adj[src])
    {

        // Recursively call for the child node
        if ((child != src) &&
            (visited[child] == false))
        {
            dfs(child, Adj, visited, level + 1);
        }
    }

    // Backtracking step
    visited[src] = false;
}

// Function to calculate maximum length of the path
// ending at vertex v from any source node
static int maximumLength(int[,] mat, int v)
{

    // Stores the maximum length of the path
    // ending at vertex v
    distance = 0;

    // Stores the size of the matrix
    int N = mat.GetLength(0);

    List<bool> visited = new List<bool>();

    for(int i = 0; i < N; i++)
    {
        visited.Add(false);
    }

    // Stores the adjacency list of the given graph
    List<List<int>> Adj = new List<List<int>>(N);

    for(int i = 0; i < N; i++)
    {
        Adj.Add(new List<int>());
    }

    // Traverse the matrix to create adjacency list
    for(int i = 0; i < mat.GetLength(0); i++)
    {
        for(int j = 0; j < mat.GetLength(0); j++)
        {
            if (mat[i, j] == 1)
            {
                Adj[i].Add(j);
            }
        }
    }

    // Perform DFS Traversal to update
    // the maximum distance
    dfs(v, Adj, visited, 0);
    return distance;
}

// Driver code
static void Main()
{
    int[,] mat = { { 0, 1, 0, 0 },
                   { 1, 0, 1, 1 },
                   { 0, 1, 0, 0 },
                   { 0, 1, 0, 0 } };
    int v = 2;

    Console.Write(maximumLength(mat, v));
}
}

// This code is contributed by mukesh07
```

## java 描述语言

```
<script>
// Javascript program for the above approach

var distance = 0;

// Function to perform DFS Traversal from source node to
// the deepest node and update maximum distance to the
// deepest node
function dfs(src, Adj, visited, level)
{

    // Mark source as visited
    visited[src] = true;

    // Update the maximum distance
    distance = Math.max(distance, level);

    // Traverse the adjacency list of the current
    // source node
    for(var child of Adj[src])
    {

        // Recursively call for the child node
        if ((child != src) &&
            (visited[child] == false))
        {
            dfs(child, Adj, visited, level + 1);
        }
    }

    // Backtracking step
    visited[src] = false;
}

// Function to calculate maximum length of the path
// ending at vertex v from any source node
function maximumLength(mat, v)
{

    // Stores the maximum length of the path ending at
    // vertex v
    distance = 0;

    // Stores the size of the matrix
    var N = mat[0].length;

    var visited = [];

    for(var i = 0; i < N; i++)
    {
        visited.push(false);
    }

    // Stores the adjacency list of the given graph
    var Adj = Array.from(Array(N), ()=>Array());

    var i, j;

    // Traverse the matrix to create adjacency list
    for(i = 0; i < mat[0].length; i++)
    {
        for(j = 0; j < mat.length; j++)
        {
            if (mat[i][j] == 1)
            {
                Adj[i].push(j);
            }
        }
    }

    // Perform DFS Traversal to update
    // the maximum distance
    dfs(v, Adj, visited, 0);
    return distance;
}

// Driver code
var mat = [ [ 0, 1, 0, 0 ],
                [ 1, 0, 1, 1 ],
                [ 0, 1, 0, 0 ],
                [ 0, 1, 0, 0 ] ];
var v = 2;

document.write(maximumLength(mat, v));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*