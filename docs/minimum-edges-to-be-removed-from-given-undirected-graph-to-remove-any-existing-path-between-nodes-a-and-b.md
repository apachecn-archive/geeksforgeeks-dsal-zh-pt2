# 要从给定无向图中移除的最小边，以移除节点 A 和 B 之间的任何现有路径

> 原文:[https://www . geeksforgeeks . org/从给定的无向图中移除最小边以移除节点 a 和 b 之间的任何现有路径/](https://www.geeksforgeeks.org/minimum-edges-to-be-removed-from-given-undirected-graph-to-remove-any-existing-path-between-nodes-a-and-b/)

给定两个整数 **N** 和 **M** 表示[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)中[顶点和边](https://www.geeksforgeeks.org/mathematics-graph-theory-basics/)的数量，以及大小为 **M** 的数组**边【】【】**，表示**边【I】【0】**和**边【I】【1】**之间的边，任务是找到与节点 **B** 直接相连的最小边，这些边必须被移除，以便

**示例:**

> **输入:** N = 4，A = 3，B = 2，边[][] = {{3，1}，{3，4}，{1，2}，{4，2}}
> **输出:** 2
> **解释:**索引 2 和 3 处的边，即{1，2}和{4，2}必须被移除，因为它们都在从顶点 A 到顶点 B 的路径中
> 
> **输入:** N = 6，A = 1，B = 6，边[][] = {{1，2}，{1，6}，{2，6}，{1，4}，{4，6}，{4，3}，{2，4}}
> **输出:** 3

**方法:**给定的问题可以使用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)算法来解决。可以观察到所有与结束顶点 **B** 相关联的边，以及存在于从开始节点 **A** 到结束节点 **B** 的任何路径中的边都必须被移除。因此，从节点 **A** 开始执行**DFS**[](https://www.geeksforgeeks.org/detect-cycle-undirected-graph/)**，并维护其中的所有访问顶点。按照以下步骤解决问题:**

*   **创建一个[邻接矩阵](http://www.geeksforgeeks.org/graph-and-its-representations/) **g[][]** ，它存储两个节点之间的边。**
*   **初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **v[]** ，标记从节点 **A** 可以到达的节点。**
*   **创建一个变量 **cnt** ，存储需要删除的节点数。最初， **cnt = 0** 。**
*   **遍历所有节点，如果从 **A** 可以到达，并且直接连接到 **B** ，则增加 **cnt** 的值。**
*   **存储在 **cnt** 中的值是要求的答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function for Depth first Search
void dfs(int s, vector<vector<int> > g,
         vector<int>& v)
{
    for (auto i : g[s]) {

        // If current vertex is
        // not visited yet
        if (!v[i]) {
            v[i] = 1;

            // Recursive call for
            // dfs function
            dfs(i, g, v);
        }
    }
}

// Function to find the out the minimum
// number of edges that must be removed
int deleteEdges(int n, int m, int a, int b,
                vector<vector<int> > edges)
{
    // Creating Adjacency Matrix
    vector<vector<int> > g(n, vector<int>());
    for (int i = 0; i < m; i++) {
        g[edges[i][0] - 1].push_back(edges[i][1] - 1);
        g[edges[i][1] - 1].push_back(edges[i][0] - 1);
    }

    // Vector for marking visited
    vector<int> v(n, 0);
    v[a - 1] = 1;

    // Calling dfs function
    dfs(a - 1, g, v);

    // Stores the final count
    int cnt = 0;

    for (int i = 0; i < n; i++) {

        // If current node can not
        // be visited from node A
        if (v[i] == 0)
            continue;
        for (int j = 0; j < g[i].size(); j++) {

            // If a node between current
            // node and node b exist
            if (g[i][j] == b - 1) {
                cnt++;
            }
        }
    }

    // Return Answer
    return cnt;
}

// Driver Code
int main()
{
    int N = 6;
    int M = 7;
    int A = 1;
    int B = 6;
    vector<vector<int> > edges{
        { 1, 2 }, { 5, 2 }, { 2, 4 },
        { 2, 3 }, { 3, 6 }, { 4, 6 }, { 5, 6 }
    };

    cout << deleteEdges(N, M, A, B, edges);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function for Depth first Search
static void dfs(int s, Vector<Integer> [] g,
         int[] v)
{
    for (int i : g[s]) {

        // If current vertex is
        // not visited yet
        if (v[i] == 0) {
            v[i] = 1;

            // Recursive call for
            // dfs function
            dfs(i, g, v);
        }
    }
}

// Function to find the out the minimum
// number of edges that must be removed
static int deleteEdges(int n, int m, int a, int b,
                int[][] edges)
{

    // Creating Adjacency Matrix
    Vector<Integer> []g = new Vector[n];
    for (int i = 0; i < g.length; i++)
        g[i] = new Vector<Integer>();
    for (int i = 0; i < m; i++) {
        g[edges[i][0] - 1].add(edges[i][1] - 1);
        g[edges[i][1] - 1].add(edges[i][0] - 1);
    }

    // Vector for marking visited
    int []v = new int[n];
    v[a - 1] = 1;

    // Calling dfs function
    dfs(a - 1, g, v);

    // Stores the final count
    int cnt = 0;

    for (int i = 0; i < n; i++) {

        // If current node can not
        // be visited from node A
        if (v[i] == 0)
            continue;
        for (int j = 0; j < g[i].size(); j++) {

            // If a node between current
            // node and node b exist
            if (g[i].get(j) == b - 1) {
                cnt++;
            }
        }
    }

    // Return Answer
    return cnt;
}

// Driver Code
public static void main(String[] args)
{
    int N = 6;
    int M = 7;
    int A = 1;
    int B = 6;
    int[][] edges ={
        { 1, 2 }, { 5, 2 }, { 2, 4 },
        { 2, 3 }, { 3, 6 }, { 4, 6 }, { 5, 6 }
    };

    System.out.print(deleteEdges(N, M, A, B, edges));

}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python program for the above approach

# Function for Depth first Search
def dfs(s, g, v):
    for i in g[s]:

        # If current vertex is
        # not visited yet
        if not v[i]:
            v[i] = 1

            # Recursive call for
            # dfs function
            dfs(i, g, v)

# Function to find the out the minimum
# number of edges that must be removed
def deleteEdges(n, m, a, b, edges):

    # Creating Adjacency Matrix
    g = [0] * m
    for i in range(len(g)):
        g[i] = []

    for i in range(m):
        g[edges[i][0] - 1].append(edges[i][1] - 1)
        g[edges[i][1] - 1].append(edges[i][0] - 1)

    # Vector for marking visited
    v = [0] * n
    v[a - 1] = 1

    # Calling dfs function
    dfs(a - 1, g, v)

    # Stores the final count
    cnt = 0

    for i in range(n):

        # If current node can not
        # be visited from node A
        if (v[i] == 0):
            continue

        for j in range(len(g[i])):

            # If a node between current
            # node and node b exist
            if (g[i][j] == b - 1):
                cnt += 1

    # Return Answer
    return cnt

# Driver Code
N = 6
M = 7
A = 1
B = 6
edges = [[1, 2], [5, 2], [2, 4],
         [2, 3], [3, 6], [4, 6],
         [5, 6]]

print(deleteEdges(N, M, A, B, edges))

# This code is contributed by gfgking
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{

// Function for Depth first Search
static void dfs(int s, List<int> [] g,
         int[] v)
{
    foreach (int i in g[s]) {

        // If current vertex is
        // not visited yet
        if (v[i] == 0) {
            v[i] = 1;

            // Recursive call for
            // dfs function
            dfs(i, g, v);
        }
    }
}

// Function to find the out the minimum
// number of edges that must be removed
static int deleteEdges(int n, int m, int a, int b,
                int[,] edges)
{

    // Creating Adjacency Matrix
    List<int> []g = new List<int>[n];
    for (int i = 0; i < g.Length; i++)
        g[i] = new List<int>();
    for (int i = 0; i < m; i++) {
        g[edges[i,0] - 1].Add(edges[i,1] - 1);
        g[edges[i,1] - 1].Add(edges[i,0] - 1);
    }

    // List for marking visited
    int []v = new int[n];
    v[a - 1] = 1;

    // Calling dfs function
    dfs(a - 1, g, v);

    // Stores the readonly count
    int cnt = 0;

    for (int i = 0; i < n; i++) {

        // If current node can not
        // be visited from node A
        if (v[i] == 0)
            continue;
        for (int j = 0; j < g[i].Count; j++) {

            // If a node between current
            // node and node b exist
            if (g[i][j] == b - 1) {
                cnt++;
            }
        }
    }

    // Return Answer
    return cnt;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 6;
    int M = 7;
    int A = 1;
    int B = 6;
    int[,] edges ={
        { 1, 2 }, { 5, 2 }, { 2, 4 },
        { 2, 3 }, { 3, 6 }, { 4, 6 }, { 5, 6 }
    };

    Console.Write(deleteEdges(N, M, A, B, edges));
}
}

// This code is contributed by shikhasingrajput
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

// Function for Depth first Search
function dfs(s, g, v)
{
    for(let i of g[s])
    {

        // If current vertex is
        // not visited yet
        if (!v[i])
        {
            v[i] = 1;

            // Recursive call for
            // dfs function
            dfs(i, g, v);
        }
    }
}

// Function to find the out the minimum
// number of edges that must be removed
function deleteEdges(n, m, a, b, edges)
{

    // Creating Adjacency Matrix
    let g = new Array(m);
    for(let i = 0; i < g.length; i++)
    {
        g[i] = [];
    }

    for(let i = 0; i < m; i++)
    {
        g[edges[i][0] - 1].push(edges[i][1] - 1);
        g[edges[i][1] - 1].push(edges[i][0] - 1);
    }

    // Vector for marking visited
    let v = new Array(n).fill(0)
    v[a - 1] = 1;

    // Calling dfs function
    dfs(a - 1, g, v);

    // Stores the final count
    let cnt = 0;

    for(let i = 0; i < n; i++)
    {

        // If current node can not
        // be visited from node A
        if (v[i] == 0)
            continue;

        for(let j = 0; j < g[i].length; j++)
        {

            // If a node between current
            // node and node b exist
            if (g[i][j] == b - 1)
            {
                cnt++;
            }
        }
    }

    // Return Answer
    return cnt;
}

// Driver Code
let N = 6;
let M = 7;
let A = 1;
let B = 6;
let edges = [ [ 1, 2 ], [ 5, 2 ], [ 2, 4 ],
              [ 2, 3 ], [ 3, 6 ], [ 4, 6 ],
              [ 5, 6 ] ];

document.write(deleteEdges(N, M, A, B, edges));

// This code is contributed by Potta Lokesh

</script>
```

****Output**

```
3
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**