# 从无向图中移除的最小标记节点，这样就没有循环

> 原文:[https://www . geesforgeks . org/从无向图中移除最小标记节点-这样就没有循环/](https://www.geeksforgeeks.org/minimum-labelled-node-to-be-removed-from-undirected-graph-such-that-there-is-no-cycle/)

给定一个从 1 到 N 标记的 **N** 节点的**无向图**，任务是找到应该从图中移除的最小标记节点，使得结果图没有循环。

**注意:**如果初始图形没有循环，即没有需要移除的节点，打印-1。

**示例:**

> **输入:** N = 5，边[][] = {{5，1}，{5，2}，{1，2}，{2，3}，{2，4}}
> **输出:** 1
> **解释:**
> 如果移除节点 1，则结果图没有循环。类似地，也可以通过移除节点 2 来避免该循环。
> 因为我们必须找到最小的标签节点，所以答案是 1。
> 
> **输入:** N = 5，边[][] = {{4，5}，{4，1}，{4，2}，{4，3}，{5，1}，{5，2}}
> **输出:** 4

**天真方法:**这个问题的天真方法是单独移除每个顶点，并检查结果图是否有循环。这种方法的时间复杂度是二次的。

**高效方法:**思路是在给定的图上应用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)，观察形成的 dfs 树。

