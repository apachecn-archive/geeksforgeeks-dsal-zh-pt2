# 计算节点对，它们之间的最小距离等于它们与根的距离之差

> 原文:[https://www . geeksforgeeks . org/count-节点对之间的最小距离等于它们与根的距离差/](https://www.geeksforgeeks.org/count-pairs-of-nodes-having-minimum-distance-between-them-equal-to-the-difference-of-their-distances-from-root/)

给定由从**【1，N】**取值的 **N** 节点组成的 [N 元树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)，其中节点 **1** 是根，任务是计算节点对，它们之间的最小距离等于两个节点到根的距离之差。

**示例:**

> **输入:** N = 3，边[][] = {{1，2}，{1，3}}，下面是树:
> 1
> /\
> 2 3
> T6】输出: 5
> **说明:**以下配对满足条件:{(1，1)、(2，2)、(3，3)、(2，1)、(3，1)}。
> 
> **输入:** N = 4，边[][] = {{1，2}，{1，3}，{2，4}}，下面是树:
> 1
> /\
> 2 3
> |
> 4
> **输出:** 8

**天真方法:**最简单的方法是找到所有可能的对之间的距离 **(i，j)** 并检查每对节点 **(i，j)** ，**距离(I，j) =距离(1，I)–距离(1，j)** 是否使用[深度优先搜索遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以基于以下观察进行优化:

> 从节点 **X** 到节点 **X** 的祖先的最小距离满足上述标准。因此，任务简化为[寻找树](https://www.geeksforgeeks.org/print-ancestors-of-a-given-node-in-binary-tree/)每个节点的所有祖先。

按照以下步骤解决问题:

*   初始化一个变量，比如**和**，来存储节点对的计数。
*   从根节点开始执行 [DFS 遍历，参数为**当前节点**、**父节点**和](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) [**节点深度**](https://www.geeksforgeeks.org/get-level-of-a-node-in-a-binary-tree/) 直到当前节点。
*   以**当前**节点为**父**节点，**深度**增加 **1** ，递归执行每个节点的**子**节点上的 DFS 遍历。
*   在每次调用中，将当前节点的[深度添加到变量**和**中。](https://www.geeksforgeeks.org/level-ancestor-problem/)
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Stores the count of pairs
long long ans = 0;

// Store the adjacency list of
// the connecting vertex
vector<int> adj[int(1e5) + 1];

// Function for theto perform DFS
// traversal of the given tree
void dfsUtil(int u, int par, int depth)
{
    // Traverse the adjacency list
    // of the current node u
    for (auto it : adj[u]) {

        // If the current node
        // is the parent node
        if (it != par) {
            dfsUtil(it, u, depth + 1);
        }
    }

    // Add number of ancestors, which
    // is same as depth of the node
    ans += depth;
}

// Function for DFS traversal of
// the given tree
void dfs(int u, int par, int depth)
{
    dfsUtil(u, par, depth);

    // Print the result
    cout << ans << endl;
}

// Function to find the count of pairs
// such that the minimum distance
// between them is equal to the difference
// between distance of the nodes from root node
void countPairs(vector<vector<int> > edges)
{
    for (int i = 0; i < edges.size(); i++) {

        int u = edges[i][0];
        int v = edges[i][1];

        // Add edges to adj[]
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    dfs(1, 1, 1);
}

// Driver Code
int main()
{
    vector<vector<int> > edges
        = { { 1, 2 }, { 1, 3 }, { 2, 4 } };

    countPairs(edges);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Stores the count of pairs
static int ans = 0;

// Store the adjacency list of
// the connecting vertex
static ArrayList<Integer> []adj = new ArrayList[(int)(1e5) + 1];
static{
    for(int i = 0; i < adj.length; i++)
        adj[i] = new ArrayList<>();
}

// Function for theto perform DFS
// traversal of the given tree
static void dfsUtil(int u, int par, int depth)
{

    // Traverse the adjacency list
    // of the current node u
    for (int it : adj[u]) {

        // If the current node
        // is the parent node
        if (it != par) {
            dfsUtil(it, u, depth + 1);
        }
    }

    // Add number of ancestors, which
    // is same as depth of the node
    ans += depth;
}

// Function for DFS traversal of
// the given tree
static void dfs(int u, int par, int depth)
{
    dfsUtil(u, par, depth);

    // Print the result
    System.out.print(ans +"\n");
}

// Function to find the count of pairs
// such that the minimum distance
// between them is equal to the difference
// between distance of the nodes from root node
static void countPairs(int [][]edges)
{
    for (int i = 0; i < edges.length; i++) {

        int u = edges[i][0];
        int v = edges[i][1];

        // Add edges to adj[]
        adj[u].add(v);
        adj[v].add(u);
    }

    dfs(1, 1, 1);
}

// Driver Code
public static void main(String[] args)
{
    int [][]edges
        = { { 1, 2 }, { 1, 3 }, { 2, 4 } };

    countPairs(edges);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Stores the count of pairs
ans = 0

# Store the adjacency list of
# the connecting vertex
adj = [[] for i in range(10**5+1)]

# Function for theto perform DFS
# traversal of the given tree
def dfsUtil(u, par, depth):
    global adj, ans

    # Traverse the adjacency list
    # of the current node u
    for it in adj[u]:

        # If the current node
        # is the parent node
        if (it != par):
            dfsUtil(it, u, depth + 1)

    # Add number of ancestors, which
    # is same as depth of the node
    ans += depth

# Function for DFS traversal of
# the given tree
def dfs(u, par, depth):
    global ans
    dfsUtil(u, par, depth)

    # Print result
    print (ans)

# Function to find the count of pairs
# such that the minimum distance
# between them is equal to the difference
# between distance of the nodes from root node
def countPairs(edges):
    global adj
    for i in range(len(edges)):
        u = edges[i][0]
        v = edges[i][1]

        # Add edges to adj[]
        adj[u].append(v)
        adj[v].append(u)
    dfs(1, 1, 1)

# Driver Code
if __name__ == '__main__':
    edges = [ [ 1, 2 ], [ 1, 3 ], [ 2, 4 ] ]

    countPairs(edges)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG
{

// Stores the count of pairs
static int ans = 0;

// Store the adjacency list of
// the connecting vertex
static List<int> []adj = new List<int>[(int)(1e5) + 1];

// Function for theto perform DFS
// traversal of the given tree
static void dfsUtil(int u, int par, int depth)
{

    // Traverse the adjacency list
    // of the current node u
    foreach (int it in adj[u]) {

        // If the current node
        // is the parent node
        if (it != par) {
            dfsUtil(it, u, depth + 1);
        }
    }

    // Add number of ancestors, which
    // is same as depth of the node
    ans += depth;
}

// Function for DFS traversal of
// the given tree
static void dfs(int u, int par, int depth)
{
    dfsUtil(u, par, depth);

    // Print the result
    Console.Write(ans +"\n");
}

// Function to find the count of pairs
// such that the minimum distance
// between them is equal to the difference
// between distance of the nodes from root node
static void countPairs(int [,]edges)
{
    for (int i = 0; i < edges.GetLength(0); i++)
    {

        int u = edges[i,0];
        int v = edges[i,1];

        // Add edges to []adj
        adj[u].Add(v);
        adj[v].Add(u);
    }

    dfs(1, 1, 1);
}

// Driver Code
public static void Main(String[] args)
{
    int [,]edges
        = { { 1, 2 }, { 1, 3 }, { 2, 4 } };

    for(int i = 0; i < adj.GetLength(0); i++)
        adj[i] = new List<int>();
    countPairs(edges);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Stores the count of pairs
var ans = 0;

// Store the adjacency list of
// the connecting vertex
var adj = Array.from(Array(100001), ()=>Array());

// Function for theto perform DFS
// traversal of the given tree
function dfsUtil(u, par, depth)
{
    // Traverse the adjacency list
    // of the current node u
    adj[u].forEach(it => {

        // If the current node
        // is the parent node
        if (it != par) {
            dfsUtil(it, u, depth + 1);
        }
    });

    // Add number of ancestors, which
    // is same as depth of the node
    ans += depth;
}

// Function for DFS traversal of
// the given tree
function dfs(u, par, depth)
{
    dfsUtil(u, par, depth);

    // Print the result
    document.write( ans + "<br>");
}

// Function to find the count of pairs
// such that the minimum distance
// between them is equal to the difference
// between distance of the nodes from root node
function countPairs(edges)
{
    for (var i = 0; i < edges.length; i++) {

        var u = edges[i][0];
        var v = edges[i][1];

        // Add edges to adj[]
        adj[u].push(v);
        adj[v].push(u);
    }

    dfs(1, 1, 1);
}

// Driver Code
var edges
    = [ [ 1, 2 ], [ 1, 3 ], [ 2, 4 ] ];
countPairs(edges);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)