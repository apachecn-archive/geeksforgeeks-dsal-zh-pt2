# 访问无向加权树所有节点的最小距离

> 原文:[https://www . geesforgeks . org/访问无向加权树的所有节点的最小距离/](https://www.geeksforgeeks.org/minimum-distance-to-visit-all-the-nodes-of-an-undirected-weighted-tree/)

给定一个加权树，从 **1 到 N** 有 **N 个**节点。任意两个节点之间的距离由边权重给出。节点 **1** 是源，任务是访问树中所有行进距离最小的节点。

**示例:**

> **输入:**
> u[] = {1，1，2，2，1}
> v[] = {2，3，5，6，4}
> w[] = {1，4，2，50，5}
> **输出:** 73
> 
> **输入:**
> u[] = {1，2}
> v[] = {2，3}
> w[] = {3，1}
> **输出:** 4

**方法:**假设有 **n** 叶 **l <sub>1</sub>** 、 **l <sub>2</sub>** 、 **l <sub>3</sub>** 、……、 **l <sub>n</sub>** 从根部到每片叶的路径成本为 **c <sub>1</sub>** 、 **c
从 **l <sub>1</sub>** 到 **l <sub>2</sub>** 有些边会被访问两次(直到 **l <sub>1</sub>** 和 **l <sub>2</sub>** 的 [LCA](https://www.geeksforgeeks.org/lowest-common-ancestor-in-a-binary-search-tree/) 所有边都会被访问两次)， 对于**l<sub>2</sub>T58】至 **l <sub>3</sub>** 和部分边将被访问两次(直到**l<sub>2</sub>T68】和**l<sub>3</sub>T72】的 [LCA](https://www.geeksforgeeks.org/lowest-common-ancestor-in-a-binary-search-tree/) 所有边都将被访问两次)，同样，树的每条边都将被访问两次********

为了最小化旅行成本，应该避免从根到某片叶子的最大成本路径。
于是成本=(**c<sub>1</sub>T4】+**c<sub>2</sub>T8】+**c<sub>3</sub>T12】+……+**c<sub>n</sub>T16)–**max**(**c<sub>1</sub>T22】、**c<sub>2</sub>T26】、 **c **c<sub>n</sub>**)
**最小成本** = **(2 *边重之和)**–**最大**(**c<sub>1</sub>T45】，**c<sub>2</sub>T49】，**c<sub>3</sub>T53】，……，**c<sub>n</sub>**********************

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

class Edge{

    public:

    // from - The source of an edge
    // to - destination of an edge
    // wt - distance between two nodes
    int from;
    int to;
    long wt;

    Edge(int a, int b, long w)
    {
        from = a;
        to = b;
        wt = w;
    }
};

// Method to add an edge between two nodes
void add_edge(vector<vector<Edge>> &adj_lis,
              int to, int from, long wt)
{
    adj_lis[from].push_back(Edge(from, to, wt));
    adj_lis[to].push_back(Edge(to, from, wt));
}

// DFS method to find distance
// between node 1 to other nodes
void dfs(vector<vector<Edge>> &adj_lis,
         long val[], int v, int par,
         long sum, bool visited[])
{
    val[v] = sum;
    visited[v] = true;

    for(Edge e : adj_lis[v])
    {
        if (!visited[e.to])
            dfs(adj_lis, val, e.to,
                v, sum + e.wt, visited);
    }
}

// Driver code
int main()
{

    // Number of nodes
    // V - Total number of
    // nodes in a tree
    int v = 6;

    // adj_lis - It is used to
    // make the adjacency list of a tree
    vector<vector<Edge>> adj_lis(v);

    // val - This array stores the
    // distance from node 1 to node 'n'
    long val[v];

    bool visited[v];

    int sum = 0;

    // Edge from a node to another
    // node with some weight
    int from[] = { 2, 3, 5, 6, 4 };
    int to[] = { 1, 1, 2, 2, 1 };
    int wt[] = { 1, 4, 2, 50, 5 };

    for(int i = 0; i < v - 1; i++)
    {
        sum += 2 * wt[i];
        add_edge(adj_lis, to[i] - 1,
                 from[i] - 1, wt[i]);
    }

    dfs(adj_lis, val, 0, -1, 0, visited);
    long large = INT_MIN;

    // Loop to find largest
    // distance in a val.
    int size = sizeof(val) / sizeof(long);

    for(int i = 1; i < size; i++)
        if (val[i] > large)
            large = val[i];

    cout << (sum - large);
}

// This code is contributed by sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.LinkedList;
import java.util.Scanner;

class Graph {

    class Edge {

        // from - The source of an edge
        // to - destination of an edge
        // wt - distance between two nodes
        int from;
        int to;
        long wt;
        Edge(int a, int b, long w)
        {
            from = a;
            to = b;
            wt = w;
        }
    }

    // adj_lis - It is used to
    // make the adjacency list of a tree

    // V - Total number of nodes in a tree

    // val - This array stores the
    // distance from node 1 to node 'n'
    static LinkedList<Edge>[] adj_lis;
    static int V;
    static long val[];

    Graph(int v)
    {
        this.V = v;
        adj_lis = new LinkedList[V];
        for (int i = 0; i < V; i++)
            adj_lis[i] = new LinkedList<>();
    }

    // Method to add an edge between two nodes
    void add_edge(int to, int from, long wt)
    {
        adj_lis[from].add(
            new Edge(from, to, wt));
        adj_lis[to].add(
            new Edge(to, from, wt));
    }

    // DFS method to find distance
    // between node 1 to other nodes
    void dfs(int v,
             int par,
             long sum,
             boolean[] visited)
    {
        val[v] = sum;
        visited[v] = true;
        for (Edge e : adj_lis[v]) {
            if (!visited[e.to])
                dfs(e.to,
                    v,
                    sum + e.wt,
                    visited);
        }
    }

    // Driver code
    public static void main(String a[])
    {

        // Number of nodes
        int v = 6;
        Graph obj = new Graph(v);
        val = new long[v];
        boolean[] visited
            = new boolean[v];

        int sum = 0;

        // Edge from a node to another
        // node with some weight
        int from[] = { 2, 3, 5, 6, 4 };
        int to[] = { 1, 1, 2, 2, 1 };
        int wt[] = { 1, 4, 2, 50, 5 };

        for (int i = 0; i < v - 1; i++) {
            sum += 2 * wt[i];
            obj.add_edge(to[i] - 1,
                         from[i] - 1,
                         wt[i]);
        }

        obj.dfs(0, -1, 0, visited);
        long large = Integer.MIN_VALUE;

        // Loop to find largest
        // distance in a val.
        for (int i = 1; i < val.length;
             i++)
            if (val[i] > large)
                large = val[i];

        System.out.println(sum - large);
    }
}
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;
class Graph
{
    public class Edge
    {

        // from - The source of an edge
        // to - destination of an edge
        // wt - distance between two nodes
        public int from;
        public int to;
        public long wt;
        public Edge(int a, int b, long w)
        {
            from = a;
            to = b;
            wt = w;
        }
    }

    // adj_lis - It is used to
    // make the adjacency list of a tree

    // V - Total number of nodes in a tree

    // val - This array stores the
    // distance from node 1 to node 'n'
    public static List<Edge>[] adj_lis;
    public static int V;
    public static long []val;

    public Graph(int v)
    {
        V = v;
        adj_lis = new List<Edge>[V];
        for (int i = 0; i < V; i++)
            adj_lis[i] = new List<Edge>();
    }

    // Method to add an edge between two nodes
    void add_edge(int to, int from, long wt)
    {
        adj_lis[from].Add(
                 new Edge(from, to, wt));
        adj_lis[to].Add(
               new Edge(to, from, wt));
    }

    // DFS method to find distance
    // between node 1 to other nodes
    void dfs(int v,
            int par,
            long sum,
            bool[] visited)
    {
        val[v] = sum;
        visited[v] = true;
        foreach (Edge e in adj_lis[v])
        {
            if (!visited[e.to])
                dfs(e.to, v,
                    sum + e.wt, visited);
        }
    }

    // Driver code
    public static void Main(String []a)
    {

        // Number of nodes
        int v = 6;
        Graph obj = new Graph(v);
        val = new long[v];
        bool []visited = new bool[v];

        int sum = 0;

        // Edge from a node to another
        // node with some weight
        int []from = { 2, 3, 5, 6, 4 };
        int []to = { 1, 1, 2, 2, 1 };
        int []wt = { 1, 4, 2, 50, 5 };

        for (int i = 0; i < v - 1; i++)
        {
            sum += 2 * wt[i];
            obj.add_edge(to[i] - 1,
                       from[i] - 1, wt[i]);
        }

        obj.dfs(0, -1, 0, visited);
        long large = int.MinValue;

        // Loop to find largest
        // distance in a val.
        for (int i = 1; i < val.Length;
            i++)
            if (val[i] > large)
                large = val[i];

        Console.WriteLine(sum - large);
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of above approach
class Edge
{
    // from - The source of an edge
    // to - destination of an edge
    // wt - distance between two nodes
    constructor(a, b, w)
    {
        this.from = a;
        this.to = b;
        this.wt = w;
    }
}
// adj_lis - It is used to
// make the adjacency list of a tree
// V - Total number of nodes in a tree
// val - This array stores the
// distance from node 1 to node 'n'
var adj_lis = [];
var V =0;
var val =[];

function Graph(v)
{
    V = v;
    adj_lis = Array.from(Array(V), ()=>Array());
}
// Method to add an edge between two nodes
function add_edge(to, from, wt)
{
    adj_lis[from].push(
             new Edge(from, to, wt));
    adj_lis[to].push(
           new Edge(to, from, wt));
}
// DFS method to find distance
// between node 1 to other nodes
function dfs(v, par, sum,  visited)
{
    val[v] = sum;
    visited[v] = true;
    for(var e of adj_lis[v])
    {
        if (!visited[e.to])
            dfs(e.to, v, sum + e.wt, visited);
    }
}

// Driver code
// Number of nodes
var v = 6;
Graph(v);
val = new Array(v).fill(0);
var visited = Array(v).fill(false);
var sum = 0;
// Edge from a node to another
// node with some weight
var from = [2, 3, 5, 6, 4];
var to = [1, 1, 2, 2, 1];
var wt = [1, 4, 2, 50, 5];
for(var i = 0; i < v - 1; i++)
{
    sum += 2 * wt[i];
    add_edge(to[i] - 1,
               from[i] - 1, wt[i]);
}
dfs(0, -1, 0, visited);
var large = -100000;
// Loop to find largest
// distance in a val.
for (var i = 1; i < val.length;i++)
    if (val[i] > large)
        large = val[i];
document.write(sum - large);

</script>
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

class Edge:

    # src - The source of an edge
    # to - destination of an edge
    # wt - distance between two nodes
    def __init__(self, a, b, w):
        self.src = a
        self.to = b
        self.wt = w

# Method to add an edge between two nodes
def add_edge(adj_lis, to, src, wt):
    adj_lis[src].append(Edge(src, to, wt))
    adj_lis[to].append(Edge(to, src, wt))

# DFS method to find distance
# between node 1 to other nodes
def dfs(adj_lis, val, v, par, sum, visited):
    val[v] = sum
    visited[v] = True

    for e in adj_lis[v]:
        if (not visited[e.to]):
            dfs(adj_lis, val, e.to, v, sum + e.wt, visited)

# Driver code
if __name__ == '__main__':

    # Number of nodes
    # V - Total number of
    # nodes in a tree
    v = 6

    # adj_lis - It is used to
    # make the adjacency list of a tree
    adj_lis=[[] for _ in range(v)]

    # val - This array stores the
    # distance src node 1 to node 'n'
    val=[-1]*v

    visited=[False]*v

    sum = 0

    # Edge src a node to another
    # node with some weight
    src = [ 2, 3, 5, 6, 4]
    to = [ 1, 1, 2, 2, 1 ]
    wt = [ 1, 4, 2, 50, 5 ]

    for i in range(v - 1):
        sum += 2 * wt[i]
        add_edge(adj_lis, to[i] - 1,
                 src[i] - 1, wt[i])

    dfs(adj_lis, val, 0, -1, 0, visited)
    large = -1e9

    # Loop to find largest
    # distance in a val.
    size = len(val)

    for i in range(1,size):
        if (val[i] > large):
            large = val[i]

    print(sum - large)

# This code is contributed by Amartya Ghosh
```

**Output:** 

```
73
```

**时间复杂度:** O(N)。
**辅助空间** : O(N)。