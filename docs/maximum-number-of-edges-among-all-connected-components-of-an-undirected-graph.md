# 无向图所有连通分支中的最大边数

> 原文:[https://www . geesforgeks . org/无向图所有连通分量中的最大边数/](https://www.geeksforgeeks.org/maximum-number-of-edges-among-all-connected-components-of-an-undirected-graph/)

给定整数“N”和“K”，其中，N 是无向图的顶点数，“K”表示同一图中的边数(每条边由一对整数表示，其中 I，j 表示顶点“I”直接连接到图中的顶点“j”)。
任务是找到给定图中所有连通分量中的最大边数。
**例:**

> **输入:** N = 6，K = 4，
> 边= {{1，2}、{2，3}、{3，1}、{4，5 } }
> T4】输出: 3
> 这里，图形有 3 个分量
> 第一分量 1-2-3-1 : 3 条边
> 第二分量 4-5 : 1 条边
> 第三分量 6 : 0 条边
> 最大(3，1，0) = 3 条边
> **输入**

**进场:**

*   使用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)，分别找出所有连接组件中每条边的度数之和。
*   现在，根据[握手引理](https://www.geeksforgeeks.org/handshaking-lemma-and-interesting-tree-properties/)，无向图的连通分支中边的总数等于其所有顶点度数总和的一半。
*   打印所有连接组件的最大边数。

以下是上述方法的实现:

## C++

```
// C++ program to find the connected component
// with maximum number of edges
#include <bits/stdc++.h>
using namespace std;

// DFS function
int dfs(int s, vector<int> adj[], vector<bool> visited,
                                             int nodes)
{
    // Adding all the edges connected to the vertex
    int adjListSize = adj[s].size();
    visited[s] = true;
    for (long int i = 0; i < adj[s].size(); i++) {
        if (visited[adj[s][i]] == false) {
            adjListSize += dfs(adj[s][i], adj, visited, nodes);
        }
    }
    return adjListSize;
}

int maxEdges(vector<int> adj[], int nodes)
{
    int res = INT_MIN;
    vector<bool> visited(nodes, false);
    for (long int i = 1; i <= nodes; i++) {
        if (visited[i] == false) {
            int adjListSize = dfs(i, adj, visited, nodes);
            res = max(res, adjListSize/2);
        }     
    }
    return res;
}

// Driver code
int main()
{
    int nodes = 3;
    vector<int> adj[nodes+1];

    // Edge from vertex 1 to vertex 2
    adj[1].push_back(2);
    adj[2].push_back(1);

    // Edge from vertex 2 to vertex 3
    adj[2].push_back(3);
    adj[3].push_back(2);

    cout << maxEdges(adj, nodes);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the connected component
// with maximum number of edges
import java.util.*;

class GFG
{

// DFS function
static int dfs(int s, Vector<Vector<Integer>> adj,boolean visited[],
                        int nodes)
{
    // Adding all the edges connected to the vertex
    int adjListSize = adj.get(s).size();
    visited[s] = true;
    for (int i = 0; i < adj.get(s).size(); i++)
    {
        if (visited[adj.get(s).get(i)] == false)
        {
            adjListSize += dfs(adj.get(s).get(i), adj, visited, nodes);
        }
    }
    return adjListSize;
}

static int maxEdges(Vector<Vector<Integer>> adj, int nodes)
{
    int res = Integer.MIN_VALUE;
    boolean visited[]=new boolean[nodes+1];
    for (int i = 1; i <= nodes; i++)
    {
        if (visited[i] == false)
        {
            int adjListSize = dfs(i, adj, visited, nodes);
            res = Math.max(res, adjListSize/2);
        }
    }
    return res;
}

// Driver code
public static void main(String args[])
{
    int nodes = 3;
    Vector<Vector<Integer>> adj=new Vector<Vector<Integer>>();

    for(int i = 0; i < nodes + 1; i++)
    adj.add(new Vector<Integer>());

    // Edge from vertex 1 to vertex 2
    adj.get(1).add(2);
    adj.get(2).add(1);

    // Edge from vertex 2 to vertex 3
    adj.get(2).add(3);
    adj.get(3).add(2);

    System.out.println(maxEdges(adj, nodes));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find the connected
# component with maximum number of edges
from sys import maxsize

INT_MIN = -maxsize

# DFS function
def dfs(s: int, adj: list,
        visited: list, nodes: int) -> int:

    # Adding all the edges
    # connected to the vertex
    adjListSize = len(adj[s])
    visited[s] = True

    for i in range(len(adj[s])):

        if visited[adj[s][i]] == False:
            adjListSize += dfs(adj[s][i], adj,
                               visited, nodes)

    return adjListSize

def maxEdges(adj: list, nodes: int) -> int:
    res = INT_MIN
    visited = [False] * (nodes + 1)

    for i in range(1, nodes + 1):

        if visited[i] == False:
            adjListSize = dfs(i, adj,
                              visited, nodes)
            res = max(res, adjListSize // 2)

    return res

# Driver Code
if __name__ == "__main__":

    nodes = 3
    adj = [0] * (nodes + 1)

    for i in range(nodes + 1):
        adj[i] = []

    # Edge from vertex 1 to vertex 2
    adj[1].append(2)
    adj[2].append(1)

    # Edge from vertex 2 to vertex 3
    adj[2].append(3)
    adj[3].append(2)

    print(maxEdges(adj, nodes))

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to find the connected component
// with maximum number of edges
using System;
using System.Collections.Generic;            

class GFG
{

// DFS function
static int dfs(int s, List<List<int>> adj,
               bool []visited, int nodes)
{
    // Adding all the edges connected to the vertex
    int adjListSize = adj[s].Count;
    visited[s] = true;
    for (int i = 0; i < adj[s].Count; i++)
    {
        if (visited[adj[s][i]] == false)
        {
            adjListSize += dfs(adj[s][i], adj,
                               visited, nodes);
        }
    }
    return adjListSize;
}

static int maxEdges(List<List<int>> adj, int nodes)
{
    int res = int.MinValue;
    bool []visited = new bool[nodes + 1];
    for (int i = 1; i <= nodes; i++)
    {
        if (visited[i] == false)
        {
            int adjListSize = dfs(i, adj, visited, nodes);
            res = Math.Max(res, adjListSize / 2);
        }
    }
    return res;
}

// Driver code
public static void Main(String []args)
{
    int nodes = 3;
    List<List<int>> adj = new List<List<int>>();

    for(int i = 0; i < nodes + 1; i++)
    adj.Add(new List<int>());

    // Edge from vertex 1 to vertex 2
    adj[1].Add(2);
    adj[2].Add(1);

    // Edge from vertex 2 to vertex 3
    adj[2].Add(3);
    adj[3].Add(2);

    Console.WriteLine(maxEdges(adj, nodes));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to find the connected component
// with maximum number of edges

// DFS function
function dfs(s,adj,visited,nodes)
{
    // Adding all the edges connected to the vertex
    let adjListSize = adj[s].length;
    visited[s] = true;
    for (let i = 0; i < adj[s].length; i++)
    {
        if (visited[adj[s][i]] == false)
        {
            adjListSize += dfs(adj[s][i], adj, visited, nodes);
        }
    }
    return adjListSize;
}

function maxEdges(adj,nodes)
{
    let res = Number.MIN_VALUE;
    let visited=new Array(nodes+1);
    for(let i=0;i<nodes+1;i++)
    {
        visited[i]=false;
    }
    for (let i = 1; i <= nodes; i++)
    {
        if (visited[i] == false)
        {
            let adjListSize = dfs(i, adj, visited, nodes);
            res = Math.max(res, adjListSize/2);
        }
    }
    return res;
}

// Driver code
let nodes = 3;
let adj=[];

for(let i = 0; i < nodes + 1; i++)
    adj.push([]);

// Edge from vertex 1 to vertex 2
adj[1].push(2);
adj[2].push(1);

// Edge from vertex 2 to vertex 3
adj[2].push(3);
adj[3].push(2);

document.write(maxEdges(adj, nodes)+"<br>");

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(节点+边)(与 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 相同)
注意:我们也可以用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 来解决这个问题。我们只需要遍历无向图中的连通分量。