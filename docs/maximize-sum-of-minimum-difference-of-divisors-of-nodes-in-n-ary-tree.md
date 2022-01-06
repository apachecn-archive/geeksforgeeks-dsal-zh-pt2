# 最大化 N 元树中节点除数的最小差之和

> 原文:[https://www . geeksforgeeks . org/n 元树中节点除数的最大和最小差/](https://www.geeksforgeeks.org/maximize-sum-of-minimum-difference-of-divisors-of-nodes-in-n-ary-tree/)

给定一个具有特定权重节点的 [n 元](https://www.geeksforgeeks.org/generic-treesn-array-trees/)树，我们的任务是找出从根到叶的每个节点的除数的最小差的最大和。

**示例:**

> **输入:**
> 
> ```
>               18
>              /  \
>             7    15
>           /  \     \
>          4   12     2
>              /
>             9
> ```
> 
> **输出:** 10
> **说明:**
> 最大和沿着路径**18->7->12->9**
> 18 的除数之间的最小差= 6–3 = 3
> 7 的除数之间的最小差= 7–1 = 6
> 12 的除数之间的最小差= 4–3 = 1
> 9 的除数之间的最小差= 3–3 = 0
> 
> **输入:**
> 
> ```
>            20
>           /  \
>          13   14
>         /  \    \
>        10   8   26
>       /
>      25 
> ```
> 
> **输出:** 17
> **说明:**
> 最大和是沿着路径 **20 - > 14 - > 26**

**方法:**
为了解决上面提到的问题，我们可以使用[深度优先遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)在数组中的每个节点存储**因子**之间的**最小**差。现在，任务是找出除数之间的最小差异。

*   我们可以观察到，对于任意一个数 N，在 **[√N，N]** 范围内的最小除数 **x** 在 **x** 和 **N/x** 之间的差值最小。
*   在每个节点，计算除数之间的最小差，最后开始使用**子级**的结果填充数组，并计算**最大值**可能的和。

下面是上述方法的实现:

## C++

```
// C++ program to maximize the sum of
// minimum difference of divisors
// of nodes in an n-ary tree

#include <bits/stdc++.h>
using namespace std;

// Array to store the
// result at each node
int sub[100005];

// Function to get minimum difference
// between the divisors of a number
int minDivisorDifference(int n)
{
    int num1;
    int num2;

    // Iterate from square
    // root of N to N
    for (int i = sqrt(n); i <= n; i++) {
        if (n % i == 0) {
            num1 = i;
            num2 = n / i;
            break;
        }
    }
    // return absolute difference
    return abs(num1 - num2);
}

// DFS function to calculate the maximum sum
int dfs(vector<int> g[], int u, int par)
{

    // Store the min difference
    sub[u] = minDivisorDifference(u);

    int mx = 0;
    for (auto c : g[u]) {
        if (c != par) {
            int ans = dfs(g, c, u);
            mx = max(mx, ans);
        }
    }
    // Add the maximum of
    // all children to sub[u]
    sub[u] += mx;

    // Return maximum sum of
    // node 'u' to its parent
    return sub[u];
}

// Driver code
int main()
{

    vector<int> g[100005];

    int edges = 6;

    g[18].push_back(7);
    g[7].push_back(18);

    g[18].push_back(15);
    g[15].push_back(18);

    g[15].push_back(2);
    g[2].push_back(15);

    g[7].push_back(4);
    g[4].push_back(7);

    g[7].push_back(12);
    g[12].push_back(7);

    g[12].push_back(9);
    g[9].push_back(12);

    int root = 18;

    cout << dfs(g, root, -1);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to maximize the sum of
// minimum difference of divisors
// of nodes in an n-ary tree
import java.util.Vector;
class GFG{

// Array to store the
// result at each node
static int []sub = new int[100005];

// Function to get minimum difference
// between the divisors of a number
static int minDivisorDifference(int n)
{
  int num1 = 0;
  int num2 = 0;

  // Iterate from square
  // root of N to N
  for (int i = (int) Math.sqrt(n);
           i <= n; i++)
  {
    if (n % i == 0)
    {
      num1 = i;
      num2 = n / i;
      break;
    }
  }
  // return absolute difference
  return Math.abs(num1 - num2);
}

// DFS function to calculate
// the maximum sum
static int dfs(Vector<Integer> g[],
               int u, int par)
{
  // Store the min difference
  sub[u] = minDivisorDifference(u);

  int mx = 0;
  for (int c : g[u])
  {
    if (c != par)
    {
      int ans = dfs(g, c, u);
      mx = Math.max(mx, ans);
    }
  }

  // Add the maximum of
  // all children to sub[u]
  sub[u] += mx;

  // Return maximum sum of
  // node 'u' to its parent
  return sub[u];
}

// Driver code
public static void main(String[] args)
{
  @SuppressWarnings("unchecked")
  Vector<Integer> []g =
         new Vector[100005];

  for (int i = 0; i < g.length; i++)
    g[i] = new Vector<Integer>();

  int edges = 6;

  g[18].add(7);
  g[7].add(18);

  g[18].add(15);
  g[15].add(18);

  g[15].add(2);
  g[2].add(15);

  g[7].add(4);
  g[4].add(7);

  g[7].add(12);
  g[12].add(7);

  g[12].add(9);
  g[9].add(12);

  int root = 18;
  System.out.print(dfs(g, root, -1));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to maximize the sum
# of minimum difference of divisors
# of nodes in an n-ary tree
import math

# Array to store the
# result at each node
sub = [0 for i in range(100005)]

# Function to get minimum difference
# between the divisors of a number
def minDivisorDifference(n):

    num1 = 0
    num2 = 0

    # Iterate from square
    # root of N to N
    for i in range(int(math.sqrt(n)), n + 1):
        if (n % i == 0):
            num1 = i
            num2 = n // i
            break

    # Return absolute difference
    return abs(num1 - num2)

# DFS function to calculate the maximum sum
def dfs(g, u, par):

    # Store the min difference
    sub[u] = minDivisorDifference(u)

    mx = 0

    for c in g[u]:
        if (c != par):
            ans = dfs(g, c, u)
            mx = max(mx, ans)

    # Add the maximum of
    # all children to sub[u]
    sub[u] += mx

    # Return maximum sum of
    # node 'u' to its parent
    return sub[u]

# Driver code
if __name__=='__main__':

    g = [[] for i in range(100005)]

    edges = 6

    g[18].append(7)
    g[7].append(18)

    g[18].append(15)
    g[15].append(18)

    g[15].append(2)
    g[2].append(15)

    g[7].append(4)
    g[4].append(7)

    g[7].append(12)
    g[12].append(7)

    g[12].append(9)
    g[9].append(12)

    root = 18

    print(dfs(g, root, -1))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to maximize the sum of
// minimum difference of divisors
// of nodes in an n-ary tree
using System;
using System.Collections.Generic;
class GFG{

// Array to store the
// result at each node
static int []sub = new int[100005];

// Function to get minimum difference
// between the divisors of a number
static int minDivisorDifference(int n)
{
  int num1 = 0;
  int num2 = 0;

  // Iterate from square
  // root of N to N
  for (int i = (int) Math.Sqrt(n);
           i <= n; i++)
  {
    if (n % i == 0)
    {
      num1 = i;
      num2 = n / i;
      break;
    }
  }

  // return absolute difference
  return Math.Abs(num1 - num2);
}

// DFS function to calculate
// the maximum sum
static int dfs(List<int> []g,
               int u, int par)
{
  // Store the min difference
  sub[u] = minDivisorDifference(u);

  int mx = 0;
  foreach (int c in g[u])
  {
    if (c != par)
    {
      int ans = dfs(g, c, u);
      mx = Math.Max(mx, ans);
    }
  }

  // Add the maximum of
  // all children to sub[u]
  sub[u] += mx;

  // Return maximum sum of
  // node 'u' to its parent
  return sub[u];
}

// Driver code
public static void Main(String[] args)
{
  List<int> []g =
       new List<int>[100005];

  for (int i = 0; i < g.Length; i++)
    g[i] = new List<int>();

  int edges = 6;

  g[18].Add(7);
  g[7].Add(18);

  g[18].Add(15);
  g[15].Add(18);

  g[15].Add(2);
  g[2].Add(15);

  g[7].Add(4);
  g[4].Add(7);

  g[7].Add(12);
  g[12].Add(7);

  g[12].Add(9);
  g[9].Add(12);

  int root = 18;
  Console.Write(dfs(g, root, -1));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to maximize the sum of
    // minimum difference of divisors

    // Array to store the
    // result at each node
    let sub = new Array(100005);
    sub.fill(0);

    // Function to get minimum difference
    // between the divisors of a number
    function minDivisorDifference(n)
    {
      let num1 = 0;
      let num2 = 0;

      // Iterate from square
      // root of N to N
      for (let i = parseInt(Math.sqrt(n), 10); i <= n; i++)
      {
        if (n % i == 0)
        {
          num1 = i;
          num2 = parseInt(n / i, 10);
          break;
        }
      }
      // return absolute difference
      return Math.abs(num1 - num2);
    }

    // DFS function to calculate
    // the maximum sum
    function dfs(g, u, par)
    {
      // Store the min difference
      sub[u] = minDivisorDifference(u);

      let mx = 0;
      for (let c = 0; c < g[u].length; c++)
      {
        if (g[u] != par)
        {
          let ans = dfs(g, g[u], u);
          mx = Math.max(mx, ans);
        }
      }

      // Add the maximum of
      // all children to sub[u]
      sub[u] += mx;

      // Return maximum sum of
      // node 'u' to its parent
      return sub[u];
    }

    let g = new Array(100005);

    for (let i = 0; i < g.length; i++)
      g[i] = [];

    let edges = 6;

    g[18].push(7);
    g[7].push(18);

    g[18].push(15);
    g[15].push(18);

    g[15].push(2);
    g[2].push(15);

    g[7].push(4);
    g[4].push(7);

    g[7].push(12);
    g[12].push(7);

    g[12].push(9);
    g[9].push(12);

    let root = 18;
    document.write(dfs(g, root, -1));

    // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
10
```