*   A [后边缘](https://www.geeksforgeeks.org/tree-back-edge-and-cross-edges-in-dfs-of-graph/)指的是不属于所构建的 DFS 树的一部分的边缘，并且是某个节点 v 和 v 的祖先之一之间的边缘。
*   显然，图中不属于 DFS 树的所有边都是后边。
*   如果图中没有后边缘，则图没有循环。所以，在这种情况下，答案将是 **-1** 。

如果图中有[后沿](https://www.geeksforgeeks.org/tree-back-edge-and-cross-edges-in-dfs-of-graph/)，那么我们需要找到最小边。为了做到这一点，我们需要检查在从图中移除特定边时循环是否被移除。因此，让 **v** 成为我们当前正在检查的顶点。因此，**以下条件必须跟随着顶点 v** ，这样在移除时，就不会导致循环:

*   **v** 必须位于连接图中每个[后边缘](https://www.geeksforgeeks.org/tree-back-edge-and-cross-edges-in-dfs-of-graph/)端点的树路径上。
    **证明:**假设存在某种后沿 x-y，使得 v 不位于树路径上。如果我们去掉 v，我们仍然能够从 x 到 y，并通过后沿回到 x，这表明循环没有被去掉。
*   v 的子树最多必须有一条到 v 的任何祖先的后边缘
    **证明:**让子树 S 必须有后边缘 w-x 和 y-z，这样 w 和 y 在 S 中，x 和 z 是 v 的祖先。如果我们去掉 v，显然仍然存在一个由 w 到 y 之间的路径、从 x 到 z 的路径以及两个后边缘 w-x 和 y-z 组成的循环，即循环没有被去掉。

因此，这个想法是保持一个后边缘的轨迹，以及一个节点的子树中的后边缘数量到它的任何祖先的指示器。为了保持对后边缘的跟踪，我们将使用[修正的 DFS 图着色算法](https://www.geeksforgeeks.org/detect-cycle-direct-graph-using-colors/)。
为了检查子树 v 是否至多有一条后边缘通向 v 的任何祖先，我们实现 [dfs](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 以使它返回 v 的子树的两条最高边缘的深度。我们维护一个数组，其中数组中的每个索引“I”存储节点“I”是否满足上面的条件 2。类似地，实现了两个数组，一个用于子数组，另一个用于父数组，以查看节点 v 是否位于连接端点的树路径上。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum labelled node to be
// removed such that there is no
// cycle in the undirected graph

#include <bits/stdc++.h>

using namespace std;

const int MAX = 100005;

int totBackEdges;
int countAdj[MAX], small[MAX];

// Variables to store if a node V has
// at-most one back edge and store the
// depth of the node for the edge
int isPossible[MAX], depth[MAX];

vector<int> adj[MAX];
int vis[MAX];

// Function to swap the pairs of the graph
void change(pair<int, int>& p, int x)
{
    // If the second value is
    // greater than x
    if (p.second > x)
        p.second = x;

    // Put the pair in the ascending
    // order internally
    if (p.first > p.second)
        swap(p.first, p.second);
}

// Function to perform the DFS
pair<int, int> dfs(int v, int p = -1, int de = 0)
{
    // Initialise with the large value
    pair<int, int> answer(100000000, 100000000);

    // Storing the depth of this vertex
    depth[v] = de;

    // Mark the vertex as visited
    vis[v] = 1;
    isPossible[v] = 1;

    // Iterating through the graph
    for (int u : adj[v]) {

        // If the node is a child node
        if (u ^ p) {

            // If the child node is unvisited
            if (!vis[u]) {

                // Move to the child and increase
                // the depth
                auto x = dfs(u, v, de + 1);

                // increase according to algorithm
                small[v] += small[u];

                change(answer, x.second);
                change(answer, x.first);

                // If the node is not having
                // exactly K backedges
                if (x.second < de)
                    isPossible[v] = 0;
            }

            // If the child is already visited
            // and in current dfs
            // (because colour is 1)
            // then this is a back edge
            else if (vis[u] == 1) {
                totBackEdges++;

                // Increase the countAdj values
                countAdj[v]++;
                countAdj[u]++;
                small[p]++;
                small[u]--;
                change(answer, depth[u]);
            }
        }
    }

    // Colour this vertex 2 as
    // we are exiting out of
    // dfs for this node
    vis[v] = 2;
    return answer;
}

// Function to find the minimum labelled
// node to be removed such that
// there is no cycle in the undirected graph
int minNodetoRemove(
    int n,
    vector<pair<int, int> > edges)
{

    // Construct the graph
    for (int i = 0; i < edges.size(); i++) {
        adj[edges[i].first]
            .push_back(edges[i].second);
        adj[edges[i].second]
            .push_back(edges[i].first);
    }

    // Mark visited as false for each node
    memset(vis, 0, sizeof(vis));

    totBackEdges = 0;

    // Apply dfs on all unmarked nodes
    for (int v = 1; v <= n; v++) {
        if (!vis[v])
            dfs(v);
    }

    // If no backedges in the initial graph
    // this means that there is no cycle
    // So, return -1
    if (totBackEdges == 0)
        return -1;

    int node = -1;

    // Iterate through the vertices and
    // return the first node that
    // satisfies the condition
    for (int v = 1; v <= n; v++) {

        // Check whether the count sum of
        // small[v] and count is the same as
        // the total back edges and
        // if the vertex v can be removed
        if (countAdj[v] + small[v]
                == totBackEdges
            && isPossible[v]) {
            node = v;
        }
        if (node != -1)
            break;
    }

    return node;
}

// Driver code
int main()
{
    int N = 5;
    vector<pair<int, int> > edges;
    edges.push_back(make_pair(5, 1));
    edges.push_back(make_pair(5, 2));
    edges.push_back(make_pair(1, 2));
    edges.push_back(make_pair(2, 3));
    edges.push_back(make_pair(2, 4));

    cout << minNodetoRemove(N, edges);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum labelled node to be
// removed such that there is no
// cycle in the undirected graph
import java.util.ArrayList;
import java.util.Arrays;

class Pair
{
    int first, second;

    public Pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

class GFG{

static final int MAX = 100005;

static int totBackEdges;
static int[] countAdj = new int[MAX];
static int[] small = new int[MAX];

// Variables to store if a node V has
// at-most one back edge and store the
// depth of the node for the edge
static int[] isPossible = new int[MAX];
static int[] depth = new int[MAX];

@SuppressWarnings("unchecked")
static ArrayList<Integer>[] adj = new ArrayList[MAX];

static int[] vis = new int[MAX];

// Function to swap the pairs of the graph
static void change(Pair p, int x)
{

    // If the second value is
    // greater than x
    if (p.second > x)
        p.second = x;

    // Put the Pair in the ascending
    // order internally
    if (p.first > p.second)
    {
        int tmp = p.first;
        p.first = p.second;
        p.second = tmp;
    }
}

// Function to perform the DFS
static Pair dfs(int v, int p, int de)
{

    // Initialise with the large value
    Pair answer = new Pair(100000000, 100000000);

    // Storing the depth of this vertex
    depth[v] = de;

    // Mark the vertex as visited
    vis[v] = 1;
    isPossible[v] = 1;

    // Iterating through the graph
    for(int u : adj[v])
    {

        // If the node is a child node
        if ((u ^ p) != 0)
        {

            // If the child node is unvisited
            if (vis[u] == 0)
            {

                // Move to the child and increase
                // the depth
                Pair x = dfs(u, v, de + 1);

                // increase according to algorithm
                small[v] += small[u];

                change(answer, x.second);
                change(answer, x.first);

                // If the node is not having
                // exactly K backedges
                if (x.second < de)
                    isPossible[v] = 0;
            }

            // If the child is already visited
            // and in current dfs
            // (because colour is 1)
            // then this is a back edge
            else if (vis[u] == 1)
            {
                totBackEdges++;

                // Increase the countAdj values
                countAdj[v]++;
                countAdj[u]++;
                small[p]++;
                small[u]--;
                change(answer, depth[u]);
            }
        }
    }

    // Colour this vertex 2 as
    // we are exiting out of
    // dfs for this node
    vis[v] = 2;
    return answer;
}

// Function to find the minimum labelled
// node to be removed such that
// there is no cycle in the undirected graph
static int minNodetoRemove(int n, ArrayList<Pair> edges)
{

    // Construct the graph
    for(int i = 0; i < edges.size(); i++)
    {
        adj[edges.get(i).first].add(
            edges.get(i).second);
        adj[edges.get(i).second].add(
            edges.get(i).first);
    }

    // Mark visited as false for each node
    Arrays.fill(vis, 0);

    totBackEdges = 0;

    // Apply dfs on all unmarked nodes
    for(int v = 1; v <= n; v++)
    {
        if (vis[v] == 0)
            dfs(v, -1, 0);
    }

    // If no backedges in the initial graph
    // this means that there is no cycle
    // So, return -1
    if (totBackEdges == 0)
        return -1;

    int node = -1;

    // Iterate through the vertices and
    // return the first node that
    // satisfies the condition
    for(int v = 1; v <= n; v++)
    {

        // Check whether the count sum of
        // small[v] and count is the same as
        // the total back edges and
        // if the vertex v can be removed
        if ((countAdj[v] + small[v] == totBackEdges) &&
           isPossible[v] != 0)
        {
            node = v;
        }

        if (node != -1)
            break;
    }
    return node;
}

// Driver code
public static void main(String[] args)
{
    int N = 5;

    ArrayList<Pair> edges = new ArrayList<>();
    for(int i = 0; i < MAX; i++)
    {
        adj[i] = new ArrayList<>();
    }

    edges.add(new Pair(5, 1));
    edges.add(new Pair(5, 2));
    edges.add(new Pair(1, 2));
    edges.add(new Pair(2, 3));
    edges.add(new Pair(2, 4));

    System.out.println(minNodetoRemove(N, edges));
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum labelled node to be
# removed such that there is no
# cycle in the undirected graph 
MAX = 100005; 
totBackEdges = 0
countAdj = [0 for i in range(MAX)]
small = [0 for i in range(MAX)]

# Variables to store if a node V has
# at-most one back edge and store the
# depth of the node for the edge
isPossible = [0 for i in range(MAX)]
depth = [0 for i in range(MAX)]
adj = [[] for i in range(MAX)]
vis = [0 for i in range(MAX)]

# Function to swap the pairs of the graph
def change(p, x):

    # If the second value is
    # greater than x
    if (p[1] > x):
        p[1] = x;

    # Put the pair in the ascending
    # order internally
    if (p[0] > p[1]):

       tmp = p[0];
       p[0] = p[1];
       p[1] = tmp;

# Function to perform the DFS
def dfs(v, p = -1, de = 0):
    global vis, totBackEdges

    # Initialise with the large value
    answer = [100000000, 100000000]

    # Storing the depth of this vertex
    depth[v] = de;

    # Mark the vertex as visited
    vis[v] = 1;
    isPossible[v] = 1;

    # Iterating through the graph
    for u in adj[v]:

        # If the node is a child node
        if ((u ^ p) != 0):

            # If the child node is unvisited
            if (vis[u] == 0):

                # Move to the child and increase
                # the depth
                x = dfs(u, v, de + 1);

                # increase according to algorithm
                small[v] += small[u];

                change(answer, x[1]);
                change(answer, x[0]);

                # If the node is not having
                # exactly K backedges
                if (x[1] < de):
                    isPossible[v] = 0;

            # If the child is already visited
            # and in current dfs
            # (because colour is 1)
            # then this is a back edge
            elif (vis[u] == 1):
                totBackEdges += 1

                # Increase the countAdj values
                countAdj[v] += 1
                countAdj[u] += 1
                small[p] += 1
                small[u] -= 1
                change(answer, depth[u]);

    # Colour this vertex 2 as
    # we are exiting out of
    # dfs for this node
    vis[v] = 2;
    return answer;

# Function to find the minimum labelled
# node to be removed such that
# there is no cycle in the undirected graph
def minNodetoRemove( n, edges):

    # Construct the graph
    for i in range(len(edges)):

        adj[edges[i][0]].append(edges[i][1]);
        adj[edges[i][1]].append(edges[i][0]);

    global vis, totBackEdges

    # Mark visited as false for each node
    vis = [0 for i in range(len(vis))] 
    totBackEdges = 0;

    # Apply dfs on all unmarked nodes
    for v in range(1, n + 1):  
        if (vis[v] == 0):
            dfs(v);

    # If no backedges in the initial graph
    # this means that there is no cycle
    # So, return -1
    if (totBackEdges == 0):
        return -1; 
    node = -1;

    # Iterate through the vertices and
    # return the first node that
    # satisfies the condition
    for v in range(1, n + 1):

        # Check whether the count sum of
        # small[v] and count is the same as
        # the total back edges and
        # if the vertex v can be removed
        if ((countAdj[v] + small[v] == totBackEdges) and isPossible[v] != 0):
            node = v;      
        if (node != -1):
            break; 
    return node;

# Driver code
if __name__=='__main__':   
    N = 5;
    edges = []
    edges.append([5, 1]);
    edges.append([5, 2]);
    edges.append([1, 2]);
    edges.append([2, 3]);
    edges.append([2, 4]); 
    print(minNodetoRemove(N, edges));

    # This code is contributed by Pratham76
```

## C#

```
// C# implementation to find the
// minimum labelled node to be
// removed such that there is no
// cycle in the undirected graph

using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

static int MAX = 100005;

static int totBackEdges;
static int []countAdj = new int[MAX];
static int []small = new int[MAX];

// Variables to store if a node V has
// at-most one back edge and store the
// depth of the node for the edge
static int []isPossible = new int[MAX];
static int []depth = new int[MAX];

static ArrayList adj = new ArrayList();

static int []vis = new int[MAX];

class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to swap the pairs of the graph
static void change(ref pair p, int x)
{
    // If the second value is
    // greater than x
    if (p.second > x)
        p.second = x;

    // Put the pair in the ascending
    // order internally
    if (p.first > p.second)
    { 
       int tmp = p.first;
       p.first = p.second;
       p.second = tmp;
    }
}

// Function to perform the DFS
static pair dfs(int v, int p = -1, int de = 0)
{
    // Initialise with the large value
    pair answer = new pair(100000000, 100000000);

    // Storing the depth of this vertex
    depth[v] = de;

    // Mark the vertex as visited
    vis[v] = 1;
    isPossible[v] = 1;

    // Iterating through the graph
    foreach (int u in (ArrayList)adj[v]) {

        // If the node is a child node
        if ((u ^ p) != 0) {

            // If the child node is unvisited
            if (vis[u] == 0) {

                // Move to the child and increase
                // the depth
                pair x = dfs(u, v, de + 1);

                // increase according to algorithm
                small[v] += small[u];

                change(ref answer, x.second);
                change(ref answer, x.first);

                // If the node is not having
                // exactly K backedges
                if (x.second < de)
                    isPossible[v] = 0;
            }

            // If the child is already visited
            // and in current dfs
            // (because colour is 1)
            // then this is a back edge
            else if (vis[u] == 1) {
                totBackEdges++;

                // Increase the countAdj values
                countAdj[v]++;
                countAdj[u]++;
                small[p]++;
                small[u]--;
                change(ref answer, depth[u]);
            }
        }
    }

    // Colour this vertex 2 as
    // we are exiting out of
    // dfs for this node
    vis[v] = 2;
    return answer;
}

// Function to find the minimum labelled
// node to be removed such that
// there is no cycle in the undirected graph
static int minNodetoRemove(
    int n,
    ArrayList edges)
{

    // Construct the graph
    for (int i = 0; i < edges.Count; i++) {
        ((ArrayList)adj[((pair)edges[i]).first])
            .Add(((pair)edges[i]).second);
        ((ArrayList)adj[((pair)edges[i]).second])
            .Add(((pair)edges[i]).first);
    }

    // Mark visited as false for each node
    Array.Fill(vis, 0);

    totBackEdges = 0;

    // Apply dfs on all unmarked nodes
    for (int v = 1; v <= n; v++) {
        if (vis[v] == 0)
            dfs(v);
    }

    // If no backedges in the initial graph
    // this means that there is no cycle
    // So, return -1
    if (totBackEdges == 0)
        return -1;

    int node = -1;

    // Iterate through the vertices and
    // return the first node that
    // satisfies the condition
    for (int v = 1; v <= n; v++) {

        // Check whether the count sum of
        // small[v] and count is the same as
        // the total back edges and
        // if the vertex v can be removed
        if ((countAdj[v] + small[v] == totBackEdges) && isPossible[v] != 0) {
            node = v;
        }
        if (node != -1)
            break;
    }

    return node;
}

// Driver code
static void Main()
{
    int N = 5;
    ArrayList edges = new ArrayList();
    for(int i = 0; i < MAX; i++)
    {
        adj.Add(new ArrayList());
    }
    edges.Add(new pair(5, 1));
    edges.Add(new pair(5, 2));
    edges.Add(new pair(1, 2));
    edges.Add(new pair(2, 3));
    edges.Add(new pair(2, 4));

    Console.Write(minNodetoRemove(N, edges));
  }
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// minimum labelled node to be
// removed such that there is no
// cycle in the undirected graph
var MAX = 100005;
var totBackEdges;
var countAdj = Array(MAX).fill(0);
var small = Array(MAX).fill(0);

// Variables to store if a node V has
// at-most one back edge and store the
// depth of the node for the edge
var isPossible = Array(MAX).fill(0);
var depth = Array(MAX).fill(0);

var adj = [];
var vis = Array(MAX).fill(0);

class pair
{
    constructor(first, second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to swap the pairs of the graph
function change(p, x)
{

    // If the second value is
    // greater than x
    if (p.second > x)
        p.second = x;

    // Put the pair in the ascending
    // order internally
    if (p.first > p.second)
    {
        var tmp = p.first;
        p.first = p.second;
        p.second = tmp;
    }
}

// Function to perform the DFS
function dfs(v, p = -1, de = 0)
{

    // Initialise with the large value
    var answer = new pair(100000000, 100000000);

    // Storing the depth of this vertex
    depth[v] = de;

    // Mark the vertex as visited
    vis[v] = 1;
    isPossible[v] = 1;

    // Iterating through the graph
    for(var u of adj[v])
    {

        // If the node is a child node
        if ((u ^ p) != 0)
        {

            // If the child node is unvisited
            if (vis[u] == 0)
            {

                // Move to the child and increase
                // the depth
                var x = dfs(u, v, de + 1);

                // Increase according to algorithm
                small[v] += small[u];

                change(answer, x.second);
                change(answer, x.first);

                // If the node is not having
                // exactly K backedges
                if (x.second < de)
                    isPossible[v] = 0;
            }

            // If the child is already visited
            // and in current dfs
            // (because colour is 1)
            // then this is a back edge
            else if (vis[u] == 1)
            {
                totBackEdges++;

                // Increase the countAdj values
                countAdj[v]++;
                countAdj[u]++;
                small[p]++;
                small[u]--;
                change(answer, depth[u]);
            }
        }
    }

    // Colour this vertex 2 as
    // we are exiting out of
    // dfs for this node
    vis[v] = 2;
    return answer;
}

// Function to find the minimum labelled
// node to be removed such that
// there is no cycle in the undirected graph
function minNodetoRemove(n, edges)
{

    // Construct the graph
    for(var i = 0; i < edges.length; i++)
    {
        (adj[(edges[i]).first]).push(
            (edges[i]).second);
        (adj[(edges[i]).second]).push(
            (edges[i]).first);
    }

    // Mark visited as false for each node
    vis = Array(MAX).fill(0);

    totBackEdges = 0;

    // Apply dfs on all unmarked nodes
    for(var v = 1; v <= n; v++)
    {
        if (vis[v] == 0)
            dfs(v);
    }

    // If no backedges in the initial graph
    // this means that there is no cycle
    // So, return -1
    if (totBackEdges == 0)
        return -1;

    var node = -1;

    // Iterate through the vertices and
    // return the first node that
    // satisfies the condition
    for(var v = 1; v <= n; v++)
    {

        // Check whether the count sum of
        // small[v] and count is the same as
        // the total back edges and
        // if the vertex v can be removed
        if ((countAdj[v] + small[v] == totBackEdges) &&
            isPossible[v] != 0)
        {
            node = v;
        }
        if (node != -1)
            break;
    }
    return node;
}

// Driver code
var N = 5;
var edges = [];
for(var i = 0; i < MAX; i++)
{
    adj.push(new Array());
}

edges.push(new pair(5, 1));
edges.push(new pair(5, 2));
edges.push(new pair(1, 2));
edges.push(new pair(2, 3));
edges.push(new pair(2, 4));

document.write(minNodetoRemove(N, edges));

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
1
```

**时间复杂度:** *O(N + M)* ，其中 N 为节点数，M 为边数。
**辅助空间:** O(N + M)。