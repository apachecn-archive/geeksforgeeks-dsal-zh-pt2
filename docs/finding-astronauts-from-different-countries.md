# 寻找来自不同国家的宇航员

> 原文:[https://www . geesforgeks . org/finding-来自不同国家的宇航员/](https://www.geeksforgeeks.org/finding-astronauts-from-different-countries/)

给定一个表示宇航员数量的正整数 **N** (标记为从 **0** 到**(N–1)**)和一个包含来自同一国家的宇航员对的矩阵 **mat[][]** ，任务是计算从不同国家选择两名宇航员的方法数量。

**示例:**

> **输入:** N = 6，mat[][] = {{0，1}，{0，2}，{2，5}}
> **输出:** 9
> **说明:**
> ID 为{0，1，2，5}的宇航员属于第一国家，ID 为{3}的宇航员属于第二国家，ID 为{4}的宇航员属于第三国家。从不同国家选择两名宇航员的方法有:
> 
> 1.  从 1 国选择 1 名宇航员，从 2 国选择 1 名宇航员，那么途径总数为 4*1 = 4。
> 2.  从 1 国选择 1 名宇航员，从 3 国选择 1 名宇航员，那么途径总数为 4*1 = 4。
> 3.  从 2 国选择 1 名宇航员，从 3 国选择 1 名宇航员，那么途径总数为 1*1 = 1。
> 
> 因此，路的总数是 4 + 4 + 1 = 9。
> 
> **输入:** N = 5，mat[][] = {{0，1}，{2，3}，{0，4 } }
> T3】输出: 6

**方法:**给定的问题可以通过将该问题建模为[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)来解决，其中宇航员代表[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)的顶点，给定的对代表图中的边。构建图后，想法是计算从不同国家选择 2 名宇航员的方法数量。按照以下步骤解决问题:

*   创建列表[列表](https://www.geeksforgeeks.org/data-structures/linked-list/)，**调整[][]** 以存储图形的[邻接表。](https://www.geeksforgeeks.org/graph-and-its-representations/)
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**，并将 **arr[i][1]** 追加到**adj【arr[I][0]】**，还将 **arr[i][0]** 追加到**adj【arr[I][1]】**用于无向边。
*   现在，通过执行[深度优先搜索](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)，使用本文[中讨论的方法，找到图形](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)的每个[连接组件的大小，并将要存储的所有连接组件的大小存储在一个](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中，比如**v[**]。
*   初始化一个整数变量，比如**和**作为从 **N** 宇航员中选择 2 名宇航员的方式总数，即**N *(N–1)/2**。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **v[]** 并从变量**和**中减去**v[I]*(v[I]–1)/2**，以排除每个连接组件中所有可能的对。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to perform the DFS Traversal
// to find the count of connected
// components
void dfs(int v, vector<vector<int> >& adj,
         vector<bool>& visited, int& num)
{
    // Marking vertex visited
    visited[v] = true;
    num++;

    // DFS call to neighbour vertices
    for (int i = 0; i < adj[v].size(); i++) {

        // If the current node is not
        // visited, then recursively
        // call DFS
        if (!visited[adj[v][i]]) {
            dfs(adj[v][i], adj,
                visited, num);
        }
    }
}

// Function to find the number of ways
// to choose two astronauts from the
// different countries
void numberOfPairs(
    int N, vector<vector<int> > arr)
{
    // Stores the Adjacency list
    vector<vector<int> > adj(N);

    // Constructing the graph
    for (vector<int>& i : arr) {
        adj[i[0]].push_back(i[1]);
        adj[i[1]].push_back(i[0]);
    }

    // Stores the visited vertices
    vector<bool> visited(N);

    // Stores the size of every
    // connected components
    vector<int> v;

    int num = 0;
    for (int i = 0; i < N; i++) {

        if (!visited[i]) {

            // DFS call to the graph
            dfs(i, adj, visited, num);

            // Store size of every
            // connected component
            v.push_back(num);
            num = 0;
        }
    }

    // Stores the total number of
    // ways to count the pairs
    int ans = N * (N - 1) / 2;

    // Traverse the array
    for (int i : v) {
        ans -= (i * (i - 1) / 2);
    }

    // Print the value of ans
    cout << ans;
}

// Driver Code
int main()
{
    int N = 6;
    vector<vector<int> > arr = { { 0, 1 }, { 0, 2 }, { 2, 5 } };
    numberOfPairs(N, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{
    // Function to perform the DFS Traversal
    // to find the count of connected
    // components
    static Vector<Vector<Integer>> adj;
    static boolean[] visited;
    static int num;

    // Function to perform the DFS Traversal
    // to find the count of connected
    // components
    static void dfs(int v)
    {

        // Marking vertex visited
        visited[v] = true;
        num++;

        // DFS call to neighbour vertices
        for (int i = 0; i < adj.get(v).size(); i++) {

            // If the current node is not
            // visited, then recursively
            // call DFS
            if (!visited[adj.get(v).get(i)]) {
                dfs(adj.get(v).get(i));
            }
        }
    }

    // Function to find the number of ways
    // to choose two astronauts from the
    // different countries
    static void numberOfPairs(int N, int[][] arr)
    {
        // Stores the Adjacency list
        adj = new Vector<Vector<Integer>>();
        for(int i = 0; i < N; i++)
        {
            adj.add(new Vector<Integer>());
        }

        // Constructing the graph
        for (int i = 0; i < 2; i++) {
            adj.get(arr[i][0]).add(arr[i][1]);
            adj.get(arr[i][1]).add(arr[i][0]);
        }

        // Stores the visited vertices
        visited = new boolean[N];
        Arrays.fill(visited, false);

        // Stores the size of every
        // connected components
        Vector<Integer> v = new Vector<Integer>();

        num = 0;
        for (int i = 0; i < N; i++) {

            if (!visited[i]) {

                // DFS call to the graph
                dfs(i);

                // Store size of every
                // connected component
                v.add(num);
                num = 0;
            }
        }

        // Stores the total number of
        // ways to count the pairs
        int ans = N * (N - 1) / 2 + 1;

        // Traverse the array
        for (int i = 0; i < v.size(); i++) {
            ans -= (v.get(i) * (v.get(i) - 1) / 2) +1;
        }

        // Print the value of ans
        System.out.print(ans);
    }

    public static void main(String[] args) {
        int N = 6;
        int[][] arr = { { 0, 1 }, { 0, 2 }, { 2, 5 } };
        numberOfPairs(N, arr);
    }
}

// This code is contributed by suresh07
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to perform the DFS Traversal
# to find the count of connected
# components
adj = []
visited = []
num = 0

def dfs(v):
    global adj, visited, num

    # Marking vertex visited
    visited[v] = True
    num+=1

    # DFS call to neighbour vertices
    for i in range(len(adj[v])):

        # If the current node is not
        # visited, then recursively
        # call DFS
        if (not visited[adj[v][i]]):
            dfs(adj[v][i])

# Function to find the number of ways
# to choose two astronauts from the
# different countries
def numberOfPairs(N, arr):
    global adj, visited, num
    # Stores the Adjacency list
    adj = []
    for i in range(N):
        adj.append([])

    # Constructing the graph
    for i in range(len(arr)):
        adj[arr[i][0]].append(arr[i][1])
        adj[arr[i][1]].append(arr[i][0])

    # Stores the visited vertices
    visited = [False]*(N)

    # Stores the size of every
    # connected components
    v = []

    num = 0
    for i in range(N):
        if (not visited[i]):
            # DFS call to the graph
            dfs(i)

            # Store size of every
            # connected component
            v.append(num)
            num = 0

    # Stores the total number of
    # ways to count the pairs
    ans = N * int((N - 1) / 2)

    # Traverse the array
    for i in range(len(v)):
        ans -= (v[i] * int((v[i] - 1) / 2))
    ans+=1

    # Print the value of ans
    print(ans)

N = 6
arr = [ [ 0, 1 ], [ 0, 2 ], [ 2, 5 ] ]
numberOfPairs(N, arr)

# This code is contributed by mukesh07.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to perform the DFS Traversal
    // to find the count of connected
    // components
    static List<List<int>> adj;
    static bool[] visited;
    static int num;

    // Function to perform the DFS Traversal
    // to find the count of connected
    // components
    static void dfs(int v)
    {
        // Marking vertex visited
        visited[v] = true;
        num++;

        // DFS call to neighbour vertices
        for (int i = 0; i < adj[v].Count; i++) {

            // If the current node is not
            // visited, then recursively
            // call DFS
            if (!visited[adj[v][i]]) {
                dfs(adj[v][i]);
            }
        }
    }

    // Function to find the number of ways
    // to choose two astronauts from the
    // different countries
    static void numberOfPairs(int N, int[,] arr)
    {
        // Stores the Adjacency list
        adj = new List<List<int>>();
        for(int i = 0; i < N; i++)
        {
            adj.Add(new List<int>());
        }

        // Constructing the graph
        for (int i = 0; i < 2; i++) {
            adj[arr[i,0]].Add(arr[i,1]);
            adj[arr[i,1]].Add(arr[i,0]);
        }

        // Stores the visited vertices
        visited = new bool[N];
        Array.Fill(visited, false);

        // Stores the size of every
        // connected components
        List<int> v = new List<int>();

        num = 0;
        for (int i = 0; i < N; i++) {

            if (!visited[i]) {

                // DFS call to the graph
                dfs(i);

                // Store size of every
                // connected component
                v.Add(num);
                num = 0;
            }
        }

        // Stores the total number of
        // ways to count the pairs
        int ans = N * (N - 1) / 2 + 1;

        // Traverse the array
        for (int i = 0; i < v.Count; i++) {
            ans -= (v[i] * (v[i] - 1) / 2) +1;
        }

        // Print the value of ans
        Console.Write(ans);
    }

  static void Main() {
    int N = 6;
    int[,] arr = { { 0, 1 }, { 0, 2 }, { 2, 5 } };
    numberOfPairs(N, arr);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach 

    // Function to perform the DFS Traversal
    // to find the count of connected
    // components

    let adj;
    let visited;
    let num;

    function dfs(v)
    {
        // Marking vertex visited
        visited[v] = true;
        num++;

        // DFS call to neighbour vertices
        for (let i = 0; i < adj[v].length; i++) {

            // If the current node is not
            // visited, then recursively
            // call DFS
            if (!visited[adj[v][i]]) {
                dfs(adj[v][i]);
            }
        }
    }

    // Function to find the number of ways
    // to choose two astronauts from the
    // different countries
    function numberOfPairs(N, arr)
    {
        // Stores the Adjacency list
        adj = [];
        for(let i = 0; i < N; i++)
        {
            adj.push([]);
        }

        // Constructing the graph
        for (let i = 0; i < arr.length; i++) {
            adj[arr[i][0]].push(arr[i][1]);
            adj[arr[i][1]].push(arr[i][0]);
        }

        // Stores the visited vertices
        visited = new Array(N);
        visited.fill(false);

        // Stores the size of every
        // connected components
        let v = [];

        num = 0;
        for (let i = 0; i < N; i++) {

            if (!visited[i]) {

                // DFS call to the graph
                dfs(i);

                // Store size of every
                // connected component
                v.push(num);
                num = 0;
            }
        }

        // Stores the total number of
        // ways to count the pairs
        let ans = N * (N - 1) / 2;

        // Traverse the array
        for (let i = 0; i < v.length; i++) {
            ans -= (v[i] * (v[i] - 1) / 2);
        }

        // Print the value of ans
        document.write(ans);
    }

    let N = 6;
    let arr = [ [ 0, 1 ], [ 0, 2 ], [ 2, 5 ] ];
    numberOfPairs(N, arr);

// This code is contributed by rameshtravel07.
</script>
```

**Output:** 

```
9
```

***时间复杂度:** O(N + E)，其中 N 为顶点数，E 为边数。*
***辅助空间:** O(N + E)*