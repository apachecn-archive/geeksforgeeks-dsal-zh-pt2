# 无向图中最大成本路径，使得没有边被连续访问两次

> 原文:[https://www . geesforgeks . org/最大成本-无向图中的路径-连续两次访问无边缘/](https://www.geeksforgeeks.org/maximum-cost-path-in-an-undirected-graph-such-that-no-edge-is-visited-twice-in-a-row/)

给定一个有 **N** 个顶点和 **M** 条边的无向图，每个顶点与一个代价相关联，并给出一个源顶点 **S** 。任务是找到从源顶点**到 S** 的最大成本路径，使得没有边被连续访问 2 次或更多次。

**示例:**

> **输入:** N = 5，M = 5，来源= 1，成本[] = {2，2，8，6，9}，下面是给定的图形:
> 
> ![](img/5e7bc662fba299d94f2a6a0723172471.png)
> 
> **输出:** 21
> **说明:**
> 最大成本路径矩阵给出为:
> 1->2->0->1->4
> 成本= 2 + 8 + 2 + 2 + 9 = 21
> 
> **输入:** N = 8，M = 8，来源= 3，成本[] = {10，11，4，12，3，4，7，9}
> 
> ![](img/d00a68ca752a39d01dc6c68194bc29c4.png)
> 
> **输出:** 46
> 
> **说明:**
> 最大成本路径矩阵给出为:
> 3->0->2->1->7

**方法:**思路是检查图中是否存在[循环，然后需要遍历循环的所有顶点，然后遍历图向代价最大的叶子节点。如果循环不存在，则问题陈述转换为在任何有向图中寻找最大成本路径。](https://www.geeksforgeeks.org/detect-cycle-undirected-graph/)

以下是程序中使用的声明:

*   **dp[i]:** 存储遍历节点**‘I’**及其所有子节点的总开销。
*   **vis[i]:** 标记已经访问过的节点。
*   **canTake:** 存储除叶顶点及其子节点(如果存在)之外的最大代价路径的所有节点的合成和。
*   **best:** 存储最大开销叶节点及其子节点(如果存在)的开销。
*   **检查:**布尔变量用作图中查找循环的标志，当找到循环时，其值变为 0。

以下是步骤:

1.  执行 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)，标志变量检查设置为**‘1’**，最初表示未找到循环。
2.  同时为每个节点建立 **dp[]** ，最大开销更新到该遍历节点。
3.  如果发现相邻节点已经被访问，并且它不是父节点，则找到循环并将**检查**的值设置为 **0** 。
4.  将循环的所有节点的成本加到**可以计算**。
5.  遍历遍历节点的相邻节点后，没有发现循环，则表示从循环到叶顶点的路径开销，如果 **dp[i]** 大于**最佳**，则将**最佳**更新为 **dp[i]** 。
6.  遍历完图形后，打印**的和即可得到**和**的最佳**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// To store the resulting
// sum of the cost
int canTake;

// To store largest
// cost leaf vertex
int best;

vector<int> dp;
vector<bool> vis;

// DFS Traversal to find the update
// the maximum cost of from any
// node to leaf
int dfs(vector<vector<int> >& g,
        int* cost, int u, int pre)
{

    // Mark vertex as visited
    vis[u] = true;

    // Store vertex initial cost
    dp[u] = cost[u];

    // Initially assuming edge
    // not to be traversed
    bool check = 1;

    int cur = cost[u];
    for (auto& x : g[u]) {

        // Back edge found so,
        // edge can be part of
        // traversal
        if (vis[x] && x != pre) {
            check = 0;
        }

        // New vertex is found
        else if (!vis[x]) {

            // Bitwise AND the current
            // check with the returned
            // check by the previous
            // DFS Call
            check &= dfs(g, cost, x, u);

            // Adds parent and its
            // children cost
            cur = max(cur,
                      cost[u] + dp[x]);
        }
    }

    // Updates total cost of parent
    // including child nodes
    dp[u] = cur;

    // Edge is part of the cycle
    if (!check) {

        // Add cost of vertex
        // to the answer
        canTake += cost[u];
    }
    else {

        // Updates the largest
        // cost leaf vertex
        best = max(best, dp[u]);
    }

    return check;
}

// Function to find the maximum cost
// from source vertex such that no
// two edges is traversed twice
int FindMaxCost(vector<vector<int> >& g,
                int* cost, int source)
{
    // DFS Call
    dfs(g, cost, source, -1);

    // Print the maximum cost
    cout << canTake + best;
}

// Driver Code
int main()
{
    int n = 5, m = 5;
    dp.resize(n+1);
      vis.resize(n+1);
    // Cost Array
    int cost[] = { 2, 2, 8, 6, 9 };

    vector<vector<int> > g(n);

    // Given Graph
    g[0].push_back(1);
    g[1].push_back(0);
    g[0].push_back(2);
    g[2].push_back(0);
    g[0].push_back(3);
    g[3].push_back(0);
    g[1].push_back(2);
    g[2].push_back(1);
    g[1].push_back(4);
    g[4].push_back(1);

    // Given Source Node
    int source = 1;

    // Function Call
    FindMaxCost(g, cost, source);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int N = 100000;

// To store the resulting
// sum of the cost
static int canTake;

// To store largest
// cost leaf vertex
static int best;

static int []dp = new int[N];
static boolean []vis = new boolean[N];

// DFS Traversal to find the update
// the maximum cost of from any
// node to leaf
static boolean dfs(Vector<Integer> []g,
                   int []cost, int u, int pre)
{

    // Mark vertex as visited
    vis[u] = true;

    // Store vertex initial cost
    dp[u] = cost[u];

    // Initially assuming edge
    // not to be traversed
    boolean check = true;

    int cur = cost[u];
    for(int x : g[u])
    {

        // Back edge found so,
        // edge can be part of
        // traversal
        if (vis[x] && x != pre)
        {
            check = false;
        }

        // New vertex is found
        else if (!vis[x])
        {

            // Bitwise AND the current
            // check with the returned
            // check by the previous
            // DFS Call
            check = dfs(g, cost, x, u) ?
                    false : true;

            // Adds parent and its
            // children cost
            cur = Math.max(cur, cost[u] +
                                  dp[x]);
        }
    }

    // Updates total cost of parent
    // including child nodes
    dp[u] = cur;

    // Edge is part of the cycle
    if (!check)
    {

        // Add cost of vertex
        // to the answer
        canTake += cost[u];
    }
    else
    {

        // Updates the largest
        // cost leaf vertex
        best = Math.max(best, dp[u]);
    }
    return check;
}

// Function to find the maximum cost
// from source vertex such that no
// two edges is traversed twice
static void FindMaxCost(Vector<Integer> [] g,
                        int []cost, int source)
{

    // DFS call
    dfs(g, cost, source, -1);

    // Print the maximum cost
    System.out.print(canTake + best);
}

// Driver Code
public static void main(String[] args)
{
    int n = 5, m = 5;

    // Cost Array
    int cost[] = { 2, 2, 8, 6, 9 };

    @SuppressWarnings("unchecked")
    Vector<Integer> []g = new Vector[n];
    for(int i = 0; i < g.length; i++)
        g[i] = new Vector<Integer>();

    // Given Graph
    g[0].add(1);
    g[1].add(0);
    g[0].add(2);
    g[2].add(0);
    g[0].add(3);
    g[3].add(0);
    g[1].add(2);
    g[2].add(1);
    g[1].add(4);
    g[4].add(1);

    // Given Source Node
    int source = 1;

    // Function call
    FindMaxCost(g, cost, source);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach
N = 100000

# To store the resulting
# sum of the cost
canTake = 0

# To store largest
# cost leaf vertex
best = 0

dp = [0 for i in range(N)]
vis = [0 for i in range(N)]

# DFS Traversal to find the update
# the maximum cost of from any
# node to leaf
def dfs(g, cost, u, pre):

    global canTake, best

    # Mark vertex as visited
    vis[u] = True

    # Store vertex initial cost
    dp[u] = cost[u]

    # Initially assuming edge
    # not to be traversed
    check = 1

    cur = cost[u]

    for x in g[u]:

        # Back edge found so,
        # edge can be part of
        # traversal
        if (vis[x] and x != pre):
            check = 0

        # New vertex is found
        elif (not vis[x]):

            # Bitwise AND the current
            # check with the returned
            # check by the previous
            # DFS Call
            check &= dfs(g, cost, x, u)

            # Adds parent and its
            # children cost
            cur = max(cur, cost[u] + dp[x])

    # Updates total cost of parent
    # including child nodes
    dp[u] = cur

    # Edge is part of the cycle
    if (not check):

        # Add cost of vertex
        # to the answer
        canTake += cost[u]

    else:

        # Updates the largest
        # cost leaf vertex
        best = max(best, dp[u])

    return check

# Function to find the maximum cost
# from source vertex such that no
# two edges is traversed twice
def FindMaxCost(g, cost, source):

    # DFS Call
    dfs(g, cost, source, -1)

    # Print the maximum cost
    print(canTake + best)

# Driver Code
if __name__=='__main__':

    n = 5
    m = 5

    # Cost Array
    cost = [ 2, 2, 8, 6, 9 ]

    g = [[] for i in range(n)]

    # Given Graph
    g[0].append(1)
    g[1].append(0)
    g[0].append(2)
    g[2].append(0)
    g[0].append(3)
    g[3].append(0)
    g[1].append(2)
    g[2].append(1)
    g[1].append(4)
    g[4].append(1)

    # Given Source Node
    source = 1

    # Function Call
    FindMaxCost(g, cost, source)

# This code is contributed by rutvik_56
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

static int N = 100000;

// To store the resulting
// sum of the cost
static int canTake;

// To store largest
// cost leaf vertex
static int best;

static int []dp = new int[N];
static bool []vis = new bool[N];

// DFS Traversal to find the update
// the maximum cost of from any
// node to leaf
static bool dfs(List<int> []g,
                int []cost,
                int u, int pre)
{
  // Mark vertex as visited
  vis[u] = true;

  // Store vertex initial cost
  dp[u] = cost[u];

  // Initially assuming edge
  // not to be traversed
  bool check = true;

  int cur = cost[u];
  foreach(int x in g[u])
  {
    // Back edge found so,
    // edge can be part of
    // traversal
    if (vis[x] && x != pre)
    {
      check = false;
    }

    // New vertex is found
    else if (!vis[x])
    {
      // Bitwise AND the current
      // check with the returned
      // check by the previous
      // DFS Call
      check = dfs(g, cost, x, u) ?
              false : true;

      // Adds parent and its
      // children cost
      cur = Math.Max(cur, cost[u] + dp[x]);
    }
  }

  // Updates total cost of parent
  // including child nodes
  dp[u] = cur;

  // Edge is part of the cycle
  if (!check)
  {
    // Add cost of vertex
    // to the answer
    canTake += cost[u];
  }
  else
  {
    // Updates the largest
    // cost leaf vertex
    best = Math.Max(best, dp[u]);
  }
  return check;
}

// Function to find the maximum cost
// from source vertex such that no
// two edges is traversed twice
static void FindMaxCost(List<int> [] g,
                        int []cost, int source)
{
  // DFS call
  dfs(g, cost, source, -1);

  // Print the maximum cost
  Console.Write(canTake + best);
}

// Driver Code
public static void Main(String[] args)
{
  int n = 5, m = 5;

  // Cost Array
  int []cost = {2, 2, 8, 6, 9};

  List<int> []g = new List<int>[n];

  for(int i = 0; i < g.Length; i++)
    g[i] = new List<int>();

  // Given Graph
  g[0].Add(1);
  g[1].Add(0);
  g[0].Add(2);
  g[2].Add(0);
  g[0].Add(3);
  g[3].Add(0);
  g[1].Add(2);
  g[2].Add(1);
  g[1].Add(4);
  g[4].Add(1);

  // Given Source Node
  int source = 1;

  // Function call
  FindMaxCost(g, cost, source);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for
// the above approach

var N = 100000;

// To store the resulting
// sum of the cost
var canTake = 0;

// To store largest
// cost leaf vertex
var best = 0;

var dp = Array(N).fill(0);
var vis = Array(N).fill(false);

// DFS Traversal to find the update
// the maximum cost of from any
// node to leaf
function dfs(g, cost, u, pre)
{
  // Mark vertex as visited
  vis[u] = true;

  // Store vertex initial cost
  dp[u] = cost[u];

  // Initially assuming edge
  // not to be traversed
  var check = true;

  var cur = cost[u];
  for(var x of g[u])
  {
    // Back edge found so,
    // edge can be part of
    // traversal
    if (vis[x] && x != pre)
    {
      check = false;
    }

    // New vertex is found
    else if (!vis[x])
    {
      // Bitwise AND the current
      // check with the returned
      // check by the previous
      // DFS Call
      check = dfs(g, cost, x, u) ?
              false : true;

      // Adds parent and its
      // children cost
      cur = Math.max(cur, cost[u] + dp[x]);
    }
  }

  // Updates total cost of parent
  // including child nodes
  dp[u] = cur;

  // Edge is part of the cycle
  if (!check)
  {
    // push cost of vertex
    // to the answer
    canTake += cost[u];
  }
  else
  {
    // Updates the largest
    // cost leaf vertex
    best = Math.max(best, dp[u]);
  }
  return check;
}

// Function to find the maximum cost
// from source vertex such that no
// two edges is traversed twice
function FindMaxCost(g, cost, source)
{
  // DFS call
  dfs(g, cost, source, -1);

  // Print the maximum cost
  document.write(canTake + best);
}

// Driver Code
var n = 5, m = 5;
// Cost Array
var cost = [2, 2, 8, 6, 9];
var g = Array.from(Array(n), ()=>Array());

// Given Graph
g[0].push(1);
g[1].push(0);
g[0].push(2);
g[2].push(0);
g[0].push(3);
g[3].push(0);
g[1].push(2);
g[2].push(1);
g[1].push(4);
g[4].push(1);
// Given Source Node
var source = 1;
// Function call
FindMaxCost(g, cost, source);

</script>
```

**Output:** 

```
21
```

**时间复杂度:** *O(N + M)* 其中 N 为顶点数，M 为边数。
**辅助空间:** *O(N + M)* 其中 N 为若干顶点，M 为若干边。