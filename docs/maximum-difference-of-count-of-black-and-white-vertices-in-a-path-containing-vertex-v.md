# 包含顶点 V 的路径中黑白顶点数的最大差值

> 原文:[https://www . geesforgeks . org/包含顶点的路径中黑白顶点的最大计数差 v/](https://www.geeksforgeeks.org/maximum-difference-of-count-of-black-and-white-vertices-in-a-path-containing-vertex-v/)

给定一棵具有 **N** 个顶点和**N–1**条边的树，其中顶点从 **0 到 N–1**进行编号，并且树中存在一个顶点 **V** 。给定树中的每个顶点分配了一种颜色**白色或黑色**，并且顶点的相应颜色由数组**arr【】**表示。任务是从包含给定顶点 **V** 的给定树的任何可能的子树中找到白色顶点的数量和黑色顶点的数量之间的最大差异。

**例:**

```
Input: V = 0,
arr[] = {'b', 'w', 'w', 'w', 'b',
         'b', 'b', 'b', 'w'}
Tree:
           0 b
         /   \
       /       \
     1 w        2 w
    /          / \
   /          /   \
  5 b      w 3     4 b
  |          |     |
  |          |     |
  7 b      b 6     8 w
Output: 2
Explanation:
We can take the subtree
containing the vertex 0 
which contains vertices
0, 1, 2, 3 such that 
the difference between
the number of white 
and the number of black vertices
is maximum which is equal to 2.

Input:
V = 2,
arr[] = {'b', 'b', 'w', 'b'}
Tree:
        0 b
     /  |  \
    /   |   \
   1    2    3
   b    w     b
Output: 1 
```

**方法:**思路是用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的概念来解决这个问题。

*   First, make a vector for the color array and white, push 1, black, and push -1.
*   Make an array dp[] to calculate the maximum possible difference between the number of white and black vertices in a subtree containing vertex V.
*   Now, use [depth-first search](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) to traverse the traversal tree and update the values in the dp[] array.
*   Finally, the minimum value in the dp[] array is the required answer.

下面是上述方法的实现:

## c++

```
// C++ program to find maximum
// difference between count of
// black and white vertices in
// a path containing vertex V

#include <bits/stdc++.h>
using namespace std;

// Defining the tree class
class tree {
    vector<int> dp;
    vector<vector<int> > g;
    vector<int> c;

public:
    // Constructor
    tree(int n)
    {
        dp = vector<int>(n);
        g = vector<vector<int> >(n);
        c = vector<int>(n);
    }

    // Function for adding edges
    void addEdge(int u, int v)
    {
        g[u].push_back(v);
        g[v].push_back(u);
    }

    // Function to perform DFS
    // on the given tree
    void dfs(int v, int p = -1)
    {
        dp[v] = c[v];

        for (auto i : g[v]) {
            if (i == p)
                continue;

            dfs(i, v);

            // Returning calculated maximum
            // difference between white
            // and black for current vertex
            dp[v] += max(0, dp[i]);
        }
    }

    // Function that prints the
    // maximum difference between
    // white and black vertices
    void maximumDifference(int v,
                           char color[],
                           int n)
    {
        for (int i = 0; i < n; i++) {

            // Condition for white vertex
            if (color[i] == 'w')
                c[i] = 1;

            // Condition for black vertex
            else
                c[i] = -1;
        }

        // Calling dfs function for vertex v
        dfs(v);

        // Printing maximum difference between
        // white and black vertices
        cout << dp[v] << "\n";
    }
};

// Driver code
int main()
{
    tree t(9);

    t.addEdge(0, 1);
    t.addEdge(0, 2);
    t.addEdge(2, 3);
    t.addEdge(2, 4);
    t.addEdge(1, 5);
    t.addEdge(3, 6);
    t.addEdge(5, 7);
    t.addEdge(4, 8);

    int V = 0;

    char color[] = { 'b', 'w', 'w',
                     'w', 'b', 'b',
                     'b', 'b', 'w' };

    t.maximumDifference(V, color, 9);

    return 0;
}
```

## Java

```
// Java program to find maximum
// difference between count of
// black and white vertices in
// a path containing vertex V
import java.util.*;

// Defining the
// tree class
class GFG{

static int []dp;
static Vector<Integer> []g;
static int[] c;

// Constructor
GFG(int n)
{
  dp = new int[n];
  g =  new Vector[n];

  for (int i = 0; i < g.length; i++)
    g[i] = new Vector<Integer>();

  c = new int[n];
}

// Function for adding edges
void addEdge(int u, int v)
{
  g[u].add(v);
  g[v].add(u);
}

// Function to perform DFS
// on the given tree
static void dfs(int v, int p)
{
  dp[v] = c[v];

  for (int i : g[v])
  {
    if (i == p)
      continue;

    dfs(i, v);

    // Returning calculated maximum
    // difference between white
    // and black for current vertex
    dp[v] += Math.max(0, dp[i]);
  }
}

// Function that prints the
// maximum difference between
// white and black vertices
void maximumDifference(int v,
                       char color[],
                       int n)
{
  for (int i = 0; i < n; i++)
  {
    // Condition for
    // white vertex
    if (color[i] == 'w')
      c[i] = 1;

    // Condition for
    // black vertex
    else
      c[i] = -1;
  }

  // Calling dfs function
  // for vertex v
  dfs(v, -1);

  // Printing maximum difference
  // between white and black vertices
  System.out.print(dp[v] + "\n");
}

// Driver code
public static void main(String[] args)
{
  GFG t = new GFG(9);

  t.addEdge(0, 1);
  t.addEdge(0, 2);
  t.addEdge(2, 3);
  t.addEdge(2, 4);
  t.addEdge(1, 5);
  t.addEdge(3, 6);
  t.addEdge(5, 7);
  t.addEdge(4, 8);

  int V = 0;

  char color[] = {'b', 'w', 'w',
                  'w', 'b', 'b',
                  'b', 'b', 'w'};
  t.maximumDifference(V, color, 9);
}
}

// This code is contributed by 29AjayKumar
```

## python 3

```
# Python3 program to find maximum
# difference between count of
# black and white vertices in
# a path containing vertex V

# Function for adding edges
def addEdge(g, u, v):

    g[u].append(v)
    g[v].append(u)

# Function to perform DFS
# on the given tree
def dfs(v, p, dp, c, g):

    dp[v] = c[v]

    for i in g[v]:
        if i == p:
            continue

        dfs(i, v, dp, c, g)

        # Returning calculated maximum
        # difference between white
        # and black for current vertex
        dp[v] += max(0, dp[i])

# Function that prints the
# maximum difference between
# white and black vertices
def maximumDifference(v, color, n, dp, c, g):

    for i in range(n):

        # Condition for white vertex
        if(color[i] == 'w'):
            c[i] = 1

        # Condition for black vertex
        else:
            c[i] = -1

    # Calling dfs function for vertex v
    dfs(v, -1, dp, c, g)

    # Printing maximum difference between
    # white and black vertices
    print(dp[v])

# Driver code
n = 9
g = {}
dp = [0] * n
c = [0] * n

for i in range(0, n + 1):
    g[i] = []

addEdge(g, 0, 1)
addEdge(g, 0, 2)
addEdge(g, 2, 2)
addEdge(g, 2, 4)
addEdge(g, 1, 5)
addEdge(g, 3, 6)
addEdge(g, 5, 7)
addEdge(g, 4, 8)

V = 0

color = [ 'b', 'w', 'w',
          'w', 'b', 'b',
          'b', 'b', 'w' ]

maximumDifference(V, color, 9, dp, c, g)

# This code is contributed by avanitrachhadiya2155
```

## c#

```
// C# program to find maximum
// difference between count of
// black and white vertices in
// a path containing vertex V
using System;
using System.Collections.Generic;

// Defining the
// tree class
class GFG{

static int []dp;
static List<int> []g;
static int[] c;

// Constructor
GFG(int n)
{
  dp = new int[n];
  g = new List<int>[n];

  for (int i = 0; i < g.Length; i++)
    g[i] = new List<int>();

  c = new int[n];
}

// Function for adding edges
void addEdge(int u, int v)
{
  g[u].Add(v);
  g[v].Add(u);
}

// Function to perform DFS
// on the given tree
static void dfs(int v, int p)
{
  dp[v] = c[v];

  foreach (int i in g[v])
  {
    if (i == p)
      continue;

    dfs(i, v);

    // Returning calculated maximum
    // difference between white
    // and black for current vertex
    dp[v] += Math.Max(0, dp[i]);
  }
}

// Function that prints the
// maximum difference between
// white and black vertices
void maximumDifference(int v,
                       char []color,
                       int n)
{
  for (int i = 0; i < n; i++)
  {
    // Condition for
    // white vertex
    if (color[i] == 'w')
      c[i] = 1;

    // Condition for
    // black vertex
    else
      c[i] = -1;
  }

  // Calling dfs function
  // for vertex v
  dfs(v, -1);

  // Printing maximum difference
  // between white and black vertices
  Console.Write(dp[v] + "\n");
}

// Driver code
public static void Main(String[] args)
{
  GFG t = new GFG(9);

  t.addEdge(0, 1);
  t.addEdge(0, 2);
  t.addEdge(2, 3);
  t.addEdge(2, 4);
  t.addEdge(1, 5);
  t.addEdge(3, 6);
  t.addEdge(5, 7);
  t.addEdge(4, 8);

  int V = 0;

  char []color = {'b', 'w', 'w',
                  'w', 'b', 'b',
                  'b', 'b', 'w'};
  t.maximumDifference(V, color, 9);
}
}

// This code is contributed by Rajput-Ji
```

## Javascript

```
<script>
    // Javascript program to find maximum
    // difference between count of
    // black and white vertices in
    // a path containing vertex V
    let n = 9;
    let dp = new Array(n);
    let g = new Array(n);
    let c = new Array(n);

    for (let i = 0; i < g.length; i++)
        g[i] = [];

      // Function for adding edges
    function addEdge(u, v)
    {
      g[u].push(v);
      g[v].push(u);
    }

    // Function to perform DFS
    // on the given tree
    function dfs(v, p)
    {
      dp[v] = c[v];

      for (let i = 0; i < g[v].length; i++)
      {
        if (g[v][i] == p)
          continue;

        dfs(g[v][i], v);

        // Returning calculated maximum
        // difference between white
        // and black for current vertex
        dp[v] += Math.max(0, dp[g[v][i]]);
      }
    }

    // Function that prints the
    // maximum difference between
    // white and black vertices
    function maximumDifference(v, color, n)
    {
      for (let i = 0; i < n; i++)
      {

        // Condition for
        // white vertex
        if (color[i] == 'w')
          c[i] = 1;

        // Condition for
        // black vertex
        else
          c[i] = -1;
      }

      // Calling dfs function
      // for vertex v
      dfs(v, -1);

      // Printing maximum difference
      // between white and black vertices
      document.write(dp[v] + "</br>");
    }

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(2, 3);
    addEdge(2, 4);
    addEdge(1, 5);
    addEdge(3, 6);
    addEdge(5, 7);
    addEdge(4, 8);

    let V = 0;

    let color = ['b', 'w', 'w',
                    'w', 'b', 'b',
                    'b', 'b', 'w'];
    maximumDifference(V, color, 9);

// This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
2
```

**时间复杂度:** *O(N)* ，其中 N 是树的顶点数。