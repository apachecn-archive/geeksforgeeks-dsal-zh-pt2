# 由至少一条黑色边组成的长度为 K 的节点序列的计数

> 原文:[https://www . geesforgeks . org/由至少一条黑边组成的长度为 k 的节点序列计数/](https://www.geeksforgeeks.org/count-of-node-sequences-of-length-k-consisting-of-at-least-one-black-edge/)

给定一个由从**【1，N】**开始编号的 **N** 节点组成的树，该树被着色为**黑色(用 1 表示)**或**绿色(用 0 表示)**，任务是计算长度为**K**【a<sub>1</sub>，a <sub>2</sub> 的序列数，..a <sub>K</sub> 使得连续节点之间的路径最短，并且覆盖的边至少由一条黑色边组成。由于答案可以很大，打印到 **10 <sup>9</sup> +7** 的模。

> **输入:** N = 4，K = 4
> 1-2 0
> 2-3 0
> 2-4 0
> T6】输出:0
> T9】说明:
> 既然树上没有黑边。没有这样的序列。
> 
> **输入:** N = 3，K = 3
> 1-2 1
> 2-3 1
> **输出:** 24
> **说明:**
> 除了(1，1，1)，(2，2，2)和(3，3，3)以外的所有 3 <sup>3</sup> 序列都包含在答案中。

**方法:**
想法是计算长度为 **K** 的序列的数量，使得没有黑色边缘被覆盖。让计数为**温度**。那么**(N<sup>K</sup>)–temp**就是需要的答案。**温度**可以很容易地通过去除黑边，然后计算结果图的不同分量的大小来计算。

请遵循以下步骤:

1.  将 **ans** 的值初始化为**N<sup>K</sup>T5。**
2.  通过仅添加绿色边来构建图形 **G** 。
3.  执行图的 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)，并继续从**和**中减去**(大小 <sup>K</sup> )** ，其中**大小**是图 g 的不同组件中的节点数

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach
#include <bits/stdc++.h>
#define int long long int
using namespace std;

const int mod = 1e9 + 7;
const int N = 1e5 + 1;

// Vector to store the graph
vector<int> G[N];

// Iterative Function to calculate
// (a<sup>b</sup>) % mod in O(log b)
int power(int a, int b) {

    // Initialize result
    int res = 1;

    // Update x if it is more than
    // or equal to p
    a = a % mod;
    if (a == 0)

      // In case x is divisible by p;
      return 0;

    while (b > 0) {

        // If a is odd,
        // multiply x with result
        if (b & 1)
            res = (res * a) % mod;

        // b must be even now
        b = b >> 1; // b = b/2
        a = (a * a) % mod;
    }
    return res;
}

// DFS traversal of the nodes
void dfs(int i, int& size,
         bool* visited) {

    // Mark the current
    // node as visited
    visited[i] = true;

    // Increment  the size of the
    // current component
    size++;

    // Recur for all the vertices
    // adjacent to this node
    for (auto nbr : G[i]) {
        if (!visited[nbr]) {
          dfs(nbr, size, visited);
        }
    }
}

// Function to calculate the
// final answer
void totalSequences(int& ans,
                    int n, int k)
{
    // Mark all the vertices as
    // not visited initially
    bool visited[n + 1];
    memset(visited, false,
           sizeof(visited));

  // Subtract (size^k) from the answer
  // for different components
    for (int i = 1; i <= n; i++) {
        if (!visited[i]) {
            int size = 0;
            dfs(i, size, visited);
            ans -= power(size, k);
            ans += mod;
            ans = ans % mod;
        }
    }
}

