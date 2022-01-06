# 求偶距节点对的计数

> 原文:[https://www . geesforgeks . org/find-偶数距离节点对计数/](https://www.geeksforgeeks.org/find-count-of-pair-of-nodes-at-even-distance/)

给定一个有 **N 个**节点和 **N-1 条边**的连通非循环图，找出彼此距离相等的一对节点。

**示例:**

```
Input:
3
1 2 
2 3
Output: 1
Explanation:
    1
   /
  2
 /
3
Input:
5
1 2
2 3
1 4
4 5
Output: 4
```

**进场:**

*   假设一个图有 6 个级别(0 到 5)，级别 0、2、4 处于偶数距离，但是级别 1、3、5 也处于偶数距离，因为它们的差是 2，这是偶数，所以我们必须考虑这两个条件，即计算偶数和奇数级别。
*   给定的问题可以通过执行 dfs 遍历来解决
*   选择任意源节点作为根，执行 dfs 遍历，并维护已访问的
    数组，以执行 dfs 和 dist 数组，从而计算到根的距离
*   现在遍历距离数组，记录偶数级和奇数级
*   计算总数为((偶数计数*(偶数计数-1)) +(奇数计数*(奇数计数-1))/2

下面是上述方法的实现:

## C++

```
// C++ program to find
// the count of nodes
// at even distance
#include <bits/stdc++.h>
using namespace std;

// Dfs function to find count of nodes at
// even distance
void dfs(vector<int> graph[], int node, int dist[],
                                    bool vis[], int c)
{
    if (vis[node]) {
        return;
    }
    // Set flag as true for current
    // node in visited array
    vis[node] = true;

    // Insert the distance in
    // dist array for current
    // visited node u
    dist[node] = c;

    for (int i = 0; i < graph[node].size(); i++) {
        // If its neighbours are not vis,
        // run dfs for them
        if (!vis[graph[node][i]]) {
            dfs(graph, graph[node][i], dist, vis, c + 1);
        }
    }
}

int countOfNodes(vector<int> graph[], int n)
{
    // bool array to
    // mark visited nodes
    bool vis[n + 1] = { false };

    // Integer array to
    // compute distance
    int dist[n + 1] = { 0 };

    dfs(graph, 1, dist, vis, 0);

    int even = 0, odd = 0;

    // Traverse the distance array
    // and count the even and odd levels
    for (int i = 1; i <= n; i++) {
        if (dist[i] % 2 == 0) {
            even++;
        }
        else {
            odd++;
        }
    }

    int ans = ((even * (even - 1)) + (odd * (odd - 1))) / 2;

    return ans;
}

// Driver code
int main()
{

    int n = 5;
    vector<int> graph[n + 1] = { {},
                                 { 2 },
                                 { 1, 3 },
                                 { 2 } };

    int ans = countOfNodes(graph, n);
    cout << ans << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of
// nodes at even distance
import java.util.*;

class GFG
{

// Dfs function to find count of nodes at
// even distance
static void dfs(Vector<Integer> graph[],
                   int node, int dist[],
                   boolean vis[], int c)
{
    if (vis[node])
    {
        return;
    }

    // Set flag as true for current
    // node in visited array
    vis[node] = true;

    // Insert the distance in
    // dist array for current
    // visited node u
    dist[node] = c;

    for (int i = 0; i < graph[node].size(); i++)
    {
        // If its neighbours are not vis,
        // run dfs for them
        if (!vis[graph[node].get(i)])
        {
            dfs(graph, graph[node].get(i),
                        dist, vis, c + 1);
        }
    }
}

static int countOfNodes(Vector<Integer> graph[],
                                         int n)
{
    // bool array to
    // mark visited nodes
    boolean []vis = new boolean[n + 1];

    // Integer array to
    // compute distance
    int []dist = new int[n + 1];

    dfs(graph, 1, dist, vis, 0);

    int even = 0, odd = 0;

    // Traverse the distance array
    // and count the even and odd levels
    for (int i = 1; i <= n; i++)
    {
        if (dist[i] % 2 == 0)
        {
            even++;
        }
        else
        {
            odd++;
        }
    }
    int ans = ((even * (even - 1)) +
                (odd * (odd - 1))) / 2;

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int n = 5;
    Vector<Integer> []graph = new Vector[n + 1];
    for(int i = 0; i< n + 1; i++)
    {
        graph[i] = new Vector<Integer>();
    }

    graph[0] = new Vector<Integer>();
    graph[1] = new Vector(Arrays.asList(2));
    graph[2] = new Vector<Integer>(1, 3);
    graph[3] = new Vector<Integer>(2);
    int ans = countOfNodes(graph, n);
    System.out.println(ans);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find
# the count of nodes
# at even distance

# Dfs function to find count of
# nodes at even distance
def dfs(graph, node, dist, vis, c) :

    if (vis[node]) :
        return;

    # Set flag as true for current
    # node in visited array
    vis[node] = True;

    # Insert the distance in
    # dist array for current
    # visited node u
    dist[node] = c;

    for i in range(len(graph[node])) :
        # If its neighbours are not vis,
        # run dfs for them
        if (not vis[graph[node][i]]) :
            dfs(graph, graph[node][i],
                    dist, vis, c + 1);

def countOfNodes(graph, n) :

    # bool array to
    # mark visited nodes
    vis = [False] * (n + 1);

    # Integer array to
    # compute distance
    dist = [0] * (n + 1);

    dfs(graph, 1, dist, vis, 0);

    even = 0; odd = 0;

    # Traverse the distance array
    # and count the even and odd levels
    for i in range(1, n + 1) :
        if (dist[i] % 2 == 0) :
            even += 1;

        else :
            odd += 1;

    ans = ((even * (even - 1)) +
            (odd * (odd - 1))) // 2;

    return ans;

# Driver code
if __name__ == "__main__" :

    n = 5;
    graph = [[], [ 2 ], [ 1, 3 ], [ 2 ]];

    ans = countOfNodes(graph, n);
    print(ans);

# This code is contributed by kanugargng
```

## C#

```
// C# program to find the count of
// nodes at even distance
using System;
using System.Collections.Generic;

class GFG
{

// Dfs function to find count of
// nodes at even distance
static void dfs(List<int> []graph,
                int node, int []dist,
                bool []vis, int c)
{
    if (vis[node])
    {
        return;
    }

    // Set flag as true for current
    // node in visited array
    vis[node] = true;

    // Insert the distance in
    // dist array for current
    // visited node u
    dist[node] = c;

    for (int i = 0; i < graph[node].Count; i++)
    {
        // If its neighbours are not vis,
        // run dfs for them
        if (!vis[graph[node][i]])
        {
            dfs(graph, graph[node][i],
                    dist, vis, c + 1);
        }
    }
}

static int countOfNodes(List<int> []graph,
                                    int n)
{
    // bool array to
    // mark visited nodes
    bool []vis = new bool[n + 1];

    // int array to
    // compute distance
    int []dist = new int[n + 1];

    dfs(graph, 1, dist, vis, 0);

    int even = 0, odd = 0;

    // Traverse the distance array
    // and count the even and odd levels
    for (int i = 1; i <= n; i++)
    {
        if (dist[i] % 2 == 0)
        {
            even++;
        }
        else
        {
            odd++;
        }
    }
    int ans = ((even * (even - 1)) +
                (odd * (odd - 1))) / 2;

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int n = 5;
    List<int> []graph = new List<int>[n + 1];
    for(int i = 0; i< n + 1; i++)
    {
        graph[i] = new List<int>();
    }

    graph[0] = new List<int>{};
    graph[1] = new List<int>{2};
    graph[2] = new List<int>{1, 3};
    graph[3] = new List<int>{2};
    int ans = countOfNodes(graph, n);
    Console.WriteLine(ans);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to find the count of
// nodes at even distance

// Dfs function to find count of
// nodes at even distance
function dfs(graph, node, dist, vis, c)
{
    if (vis[node])
    {
        return;
    }

    // Set flag as true for current
    // node in visited array
    vis[node] = true;

    // Insert the distance in
    // dist array for current
    // visited node u
    dist[node] = c;

    for (var i = 0; i < graph[node].length; i++)
    {
        // If its neighbours are not vis,
        // run dfs for them
        if (!vis[graph[node][i]])
        {
            dfs(graph, graph[node][i],
                    dist, vis, c + 1);
        }
    }
}

function countOfNodes(graph, n)
{
    // bool array to
    // mark visited nodes
    var vis = Array(n+1).fill(false);

    // int array to
    // compute distance
    var dist = Array(n+1).fill(0);

    dfs(graph, 1, dist, vis, 0);

    var even = 0, odd = 0;

    // Traverse the distance array
    // and count the even and odd levels
    for (var i = 1; i <= n; i++)
    {
        if (dist[i] % 2 == 0)
        {
            even++;
        }
        else
        {
            odd++;
        }
    }
    var ans = ((even * (even - 1)) +
                (odd * (odd - 1))) / 2;

    return ans;
}

// Driver code
var n = 5;
var graph = Array.from(Array(n+1), ()=>Array());

graph[1] = [2];
graph[2] = [1, 3];
graph[3] = [2];
var ans = countOfNodes(graph, n);
document.write(ans);

</script>
```

**输出:**

```
6
```

**时间复杂度:** O(V+E)