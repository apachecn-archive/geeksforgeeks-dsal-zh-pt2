# 未加权双向图中最短路径和第二最短路径之差

> 原文:[https://www . geesforgeks . org/最短路径和第二最短路径之差未加权双向图/](https://www.geeksforgeeks.org/difference-between-the-shortest-and-second-shortest-path-in-an-unweighted-bidirectional-graph/)

给定一个包含 **N** 节点和 **M** 边的[未加权双向图](https://www.geeksforgeeks.org/shortest-path-unweighted-graph/)，这些边由一个[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr[]【2】**表示。任务是找出从节点 **1** 到 **N** 的最短路径和第二最短路径的长度差。如果第二条最短路径不存在，打印 **0** 。

> **注:**图是连通的，不包含多条边和自循环。 **(2 < =N < =20)**

**示例:**

> **输入:** N = 4，M = 4，arr[M][2]={{1，2}，{2，3}，{3，4}，{1，4}}
> **输出:** 2
> **说明:**最短路径为 1- > 4，第二最短路径为 1- > 2- > 3- > 4。因此，差别是 2。
> 
> **输入:** N = 6，M = 8，arr[M][2]={{1，2}，{1，3}，{2，6}，{2，3}，{2，4}，{3，4}，{3，5}，{4，6}}
> **输出:** 1

**方法:**思路是[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)找到所有可能的路径并存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)和[中对](https://www.geeksforgeeks.org/quick-sort/)向量[进行排序](https://www.geeksforgeeks.org/vector-in-cpp-stl/)找到最短路径和第二最短路径的区别。按照以下步骤解决问题:

*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/)**DFS(vector<vector<int>>T8】图，int s，int e，vector < int > vis，int count，vector<int>T13】DP)**并执行以下步骤:
    *   如果 **s** 等于 **e** ，则表示当前路径是可能的路径之一，[推](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)值**计数[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中的**并返回。
    *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，图【s】】**，并执行以下步骤:
        *   如果 **vis[i]** 不等于 **1，**则将 **vis[i]** 的值设置为 **1** ，调用函数 **dfs(graph，即 vis，count+1，dp)** 寻找其他可能的路径，并将 **vis[0]** 的值再次设置回 **0。**
*   [用 **N** 行数初始化二维向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/) **图形[][]** ，以存储从每个顶点连接的顶点。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M】**，并执行以下步骤:
    *   [将](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **图中 **b-1** 的值【】【】**推到第 **a-1 行。**
    *   [将](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **图中 **a-1** 的值【】【】**推到第 **b-1 行。**
*   [初始化一个大小为 **N** 的向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/) **vis[]** ，以跟踪访问的节点。
*   [初始化一个向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/) **dp[]** 来存储所有可能路径的长度。
*   调用函数 **dfs(graph，0，N-1，vis，0，dp)** 找到所有可能的路径，并将它们存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)**DP【】**中。
*   [按升序排列向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)**【DP】**。
*   如果[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **dp[]** 的大小大于 **1，**则返回值 **dp[1]-dp[0]** 否则返回 **0** 作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// DFS function to find all possible paths.
void dfs(vector<vector<int> >& graph, int s, int e,
         vector<int> v, int count, vector<int>& dp)
{
    if (s == e) {
        // Push the number of nodes required for
        // one of the possible paths
        dp.push_back(count);
        return;
    }
    for (auto i : graph[s]) {
        if (v[i] != 1) {

            // Mark the node as visited and
            // call the function to search for
            // possible paths and unmark the node.
            v[i] = 1;
            dfs(graph, i, e, v, count + 1, dp);
            v[i] = 0;
        }
    }
}

// Function to find the difference between the
// shortest and second shortest path
void findDifference(int n, int m, int arr[][2])
{
    // Construct the graph
    vector<vector<int> > graph(n, vector<int>());
    for (int i = 0; i < m; i++) {
        int a, b;
        a = arr[i][0];
        b = arr[i][1];
        graph[a - 1].push_back(b - 1);
        graph[b - 1].push_back(a - 1);
    }

    // Vector to mark the nodes as visited or not.
    vector<int> v(n, 0);

    // Vector to store the count of all possible paths.
    vector<int> dp;

    // Mark the starting node as visited.
    v[0] = 1;

    // Function to find all possible paths.
    dfs(graph, 0, n - 1, v, 0, dp);

    // Sort the vector
    sort(dp.begin(), dp.end());

    // Print the difference
    if (dp.size() != 1)
        cout << dp[1] - dp[0];
    else
        cout << 0;
}

// Driver Code
int main()
{
    int n, m;
    n = 6;
    m = 8;
    int arr[m][2]
        = { { 1, 2 }, { 1, 3 },
            { 2, 6 }, { 2, 3 },
            { 2, 4 }, { 3, 4 },
            { 3, 5 }, { 4, 6 } };

    findDifference(n, m, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    // DFS function to find all possible paths.
    static void dfs(Vector<Vector<Integer>> graph, int s,
                    int e, int[] v, int count, Vector<Integer> dp) {
      if (s == e)
      {

        // Push the number of nodes required for
        // one of the possible paths
        dp.add(count);
        return;
      }
      for(int i : graph.get(s)) {
        if (v[i] != 1)
        {

          // Mark the node as visited and
          // call the function to search for
          // possible paths and unmark the node.
          v[i] = 1;
          dfs(graph, i, e, v, count + 1, dp);
          v[i] = 0;
        }
      }
    }

    // Function to find the difference between the
    // shortest and second shortest path
    static void findDifference(int n, int m, int[][] arr)
    {

      // Construct the graph
      Vector<Vector<Integer>> graph = new Vector<Vector<Integer>>();
      for(int i = 0; i < n; i++)
      {
        graph.add(new Vector<Integer>());
      }

      for (int i = 0; i < m; i++) {
        int a, b;
        a = arr[i][0];
        b = arr[i][1];
        graph.get(a - 1).add(b - 1);
        graph.get(b - 1).add(a - 1);
      }

      // Vector to mark the nodes as visited or not.
      int[] v = new int[n];
      Arrays.fill(v, 0);

      // Vector to store the count of all possible paths.
      Vector<Integer> dp = new Vector<Integer>();

      // Mark the starting node as visited.
      v[0] = 1;

      // Function to find all possible paths.
      dfs(graph, 0, n - 1, v, 0, dp);

      // Sort the vector
      Collections.sort(dp);

      // Print the difference
      if (dp.size() != 1) System.out.print(dp.get(1) - dp.get(0));
      else System.out.print(0);
    }

    public static void main(String[] args) {
        int n, m;
        n = 6;
        m = 8;
        int[][] arr
            = { { 1, 2 }, { 1, 3 },
                { 2, 6 }, { 2, 3 },
                { 2, 4 }, { 3, 4 },
                { 3, 5 }, { 4, 6 } };

        findDifference(n, m, arr);
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# DFS function to find all possible paths.
def dfs(graph, s, e, v, count, dp):
  if (s == e):

    # Push the number of nodes required for
    # one of the possible paths
    dp.append(count)
    return
  for i in graph[s]:
    if (v[i] != 1):

      # Mark the node as visited and
      # call the function to search for
      # possible paths and unmark the node.
      v[i] = 1
      dfs(graph, i, e, v, count + 1, dp)
      v[i] = 0

# Function to find the difference between the
# shortest and second shortest path
def findDifference(n, m, arr):
  # Construct the graph
  graph = []
  for i in range(n):
      graph.append([])

  for i in range(m):
    a = arr[i][0]
    b = arr[i][1]
    graph[a - 1].append(b - 1)
    graph[b - 1].append(a - 1)

  # Vector to mark the nodes as visited or not.
  v = [0]*(n)

  # Vector to store the count of all possible paths.
  dp = []

  # Mark the starting node as visited.
  v[0] = 1

  # Function to find all possible paths.
  dfs(graph, 0, n - 1, v, 0, dp)

  # Sort the vector
  dp.sort()

  # Print the difference
  if (len(dp) != 1):
    print(dp[1] - dp[0], end = "")
  else:
    print(0, end = "")

# Driver Code
n = 6
m = 8
arr = [
  [1, 2],
  [1, 3],
  [2, 6],
  [2, 3],
  [2, 4],
  [3, 4],
  [3, 5],
  [4, 6],
]

findDifference(n, m, arr)

# This code is contributed by divyesh072019.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // DFS function to find all possible paths.
    static void dfs(List<List<int>> graph, int s, int e, List<int> v, int count, List<int> dp) {
      if (s == e)
      {

        // Push the number of nodes required for
        // one of the possible paths
        dp.Add(count);
        return;
      }
      foreach(int i in graph[s]) {
        if (v[i] != 1)
        {

          // Mark the node as visited and
          // call the function to search for
          // possible paths and unmark the node.
          v[i] = 1;
          dfs(graph, i, e, v, count + 1, dp);
          v[i] = 0;
        }
      }
    }

    // Function to find the difference between the
    // shortest and second shortest path
    static void findDifference(int n, int m, int[,] arr)
    {

      // Construct the graph
      List<List<int>> graph = new List<List<int>>();
      for(int i = 0; i < n; i++)
      {
          graph.Add(new List<int>());
      }

      for (int i = 0; i < m; i++) {
        int a, b;
        a = arr[i,0];
        b = arr[i,1];
        graph[a - 1].Add(b - 1);
        graph[b - 1].Add(a - 1);
      }

      // Vector to mark the nodes as visited or not.
      List<int> v = new List<int>();
      for(int i = 0; i < n; i++)
      {
          v.Add(0);
      }

      // Vector to store the count of all possible paths.
      List<int> dp = new List<int>();

      // Mark the starting node as visited.
      v[0] = 1;

      // Function to find all possible paths.
      dfs(graph, 0, n - 1, v, 0, dp);

      // Sort the vector
      dp.Sort();

      // Print the difference
      if (dp.Count != 1) Console.Write(dp[1] - dp[0]);
      else Console.Write(0);
    }

  static void Main() {
    int n, m;
    n = 6;
    m = 8;
    int[,] arr
        = { { 1, 2 }, { 1, 3 },
            { 2, 6 }, { 2, 3 },
            { 2, 4 }, { 3, 4 },
            { 3, 5 }, { 4, 6 } };

    findDifference(n, m, arr);
  }
}

// Ths code is contributed by decode2207.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// DFS function to find all possible paths.
function dfs(graph, s, e, v, count, dp) {
  if (s == e)
  {

    // Push the number of nodes required for
    // one of the possible paths
    dp.push(count);
    return;
  }
  for (let i of graph[s]) {
    if (v[i] != 1)
    {

      // Mark the node as visited and
      // call the function to search for
      // possible paths and unmark the node.
      v[i] = 1;
      dfs(graph, i, e, v, count + 1, dp);
      v[i] = 0;
    }
  }
}

// Function to find the difference between the
// shortest and second shortest path
function findDifference(n, m, arr)
{

  // Construct the graph
  let graph = new Array(n).fill(0).map(() => []);

  for (let i = 0; i < m; i++) {
    let a, b;
    a = arr[i][0];
    b = arr[i][1];
    graph[a - 1].push(b - 1);
    graph[b - 1].push(a - 1);
  }

  // Vector to mark the nodes as visited or not.
  let v = new Array(n).fill(0);

  // Vector to store the count of all possible paths.
  let dp = [];

  // Mark the starting node as visited.
  v[0] = 1;

  // Function to find all possible paths.
  dfs(graph, 0, n - 1, v, 0, dp);

  // Sort the vector
  dp.sort((a, b) => a - b);

  // Print the difference
  if (dp.length != 1) document.write(dp[1] - dp[0]);
  else document.write(0);
}

// Driver Code
let n, m;
n = 6;
m = 8;
let arr = [
  [1, 2],
  [1, 3],
  [2, 6],
  [2, 3],
  [2, 4],
  [3, 4],
  [3, 5],
  [4, 6],
];

findDifference(n, m, arr);

// This code is contributed by gfgking.
</script>
```

**Output**

```
1
```

***时间复杂度:** O(2^N)*
***辅助空间:** O(N)*

**高效方法:**利用第二最短路径不能包含与最短路径相同的所有边的事实。每次移除最短路径的每条边，并不断寻找最短路径，那么其中一条必须是所需的第二条最短路径。使用[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)找到最优解。按照以下步骤解决问题:

*   定义函数 **get_edges(int s，vector < int > & edges，vector < int > p)** ，并执行以下步骤:
    *   如果 **s** 等于 **-1，**则返回。
    *   调用函数 **get_edges(p[s]，edges，p)** 求最短路径上的所有边。
    *   [将 **s** 的值推送到](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **边[]。**
*   定义一个函数**dist _ helper(vector<vector<int>T5】graph，vector<int>T8】d，int v1，int v2，int N)** 并执行以下步骤:
    *   [初始化向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/)**【vis】**以跟踪访问的节点。
    *   [初始化一对队列](https://www.geeksforgeeks.org/queue-of-pairs-in-c-stl-with-examples/) **q[]** 进行[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)找到路径。
    *   [将](https://www.geeksforgeeks.org/queue-set-1introduction-and-array-implementation/)[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)和 **{0，0}** 排入对和**的[队列。](https://www.geeksforgeeks.org/queue-of-pairs-in-c-stl-with-examples/)**
    *   将**vis【0】**的值标记为 **1(已访问)**。
    *   [循环迭代](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到成对 **q[]** 的[队列不为空。](https://www.geeksforgeeks.org/queue-of-pairs-in-c-stl-with-examples/)
        *   将变量 **a** 初始化为对**q【】**的[队列的](https://www.geeksforgeeks.org/queue-of-pairs-in-c-stl-with-examples/)[前端](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)，并将元素从对[队列](https://www.geeksforgeeks.org/queue-of-pairs-in-c-stl-with-examples/) **q【】中出列。**
        *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，图形【a . first】】**，并执行以下步骤:
            *   如果 **i** 等于 **v1** 和 **a.first** 等于 **v2** 或 **i** 等于 **v2** 和 **a.first** 等于 **v1、**，则[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)。
            *   如果 **vis[i]** 等于 **0，**则将 **d[i]** 的值设置为 **1+a .秒，p[i]** 设置为 **a .秒，将 **vis[i]** 设置为 **1** 和[将](https://www.geeksforgeeks.org/queue-set-1introduction-and-array-implementation/)[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/) **{i，d[i]}** 入队**
*   定义函数 **dist(向量<向量<int>T5】graph，向量<int>T8】d，向量<int>T11】p，int N)** 并执行以下步骤:
    *   [初始化向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/)**【vis】**以跟踪访问的节点。
    *   [初始化一对队列](https://www.geeksforgeeks.org/queue-of-pairs-in-c-stl-with-examples/) **q[]** 进行[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)找到路径。
    *   [将](https://www.geeksforgeeks.org/queue-set-1introduction-and-array-implementation/)[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)和 **{0，0}** 排入对和**的[队列。](https://www.geeksforgeeks.org/queue-of-pairs-in-c-stl-with-examples/)**
    *   将**vis【0】**的值标记为 **1(已访问)**。
    *   [循环迭代](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到成对 **q[]** 的[队列不为空。](https://www.geeksforgeeks.org/queue-of-pairs-in-c-stl-with-examples/)
        *   将变量 **a** 初始化为对**q【】**的[队列的](https://www.geeksforgeeks.org/queue-of-pairs-in-c-stl-with-examples/)[前端](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)，并将元素[从对](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)[队列](https://www.geeksforgeeks.org/queue-of-pairs-in-c-stl-with-examples/) **q【】中出队。**
        *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，图形【a . first】】**，并执行以下步骤:
            *   如果 **vis[i]** 等于 **0，**则将 **d[i]** 的值设置为**1+1 秒**并将 **vis[i]** 设置为 **1** 和[将](https://www.geeksforgeeks.org/queue-set-1introduction-and-array-implementation/)[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/) **{i，d[i]}** 排入对 **q[]的[队列。](https://www.geeksforgeeks.org/queue-of-pairs-in-c-stl-with-examples/)**
*   [用 **N** 行数初始化二维向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/) **图形[][]** ，以存储从每个顶点连接的顶点。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M】**，并执行以下步骤:
    *   [将](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **图中 **b-1** 的值【】【】**推到第 **a-1 行。**
    *   [将](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **图中 **a-1** 的值【】【】**推到第 **b-1 行。**
*   [初始化大小为 **N** 的向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/) **p[]** 和 **d[]** ，以跟踪父节点和路径长度。
*   调用函数 **dist(图，d，p，N)** 求最短路径的长度。
*   [初始化一个向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/) **距离[]** 来存储所有可能路径的长度。
*   [将**d【N-1】**的值推至](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **距离[]。**
*   [初始化一个向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/) **边[]** 得到沿最短路径的所有边。
*   调用函数 **get_edges(N-1，edges，p)** 找到沿最短路径的所有边。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，edges()-1】**，并执行以下步骤:
    *   调用函数 **dist_helper(图，d，边[i]，边[i+1]，N)** 求最短路径上的所有边。
    *   [将**d【N-1】**的值推至](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **距离[]。**
*   [按升序排列向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/) **距离[]** 。
*   如果[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **距离[]** 的大小大于 **1、**，则返回值**距离[1]-距离[0]** ，否则返回 **0** 作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to get all the edges in
// the shortest path
void get_edges(int s, vector<int>& edges, vector<int> p)
{
    if (s == -1)
        return;
    get_edges(p[s], edges, p);
    edges.push_back(s);
}

// Calculate the shortest distance
// after removing an edge between
// v1 and v2
void dist_helper(vector<vector<int> > graph, vector<int>& d,
                 int v1, int v2, int n)
{
    // Vector to mark the nodes visited
    vector<int> v(n, 0);

    // For BFS
    queue<pair<int, int> > q;
    q.push(make_pair(0, 0));
    v[0] = 1;

    // Iterate over the range
    while (!q.empty()) {
        auto a = q.front();
        q.pop();
        for (int i : graph[a.first]) {
            if ((i == v1 && a.first == v2)
                || (i == v2 && a.first == v1))
                continue;
            if (v[i] == 0) {
                d[i] = 1 + a.second;
                v[i] = 1;
                q.push(make_pair(i, d[i]));
            }
        }
    }
}

// Calculates the shortest distances and
// maintain a parent array
void dist(vector<vector<int> > graph, vector<int>& d,
          vector<int>& p, int n)
{
    // Vector to mark the nodes visited
    vector<int> v(n, 0);

    // For BFS
    queue<pair<int, int> > q;
    q.push(make_pair(0, 0));
    v[0] = 1;

    // Iterate over the range
    while (!q.empty()) {
        auto a = q.front();
        q.pop();
        for (int i : graph[a.first]) {
            if (v[i] == 0) {
                p[i] = a.first;
                d[i] = 1 + a.second;
                v[i] = 1;
                q.push(make_pair(i, d[i]));
            }
        }
    }
}

// Function to find the difference between the
// shortest and second shortest path
void findDifference(int n, int m, int arr[][2])
{

    // Initializing and constructing the graph
    vector<vector<int> > graph(n, vector<int>());
    for (int i = 0; i < m; i++) {
        int a, b;
        a = arr[i][0];
        b = arr[i][1];
        graph[a - 1].push_back(b - 1);
        graph[b - 1].push_back(a - 1);
    }

    // Initializing the arrays
    vector<int> p(n, -1);
    vector<int> d(n, 1e9);

    // Calculate the shortest path
    dist(graph, d, p, n);

    // Vector to store the lengths
    // of possible paths
    vector<int> distances;
    distances.push_back(d[n - 1]);

    vector<int> edges;

    // Get all the edges along the shortest path
    get_edges(n - 1, edges, p);

    // Iterate over the range
    for (int i = 0; i + 1 < edges.size(); i++) {
        // Calculate shortest distance after
        // removing the edge
        dist_helper(graph, d, edges[i], edges[i + 1], n);
        distances.push_back(d[n - 1]);
    }

    // Sort the paths in ascending order
    sort(distances.begin(), distances.end());
    if (distances.size() == 1)
        cout << 0 << endl;
    else
        cout << distances[1] - distances[0] << endl;
}

// Driver Code
int main()
{
    int n, m;
    n = 6;
    m = 8;
    int arr[m][2]
        = { { 1, 2 }, { 1, 3 },
            { 2, 6 }, { 2, 3 },
            { 2, 4 }, { 3, 4 },
            { 3, 5 }, { 4, 6 } };

    findDifference(n, m, arr);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

edges, d, p = [], [], []

# Function to get all the edges in
# the shortest path
def get_edges(s):
    global edges, d, p
    if s == -1:
        return
    get_edges(p[s])
    edges.append(s)

# Calculate the shortest distance
# after removing an edge between
# v1 and v2
def dist_helper(graph, v1, v2, n):
    global edges, d, p
    # Vector to mark the nodes visited
    v = [0]*(n)

    # For BFS
    q = []
    q.append([0, 0])
    v[0] = 1

    # Iterate over the range
    while len(q) > 0:
        a = q[0]
        q.pop(0)
        for i in graph[a[0]]:
            if (i == v1 and a[0] == v2) or (i == v2 and a[0] == v1):
                continue
            if v[i] == 0:
                d[i] = 1 + a[1]
                v[i] = 1
                q.append([i, d[i]])

# Calculates the shortest distances and
# maintain a parent array
def dist(graph, n):
    global edges, d, p
    # Vector to mark the nodes visited
    v = [0]*(n)

    # For BFS
    q = []
    q.append([0, 0])
    v[0] = 1

    # Iterate over the range
    while len(q) > 0:
        a = q[0]
        q.pop(0)
        for i in graph[a[0]]:
            if v[i] == 0:
                p[i] = a[0]
                d[i] = 1 + a[1]
                v[i] = 1
                q.append([i, d[i]])

# Function to find the difference between the
# shortest and second shortest path
def findDifference(n, m, arr):
    global edges, d, p
    # Initializing and constructing the graph
    graph = []
    for i in range(n):
        graph.append([])
    for i in range(m):
        a = arr[i][0]
        b = arr[i][1]
        graph[a - 1].append(b - 1)
        graph[b - 1].append(a - 1)

    # Initializing the arrays
    p = [-1]*(n)
    d = [1e9]*(n)

    # Calculate the shortest path
    dist(graph, n)

    # Vector to store the lengths
    # of possible paths
    distances = []
    distances.append(d[n - 1])

    edges = []

    # Get all the edges along the shortest path
    get_edges(n - 1)

    # Iterate over the range
    i = 0
    while i + 1 < len(edges):

        # Calculate shortest distance after
        # removing the edge
        dist_helper(graph, edges[i], edges[i + 1], n)
        distances.append(d[n - 1])
        i+=1

    # Sort the paths in ascending order
    distances.sort()
    if len(distances) == 1:
        print(0)
    else:
        print(distances[1] - distances[0])

n = 6;
m = 8;
arr = [ [ 1, 2 ], [ 1, 3 ], [ 2, 6 ], [ 2, 3 ], [ 2, 4 ], [ 3, 4 ], [ 3, 5 ], [ 4, 6 ] ]

findDifference(n, m, arr)

# This code is contributed by suresh07.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

   static List<int> edges = new List<int>();
   static List<int> d = new List<int>();
   static List<int> p = new List<int>();

    // Function to get all the edges in
    // the shortest path
    static void get_edges(int s)
    {
        if (s == -1)
            return;
        get_edges(p[s]);
        edges.Add(s);
    }

    // Calculate the shortest distance
    // after removing an edge between
    // v1 and v2
    static void dist_helper(List<List<int>> graph, int v1, int v2, int n)
    {
        // Vector to mark the nodes visited
        List<int> v = new List<int>();
        for(int i = 0; i < n; i++)
        {
            v.Add(0);
        }

        // For BFS
        List<Tuple<int,int>> q = new List<Tuple<int,int>>();
        q.Add(new Tuple<int,int>(0, 0));
        v[0] = 1;

        // Iterate over the range
        while (q.Count > 0) {
            Tuple<int,int> a = q[0];
            q.RemoveAt(0);
            for (int i = 0; i < graph[a.Item1].Count; i++) {
                if ((graph[a.Item1][i] == v1 && a.Item1 == v2)
                    || (graph[a.Item1][i] == v2 && a.Item1 == v1))
                    continue;
                if (v[graph[a.Item1][i]] == 0) {
                    d[graph[a.Item1][i]] = 1 + a.Item2;
                    v[graph[a.Item1][i]] = 1;
                    q.Add(new Tuple<int,int>(graph[a.Item1][i], d[graph[a.Item1][i]]));
                }
            }
        }
    }

    // Calculates the shortest distances and
    // maintain a parent array
    static void dist(List<List<int>> graph, int n)
    {
        // Vector to mark the nodes visited
        List<int> v = new List<int>();
        for(int i = 0; i < n; i++)
        {
            v.Add(0);
        }

        // For BFS
        List<Tuple<int,int>> q = new List<Tuple<int,int>>();
        q.Add(new Tuple<int,int>(0, 0));
        v[0] = 1;

        // Iterate over the range
        while (q.Count > 0) {
            Tuple<int,int> a = q[0];
            q.RemoveAt(0);
            for (int i = 0; i < graph[a.Item1].Count; i++) {
                if (v[graph[a.Item1][i]] == 0) {
                    p[graph[a.Item1][i]] = a.Item1;
                    d[graph[a.Item1][i]] = 1 + a.Item2;
                    v[graph[a.Item1][i]] = 1;
                    q.Add(new Tuple<int,int>(graph[a.Item1][i], d[graph[a.Item1][i]]));
                }
            }
        }
    }

    // Function to find the difference between the
    // shortest and second shortest path
    static void findDifference(int n, int m, int[,] arr)
    {

        // Initializing and constructing the graph
        List<List<int>> graph = new List<List<int>>();
        for(int i = 0; i < n; i++)
        {
            graph.Add(new List<int>());
        }
        for (int i = 0; i < m; i++) {
            int a, b;
            a = arr[i,0];
            b = arr[i,1];
            graph[a - 1].Add(b - 1);
            graph[b - 1].Add(a - 1);
        }

        // Initializing the arrays
        for(int i = 0; i < n; i++)
        {
            p.Add(-1);
            d.Add(1000000000);
        }

        // Calculate the shortest path
        dist(graph, n);

        // Vector to store the lengths
        // of possible paths
        List<int> distances = new List<int>();
        distances.Add(d[n - 1]);

        // Get all the edges along the shortest path
        get_edges(n - 1);

        // Iterate over the range
        for (int i = 0; i + 1 < edges.Count; i++) {
            // Calculate shortest distance after
            // removing the edge
            dist_helper(graph, edges[i], edges[i + 1], n);
            distances.Add(d[n - 1]);
        }

        // Sort the paths in ascending order
        distances.Sort();
        if (distances.Count == 1)
        {
            Console.WriteLine(0);
        }
        else
        {
            Console.WriteLine((distances[1] - distances[0]));
        }
    }

  // Driver code
  static void Main() {
    int n, m;
    n = 6;
    m = 8;
    int[,] arr
        = { { 1, 2 }, { 1, 3 },
            { 2, 6 }, { 2, 3 },
            { 2, 4 }, { 3, 4 },
            { 3, 5 }, { 4, 6 } };

    findDifference(n, m, arr);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    let edges = [], d = [], p = [];   

    // Function to get all the edges in
    // the shortest path
    function get_edges(s)
    {
        if (s == -1)
            return;
        get_edges(p[s]);
        edges.push(s);
    }

    // Calculate the shortest distance
    // after removing an edge between
    // v1 and v2
    function dist_helper(graph, v1, v2, n)
    {
        // Vector to mark the nodes visited
        let v = [];
        for(let i = 0; i < n; i++)
        {
            v.push(0);
        }

        // For BFS
        let q = [];
        q.push([0, 0]);
        v[0] = 1;

        // Iterate over the range
        while (q.length > 0) {
            let a = q[0];
            q.shift();
            for (let i = 0; i < graph[a[0]].length; i++) {
                if ((graph[a[0]][i] == v1 && a[0] == v2)
                    || (graph[a[0]][i] == v2 && a[0] == v1))
                    continue;
                if (v[graph[a[0]][i]] == 0) {
                    d[graph[a[0]][i]] = 1 + a[1];
                    v[graph[a[0]][i]] = 1;
                    q.push([graph[a[0]][i], d[graph[a[0]][i]]]);
                }
            }
        }
    }

    // Calculates the shortest distances and
    // maintain a parent array
    function dist(graph, n)
    {
        // Vector to mark the nodes visited
        let v = [];
        for(let i = 0; i < n; i++)
        {
            v.push(0);
        }

        // For BFS
        let q = [];
        q.push([0, 0]);
        v[0] = 1;

        // Iterate over the range
        while (q.length > 0) {
            let a = q[0];
            q.shift();
            for (let i = 0; i < graph[a[0]].length; i++) {
                if (v[graph[a[0]][i]] == 0) {
                    p[graph[a[0]][i]] = a[0];
                    d[graph[a[0]][i]] = 1 + a[1];
                    v[graph[a[0]][i]] = 1;
                    q.push([graph[a[0]][i], d[graph[a[0]][i]]]);
                }
            }
        }
    }

    // Function to find the difference between the
    // shortest and second shortest path
    function findDifference(n, m, arr)
    {

        // Initializing and constructing the graph
        let graph = [];
        for(let i = 0; i < n; i++)
        {
            graph.push([]);
        }
        for (let i = 0; i < m; i++) {
            let a, b;
            a = arr[i][0];
            b = arr[i][1];
            graph[a - 1].push(b - 1);
            graph[b - 1].push(a - 1);
        }

        // Initializing the arrays
        for(let i = 0; i < n; i++)
        {
            p.push(-1);
            d.push(1e9);
        }

        // Calculate the shortest path
        dist(graph, n);

        // Vector to store the lengths
        // of possible paths
        let distances = [];
        distances.push(d[n - 1]);

        // Get all the edges along the shortest path
        get_edges(n - 1);

        // Iterate over the range
        for (let i = 0; i + 1 < edges.length; i++) {
            // Calculate shortest distance after
            // removing the edge
            dist_helper(graph, edges[i], edges[i + 1], n);
            distances.push(d[n - 1]);
        }

        // Sort the paths in ascending order
        distances.sort(function(a, b){return a - b});
        if (distances.length == 1)
        {
            document.write(0 + "</br>");
        }
        else
        {
            document.write((distances[1] - distances[0]) + "</br>");
        }
    }

    let n, m;
    n = 6;
    m = 8;
    let arr
        = [ [ 1, 2 ], [ 1, 3 ],
            [ 2, 6 ], [ 2, 3 ],
            [ 2, 4 ], [ 3, 4 ],
            [ 3, 5 ], [ 4, 6 ] ];

    findDifference(n, m, arr);

// This code is contributed by rameshtravel07.
</script>
```

**Output**

```
1
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N)*