// Function to add edges to the graph
void addEdge(int x, int y, int color)
{
    // If the colour is green,
    // include it in the graph
    if (color == 0) {
        G[x].push_back(y);
        G[y].push_back(x);
    }
}
int32_t main()
{
    // Number of node in the tree
    int n = 3;

    // Size of sequence
    int k = 3;

    // Initialize the result as n^k
    int ans = power(n, k);
    /* 2
     /   \
    1     3

   Let us create binary tree as shown
   in above example */
    addEdge(1, 2, 1);
    addEdge(2, 3, 1);

    totalSequences(ans, n, k);
    cout << ans << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.util.*;

class GFG{

static int mod = (int)(1e9 + 7);
static int N = (int)(1e5 + 1);
static  int size;
static int ans;

// Vector to store the graph
@SuppressWarnings("unchecked")
static Vector<Integer> []G = new Vector[N];

// Iterative Function to calculate
// (a<sup>b</sup>) % mod in O(log b)
static int power(int a, int b)
{

    // Initialize result
    int res = 1;

    // Update x if it is more than
    // or equal to p
    a = a % mod;

    if (a == 0)

        // In case x is divisible by p;
        return 0;

    while (b > 0)
    {

        // If a is odd,
        // multiply x with result
        if (b % 2 == 1)
            res = (res * a) % mod;

        // b must be even now
        b = b >> 1; // b = b/2
        a = (a * a) % mod;
    }
    return res;
}

// DFS traversal of the nodes
static void dfs(int i, boolean []visited)
{

    // Mark the current
    // node as visited
    visited[i] = true;

    // Increment  the size of the
    // current component
    size++;

    // Recur for all the vertices
    // adjacent to this node
    for(int nbr : G[i])
    {
        if (!visited[nbr])
        {
            dfs(nbr, visited);
        }
    }
}

// Function to calculate the
// final answer
static void totalSequences(int n, int k)
{

    // Mark all the vertices as
    // not visited initially
    boolean []visited = new boolean[n + 1];

    // Subtract (size^k) from the answer
    // for different components
    for(int i = 1; i <= n; i++)
    {
        if (!visited[i])
        {
            size = 0;
            dfs(i, visited);
            ans -= power(size, k);
            ans += mod;
            ans = ans % mod;
        }
    }
}

// Function to add edges to the graph
static void addEdge(int x, int y, int color)
{

    // If the colour is green,
    // include it in the graph
    if (color == 0)
    {
        G[x].add(y);
        G[y].add(x);
    }
}

// Driver code
public static void main(String[] args)
{
    for(int i = 0; i < G.length; i++)
        G[i] = new Vector<Integer>();

    // Number of node in the tree
    int n = 3;

    // Size of sequence
    int k = 3;

    // Initialize the result as n^k
    ans = power(n, k);

    /* 2
     /   \
    1     3
    Let us create binary tree as shown
    in above example */
    addEdge(1, 2, 1);
    addEdge(2, 3, 1);

    totalSequences(n, k);
    System.out.print(ans + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach
mod = 1e9 + 7
N = 1e5 + 1

# List to store the graph
G = [0] * int(N)

# Iterative Function to calculate
# (a<sup>b</sup>) % mod in O(log b)
def power(a, b):

    # Initialize result
    res = 1

    # Update x if it is more than
    # or equal to p
    a = a % mod

    if a == 0:

        # In case x is divisible by p;
        return 0

    while b > 0:

        # If a is odd,
        # multiply x with result
        if b & 1:
            res = (res * a) % mod

        # b must be even now
        b = b >> 1 # b = b/2
        a = (a * a) % mod

    return res

# DFS traversal of the nodes
def dfs(i, size, visited):

    # Mark the current
    # node as visited
    visited[i] = True

    # Increment the size of the
    # current component
    size[0] += 1

    # Recur for all the vertices
    # adjacent to this node
    for nbr in range(G[i]):
        if not visited[nbr]:
            dfs(nbr, size, visited)

# Function to calculate the
# final answer
def totalSequences(ans, n, k):

    # Mark all the vertices as
    # not visited initially
    visited = [False] * (n + 1)

    # Subtract (size^k) from the answer
    # for different components
    for i in range(1, n + 1):
        if not visited[i]:
            size = [0]
            dfs(i, size, visited)

            ans[0] -= power(size[0], k)
            ans[0] += mod
            ans[0] = ans[0] % mod

# Function to add edges to the graph
def addEdge(x, y, color):

    # If the colour is green,
    # include it in the graph
    if color == 0:
        G[x].append(y)
        G[y].append(x)

# Driver code
if __name__ == '__main__':

    # Number of node in the tree
    n = 3

    # Size of sequence
    k = 3

    # Initialize the result as n^k
    ans = [power(n, k)]

    """
      2
     / \
    1   3

    Let us create binary tree as shown
    in above example
    """
    addEdge(1, 2, 1)
    addEdge(2, 3, 1)

    totalSequences(ans, n, k)
    print(int(ans[0]))

# This code is contributed by Shivam Singh
```

## C#

```
// C# implementation of the
// above approach
using System;
using System.Collections.Generic;
class GFG{

static int mod = (int)(1e9 + 7);
static int N = (int)(1e5 + 1);
static  int size;
static int ans;

// List to store the graph
static List<int> []G =
       new List<int>[N];

// Iterative Function to
// calculate (a<sup>b</sup>)
// % mod in O(log b)
static int power(int a,
                 int b)
{
  // Initialize result
  int res = 1;

  // Update x if it is
  // more than or equal
  // to p
  a = a % mod;

  if (a == 0)

    // In case x is
    // divisible by p;
    return 0;

  while (b > 0)
  {
    // If a is odd,
    // multiply x
    // with result
    if (b % 2 == 1)
      res = (res * a) % mod;

    // b must be even now
    // b = b/2
    b = b >> 1;

    a = (a * a) % mod;
  }
  return res;
}

// DFS traversal of the nodes
static void dfs(int i,
                bool []visited)
{
  // Mark the current
  // node as visited
  visited[i] = true;

  // Increment  the size of the
  // current component
  size++;

  // Recur for all the vertices
  // adjacent to this node
  foreach(int nbr in G[i])
  {
    if (!visited[nbr])
    {
      dfs(nbr, visited);
    }
  }
}

// Function to calculate the
// readonly answer
static void totalSequences(int n,
                           int k)
{
  // Mark all the vertices as
  // not visited initially
  bool []visited = new bool[n + 1];

  // Subtract (size^k) from the
  // answer for different components
  for(int i = 1; i <= n; i++)
  {
    if (!visited[i])
    {
      size = 0;
      dfs(i, visited);
      ans -= power(size, k);
      ans += mod;
      ans = ans % mod;
    }
  }
}

// Function to add edges
// to the graph
static void addEdge(int x,
                    int y,
                    int color)
{
  // If the colour is green,
  // include it in the graph
  if (color == 0)
  {
    G[x].Add(y);
    G[y].Add(x);
  }
}

// Driver code
public static void Main(String[] args)
{
  for(int i = 0; i < G.Length; i++)
    G[i] = new List<int>();

  // Number of node
  // in the tree
  int n = 3;

  // Size of sequence
  int k = 3;

  // Initialize the
  // result as n^k
  ans = power(n, k);

  /*   2
     /   \
    1     3
    Let us create binary tree
    as shown in above example */
  addEdge(1, 2, 1);
  addEdge(2, 3, 1);

  totalSequences(n, k);
  Console.Write(ans + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    let mod = (1e9 + 7);
    let N = (1e5 + 1);
    let size;
    let ans;

    // List to store the graph
    let G = new Array(N);

    // Iterative Function to
    // calculate (a<sup>b</sup>)
    // % mod in O(log b)
    function power(a, b)
    {
      // Initialize result
      let res = 1;

      // Update x if it is
      // more than or equal
      // to p
      a = a % mod;

      if (a == 0)

        // In case x is
        // divisible by p;
        return 0;

      while (b > 0)
      {
        // If a is odd,
        // multiply x
        // with result
        if (b % 2 == 1)
          res = (res * a) % mod;

        // b must be even now
        // b = b/2
        b = b >> 1;

        a = (a * a) % mod;
      }
      return res;
    }

    // DFS traversal of the nodes
    function dfs(i, visited)
    {
      // Mark the current
      // node as visited
      visited[i] = true;

      // Increment  the size of the
      // current component
      size++;

      // Recur for all the vertices
      // adjacent to this node
      for(let nbr = 0; nbr < G[i].length; nbr++)
      {
        if (!visited[G[i][nbr]])
        {
          dfs(G[i][nbr], visited);
        }
      }
    }

    // Function to calculate the
    // readonly answer
    function totalSequences(n, k)
    {
      // Mark all the vertices as
      // not visited initially
      let visited = new Array(n + 1);
      visited.fill(false);

      // Subtract (size^k) from the
      // answer for different components
      for(let i = 1; i <= n; i++)
      {
        if (!visited[i])
        {
          size = 0;
          dfs(i, visited);
          ans -= power(size, k);
          ans += mod;
          ans = ans % mod;
        }
      }
    }

    // Function to add edges
    // to the graph
    function addEdge(x, y, color)
    {
      // If the colour is green,
      // include it in the graph
      if (color == 0)
      {
        G[x].push(y);
        G[y].push(x);
      }
    }

    for(let i = 0; i < G.length; i++)
        G[i] = [];

    // Number of node
    // in the tree
    let n = 3;

    // Size of sequence
    let k = 3;

    // Initialize the
    // result as n^k
    ans = power(n, k);

    /*   2
           /   \
          1     3
          Let us create binary tree
          as shown in above example */
    addEdge(1, 2, 1);
    addEdge(2, 3, 1);

    totalSequences(n, k);
    document.write(ans + "</br>");

</script>
```

**Output:** 

```
24
```

***时间复杂度:** O(N)，因为 DFS 遍历需要 O(顶点+边)== O(N + (N-1)) == O(N))复杂度。*