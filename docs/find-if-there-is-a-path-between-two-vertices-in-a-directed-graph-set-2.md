# 查找有向图中两个顶点之间是否有路径|集合 2

> 原文:[https://www . geesforgeks . org/find-如果有向图集中的两个顶点之间有路径-2/](https://www.geeksforgeeks.org/find-if-there-is-a-path-between-two-vertices-in-a-directed-graph-set-2/)

给定一个有向图和其中的两个顶点，检查是否有从第一个给定顶点到第二个给定顶点的路径。

**示例:**

> **考虑以下图表:**
> 
> [![](img/40ca76ea468053c881ac72e49e82f1e2.png)](https://media.geeksforgeeks.org/wp-content/uploads/bfs-5.png)
> 
> **输入:** (u，v) = (1，3)
> **输出:**是
> **说明:**
> 有一条从 1 到 3 的路径，1 - > 2 - > 3
> 
> **输入:** (u，v) = (3，6)
> **输出:**否
> **说明:**
> 没有从 3 到 6 的路径

这个问题的基于 BFS 或 T2 DFS 的解决方案在此讨论。
**方法:**这里我们将讨论使用[弗洛伊德沃肖尔算法](https://www.geeksforgeeks.org/floyd-warshall-algorithm-dp-16/)的基于[动态编程的解决方案。](https://www.geeksforgeeks.org/dynamic-programming/)

*   创建一个布尔 2D 矩阵 **mat** ，其中**mat【I】【j】**将为真，如果有一条从顶点 **i** 到 **j** 的路径。
*   对于每个起始顶点 **i** 和结束顶点 **j** 迭代所有中间顶点 **k** ，并检查是否存在路径 **i** 到 **j** 到 **k** ，然后将**mat【I】【j】**标记为真。
*   最后，检查 **mat[u][v]** 是否为真，然后返回真，否则返回假。

下面是上述方法的实现:

## C++

```
// C++ program to find if there is a
// path between two vertices in a
// directed graph using Dynamic Programming

#include <bits/stdc++.h>
using namespace std;
#define X 6
#define Z 2

// function to find if there is a
// path between two vertices in a
// directed graph
bool existPath(int V, int edges[X][Z],
               int u, int v)
{
    // dp matrix
    bool mat[V][V];
    memset(mat, false, sizeof(mat));

    // set dp[i][j]=true if there is
    // edge between i to j
    for (int i = 0; i < X; i++)
        mat[edges[i][0]][edges[i][1]] = true;

    // check for all intermediate vertex
    for (int k = 0; k < V; k++) {
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {

                mat[i][j] = mat[i][j]
                            || mat[i][k]
                                   && mat[k][j];
            }
        }
    }

    // if vertex is invalid
    if (u >= V || v >= V) {
        return false;
    }

    // if there is a path
    if (mat[u][v])
        return true;
    return false;
}

// Driver function
int main()
{
    int V = 4;
    int edges[X][Z]
        = { { 0, 2 }, { 0, 1 },
            { 1, 2 }, { 2, 3 },
            { 2, 0 }, { 3, 3 } };
    int u = 1, v = 3;

    if (existPath(V, edges, u, v))
        cout << "Yes\n";
    else
        cout << "No\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if there is a path
// between two vertices in a directed graph
// using Dynamic Programming
import java.util.*;

class GFG{

static final int X = 6;
static final int Z = 2;

// Function to find if there is a
// path between two vertices in a
// directed graph
static boolean existPath(int V, int edges[][],
                         int u, int v)
{

    // mat matrix
    boolean [][]mat = new boolean[V][V];

    // set mat[i][j]=true if there is
    // edge between i to j
    for (int i = 0; i < X; i++)
        mat[edges[i][0]][edges[i][1]] = true;

    // Check for all intermediate vertex
    for(int k = 0; k < V; k++)
    {
        for(int i = 0; i < V; i++)
        {
            for(int j = 0; j < V; j++)
            {
                mat[i][j] = mat[i][j] ||
                            mat[i][k] &&
                            mat[k][j];
            }
        }
    }

    // If vertex is invalid
    if (u >= V || v >= V)
    {
        return false;
    }

    // If there is a path
    if (mat[u][v])
        return true;
    return false;
}

// Driver code
public static void main(String[] args)
{
    int V = 4;
    int edges[][] = { { 0, 2 }, { 0, 1 },
                      { 1, 2 }, { 2, 3 },
                      { 2, 0 }, { 3, 3 } };
    int u = 1, v = 3;

    if (existPath(V, edges, u, v))
        System.out.print("Yes\n");
    else
        System.out.print("No\n");
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find if there
# is a path between two vertices in a
# directed graph using Dynamic Programming
X = 6
Z = 2

# Function to find if there is a
# path between two vertices in a
# directed graph
def existPath(V, edges, u, v):

    # dp matrix
    mat = [[False for i in range(V)]
                  for j in range(V)]

    # Set dp[i][j]=true if there is
    # edge between i to j
    for i in range(X):
        mat[edges[i][0]][edges[i][1]] = True

    # Check for all intermediate vertex
    for k in range(V):
        for i in range(V):
            for j in range(V):
                mat[i][j] = (mat[i][j] or
                             mat[i][k] and
                             mat[k][j])

    # If vertex is invalid
    if (u >= V or v >= V):
        return False

    # If there is a path
    if (mat[u][v]):
        return True

    return False

# Driver code
V = 4
edges = [ [ 0, 2 ], [ 0, 1 ],
          [ 1, 2 ], [ 2, 3 ],
          [ 2, 0 ], [ 3, 3 ] ]

u, v = 1, 3

if (existPath(V, edges, u, v)):
    print("Yes")
else:
    print("No")

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to find if there is a path
// between two vertices in a directed graph
// using Dynamic Programming
using System;
class GFG{

static readonly int X = 6;
static readonly int Z = 2;

// Function to find if there is a
// path between two vertices in a
// directed graph
static bool existPath(int V, int [,]edges,
                      int u, int v)
{

    // mat matrix
    bool [,]mat = new bool[V, V];

    // set mat[i,j]=true if there is
    // edge between i to j
    for (int i = 0; i < X; i++)
        mat[edges[i, 0], edges[i, 1]] = true;

    // Check for all intermediate vertex
    for(int k = 0; k < V; k++)
    {
        for(int i = 0; i < V; i++)
        {
            for(int j = 0; j < V; j++)
            {
                mat[i, j] = mat[i, j] ||
                            mat[i, k] &&
                            mat[k, j];
            }
        }
    }

    // If vertex is invalid
    if (u >= V || v >= V)
    {
        return false;
    }

    // If there is a path
    if (mat[u, v])
        return true;
    return false;
}

// Driver code
public static void Main(String[] args)
{
    int V = 4;
    int [,]edges = { { 0, 2 }, { 0, 1 },
                     { 1, 2 }, { 2, 3 },
                     { 2, 0 }, { 3, 3 } };
    int u = 1, v = 3;

    if (existPath(V, edges, u, v))
        Console.Write("Yes\n");
    else
        Console.Write("No\n");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to find if there is a path
// between two vertices in a directed graph
// using Dynamic Programming

var X = 6;
var Z = 2;

// Function to find if there is a
// path between two vertices in a
// directed graph
function existPath(V, edges, u, v)
{

    // mat matrix
    var mat = Array.from(Array(V), ()=>Array(V));

    // set mat[i,j]=true if there is
    // edge between i to j
    for (var i = 0; i < X; i++)
        mat[edges[i][0]][edges[i][1]] = true;

    // Check for all intermediate vertex
    for(var k = 0; k < V; k++)
    {
        for(var i = 0; i < V; i++)
        {
            for(var j = 0; j < V; j++)
            {
                mat[i][j] = mat[i][j] ||
                            mat[i][k] &&
                            mat[k][j];
            }
        }
    }

    // If vertex is invalid
    if (u >= V || v >= V)
    {
        return false;
    }

    // If there is a path
    if (mat[u][v])
        return true;
    return false;
}

// Driver code
var V = 4;
var edges = [ [ 0, 2 ], [ 0, 1 ],
                 [ 1, 2 ], [ 2, 3 ],
                 [ 2, 0 ], [ 3, 3 ] ];
var u = 1, v = 3;
if (existPath(V, edges, u, v))
    document.write("Yes<br>");
else
    document.write("No<br>");

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(V<sup>3</sup>)*
***辅助空间:** O ( V <sup>2</sup> )*