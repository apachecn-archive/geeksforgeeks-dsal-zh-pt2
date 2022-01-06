# 树上不相交的集合并集|集合 1

> 原文:[https://www . geesforgeks . org/disjoint-set-union-trees-set-1/](https://www.geeksforgeeks.org/disjoint-set-union-trees-set-1/)

给定树和节点权重。权重是非负整数。任务是找到给定树的子树的最大大小，使得所有节点的权重相等。
**先决条件:** [不相交集合并集](https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/)

**示例:**

```
Input : Number of nodes = 7
        Weights of nodes = 1 2 6 4 2 0 3
        Edges = (1, 2), (1, 3), (2, 4), 
                (2, 5), (4, 6), (6, 7)
Output : Maximum size of the subtree 
with even weighted nodes = 4 
Explanation : 
Subtree of nodes {2, 4, 5, 6} gives the maximum size.

Input : Number of nodes = 6
        Weights of nodes = 2 4 0 2 2 6
        Edges = (1, 2), (2, 3), (3, 4), 
                (4, 5), (1, 6)
Output : Maximum size of the subtree
with even weighted nodes = 6
Explanation : 
The given tree gives the maximum size.
```

**方法:**我们只需在树上运行 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 就可以找到解决方案。DFS 解决方案在*T5【O(n)T7】中给了我们答案。但是，我们如何利用 DSU 来解决这个问题呢？我们首先遍历所有边。如果两个节点的权重相等，我们就把它们合并。最大大小的节点集就是答案。如果我们使用联合查找和路径压缩，那么时间复杂度是 ***O(n)*** 。*

**以下是上述方法的实施:**

## C++

```
// CPP code to find maximum subtree such
// that all nodes are even in weight
#include<bits/stdc++.h>

using namespace std;

#define N 100010

// Structure for Edge
struct Edge
{
    int u, v;
};

/*
    'id': stores parent of a node.
    'sz': stores size of a DSU tree.
*/
int id[N], sz[N];

// Function to assign root
int Root(int idx)
{
    int i = idx;

    while(i != id[i])
        id[i] = id[id[i]], i = id[i];

    return i;
}

// Function to find Union
void Union(int a, int b)
{
    int i = Root(a), j = Root(b);

    if (i != j)
    {
        if(sz[i] >= sz[j])
        {
            id[j] = i, sz[i] += sz[j];
            sz[j] = 0;
        }
        else
        {
            id[i] = j, sz[j] += sz[i];
            sz[i] = 0;
        }
    }
}

// Utility function for Union
void UnionUtil(struct Edge e[], int W[], int q)
{

    for(int i = 0; i < q; i++)
    {
        // Edge between 'u' and 'v'
        int u, v;
        u = e[i].u, v = e[i].v;

        // 0-indexed nodes
        u--, v--;

        // If weights of both 'u' and 'v'
        // are even then we make union of them.
        if(W[u] % 2 == 0 && W[v] % 2 == 0)
                    Union(u,v);
    }
}

// Function to find maximum
// size of DSU tree
int findMax(int n, int W[])
{
    int maxi = 0;
    for(int i = 1; i <= n; i++)
        if(W[i] % 2 == 0)
            maxi = max(maxi, sz[i]);  

    return maxi;
}

// Driver code
int main()
{
    /*
        Nodes are 0-indexed in this code
        So we have to make necessary changes
        while taking inputs
    */

    // Weights of nodes
    int W[] = {1, 2, 6, 4, 2, 0, 3};

    // Number of nodes in a tree
    int n = sizeof(W) / sizeof(W[0]);

    // Initializing every node as
    // a tree with single node.
    for(int i = 0; i < n; i++)
            id[i] = i, sz[i] = 1;

    Edge e[] = {{1, 2}, {1, 3}, {2, 4},
                {2, 5}, {4, 6}, {6, 7}};

    int q = sizeof(e) / sizeof(e[0]);

    UnionUtil(e, W, q);

    // Find maximum size of DSU tree.
    int maxi = findMax(n, W);

    printf("Maximum size of the subtree with ");
    printf("even weighted nodes = %d\n", maxi);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find maximum subtree such
// that all nodes are even in weight
class GFG
{
static int N = 100010;

// Structure for Edge
static class Edge
{
    int u, v;

    public Edge(int u, int v)
    {
        this.u = u;
        this.v = v;
    }
}

/*
'id': stores parent of a node.
'sz': stores size of a DSU tree.
*/
static int []id = new int[N];
static int []sz = new int[N];

// Function to assign root
static int Root(int idx)
{
    int i = idx;

    while(i != id[i])
    {
        id[i] = id[id[i]];
        i = id[i];
    }
    return i;
}

// Function to find Union
static void Union(int a, int b)
{
    int i = Root(a), j = Root(b);

    if (i != j)
    {
        if(sz[i] >= sz[j])
        {
            id[j] = i;
            sz[i] += sz[j];
            sz[j] = 0;
        }
        else
        {
            id[i] = j;
            sz[j] += sz[i];
            sz[i] = 0;
        }
    }
}

// Utility function for Union
static void UnionUtil(Edge e[], int W[], int q)
{
    for(int i = 0; i < q; i++)
    {
        // Edge between 'u' and 'v'
        int u, v;
        u = e[i].u;
        v = e[i].v;

        // 0-indexed nodes
        u--;
        v--;

        // If weights of both 'u' and 'v'
        // are even then we make union of them.
        if(W[u] % 2 == 0 && W[v] % 2 == 0)
            Union(u, v);
    }
}

// Function to find maximum
// size of DSU tree
static int findMax(int n, int W[])
{
    int maxi = 0;
    for(int i = 1; i < n; i++)
        if(W[i] % 2 == 0)
            maxi = Math.max(maxi, sz[i]);

    return maxi;
}

// Driver code
public static void main(String[] args)
{
    /*
    Nodes are 0-indexed in this code
    So we have to make necessary changes
    while taking inputs
    */

    // Weights of nodes
    int W[] = {1, 2, 6, 4, 2, 0, 3};

    // Number of nodes in a tree
    int n = W.length;

    // Initializing every node as
    // a tree with single node.
    for(int i = 0; i < n; i++)
    {
        id[i] = i;
        sz[i] = 1;
    }

    Edge e[] = {new Edge(1, 2), new Edge(1, 3),
                new Edge(2, 4), new Edge(2, 5),
                new Edge(4, 6), new Edge(6, 7)};

    int q = e.length;

    UnionUtil(e, W, q);

    // Find maximum size of DSU tree.
    int maxi = findMax(n, W);

    System.out.printf("Maximum size of the subtree with ");
    System.out.printf("even weighted nodes = %d\n", maxi);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 code to find maximum subtree such
# that all nodes are even in weight
N = 100010

# Structure for Edge
class Edge:

    def __init__(self, u, v):
        self.u = u
        self.v = v

'''
    'id': stores parent of a node.
    'sz': stores size of a DSU tree.
'''

id = [0 for i in range(N)]
sz = [0 for i in range(N)];

# Function to assign root
def Root(idx):

    i = idx;

    while(i != id[i]):

        id[i] = id[id[i]]
        i = id[i];

    return i;

# Function to find Union
def Union(a, b):

    i = Root(a)
    j = Root(b);

    if (i != j):

        if(sz[i] >= sz[j]):

            id[j] = i
            sz[i] += sz[j];
            sz[j] = 0;
        else:

            id[i] = j
            sz[j] += sz[i];
            sz[i] = 0;

# Utility function for Union
def UnionUtil( e, W, q):

    for i in range(q):

         # Edge between 'u' and 'v'
        u = e[i].u
        v = e[i].v

        # 0-indexed nodes
        u -= 1
        v -= 1

        # If weights of both 'u' and 'v'
        # are even then we make union of them.
        if(W[u] % 2 == 0 and W[v] % 2 == 0):
            Union(u, v);

# Function to find maximum
# size of DSU tree
def findMax(n, W):

    maxi = 0

    for i in range(1, n):

        if(W[i] % 2 == 0):
            maxi = max(maxi, sz[i]);  

    return maxi;

# Driver code
if __name__=='__main__':

    '''
        Nodes are 0-indexed in this code
        So we have to make necessary changes
        while taking inputs
    '''

    # Weights of nodes
    W = [1, 2, 6, 4, 2, 0, 3]

    # Number of nodes in a tree
    n = len(W)

    # Initializing every node as
    # a tree with single node.
    for i in range(n):

            id[i] = i
            sz[i] = 1;

    e = [Edge(1, 2), Edge(1, 3), Edge(2, 4),
                Edge(2, 5), Edge(4, 6), Edge(6, 7)]

    q = len(e)

    UnionUtil(e, W, q);

    # Find maximum size of DSU tree.
    maxi = findMax(n, W);

    print("Maximum size of the subtree with ", end='');
    print("even weighted nodes =", maxi);

# This code is contributed by rutvik_56
```

## C#

```
// C# code to find maximum subtree such
// that all nodes are even in weight
using System;

class GFG
{
static int N = 100010;

// Structure for Edge
public class Edge
{
    public int u, v;

    public Edge(int u, int v)
    {
        this.u = u;
        this.v = v;
    }
}

/*
'id': stores parent of a node.
'sz': stores size of a DSU tree.
*/
static int []id = new int[N];
static int []sz = new int[N];

// Function to assign root
static int Root(int idx)
{
    int i = idx;

    while(i != id[i])
    {
        id[i] = id[id[i]];
        i = id[i];
    }
    return i;
}

// Function to find Union
static void Union(int a, int b)
{
    int i = Root(a), j = Root(b);

    if (i != j)
    {
        if(sz[i] >= sz[j])
        {
            id[j] = i;
            sz[i] += sz[j];
            sz[j] = 0;
        }
        else
        {
            id[i] = j;
            sz[j] += sz[i];
            sz[i] = 0;
        }
    }
}

// Utility function for Union
static void UnionUtil(Edge []e, int []W, int q)
{
    for(int i = 0; i < q; i++)
    {
        // Edge between 'u' and 'v'
        int u, v;
        u = e[i].u;
        v = e[i].v;

        // 0-indexed nodes
        u--;
        v--;

        // If weights of both 'u' and 'v'
        // are even then we make union of them.
        if(W[u] % 2 == 0 && W[v] % 2 == 0)
            Union(u, v);
    }
}

// Function to find maximum
// size of DSU tree
static int findMax(int n, int []W)
{
    int maxi = 0;
    for(int i = 1; i < n; i++)
        if(W[i] % 2 == 0)
            maxi = Math.Max(maxi, sz[i]);

    return maxi;
}

// Driver code
public static void Main(String[] args)
{
    /*
    Nodes are 0-indexed in this code
    So we have to make necessary changes
    while taking inputs
    */

    // Weights of nodes
    int []W = {1, 2, 6, 4, 2, 0, 3};

    // Number of nodes in a tree
    int n = W.Length;

    // Initializing every node as
    // a tree with single node.
    for(int i = 0; i < n; i++)
    {
        id[i] = i;
        sz[i] = 1;
    }

    Edge []e = {new Edge(1, 2), new Edge(1, 3),
                new Edge(2, 4), new Edge(2, 5),
                new Edge(4, 6), new Edge(6, 7)};

    int q = e.Length;

    UnionUtil(e, W, q);

    // Find maximum size of DSU tree.
    int maxi = findMax(n, W);

    Console.Write("Maximum size of the subtree with ");
    Console.WriteLine("even weighted nodes = {0}\n", maxi);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript code to find maximum subtree such
// that all nodes are even in weight
let N = 100010;

/*
'id': stores parent of a node.
'sz': stores size of a DSU tree.
*/
let id = new Array(N);
let sz = new Array(N);

// Function to assign root
function Root(idx)
{
    let i = idx;

    while(i != id[i])
    {
        id[i] = id[id[i]];
        i = id[i];
    }
    return i;
}

// Function to find Union
function Union(a, b)
{
    let i = Root(a), j = Root(b);

    if (i != j)
    {
        if (sz[i] >= sz[j])
        {
            id[j] = i;
            sz[i] += sz[j];
            sz[j] = 0;
        }
        else
        {
            id[i] = j;
            sz[j] += sz[i];
            sz[i] = 0;
        }
    }
}

// Utility function for Union
function UnionUtil(e, W, q)
{
    for(let i = 0; i < q; i++)
    {

        // Edge between 'u' and 'v'
        let u, v;
        u = e[i][0];
        v = e[i][1];

        // 0-indexed nodes
        u--;
        v--;

        // If weights of both 'u' and 'v'
        // are even then we make union of them.
        if (W[u] % 2 == 0 && W[v] % 2 == 0)
            Union(u, v);
    }
}

// Function to find maximum
// size of DSU tree
function findMax(n, W)
{
    let maxi = 0;
    for(let i = 1; i < n; i++)
        if (W[i] % 2 == 0)
            maxi = Math.max(maxi, sz[i]);

    return maxi;
}

// Driver code

/*
Nodes are 0-indexed in this code
So we have to make necessary changes
while taking inputs
*/

// Weights of nodes
let W = [ 1, 2, 6, 4, 2, 0, 3 ];

// Number of nodes in a tree
let n = W.length;

// Initializing every node as
// a tree with single node.
for(let i = 0; i < n; i++)
{
    id[i] = i;
    sz[i] = 1;
}

let e = [ [ 1, 2 ], [ 1, 3 ],
          [ 2, 4 ], [ 2, 5 ],
          [ 4, 6 ], [ 6, 7 ] ];
let q = e.length;

UnionUtil(e, W, q);

// Find maximum size of DSU tree.
let maxi = findMax(n, W);

document.write("Maximum size of the subtree with ");
document.write("even weighted nodes = " + maxi);

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
Maximum size of the subtree with even weighted nodes = 4
```