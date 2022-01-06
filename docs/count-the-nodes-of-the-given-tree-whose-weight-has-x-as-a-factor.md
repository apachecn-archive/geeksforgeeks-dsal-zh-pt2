# 计算权重为 X 的给定树的节点数

> 原文:[https://www . geeksforgeeks . org/计算给定树的节点数，该树的权重以 x 为因子/](https://www.geeksforgeeks.org/count-the-nodes-of-the-given-tree-whose-weight-has-x-as-a-factor/)

给定一棵树，以及所有节点的权重，任务是统计权重可被 **x** 整除的节点。
**例:**

> **输入:**
> 
> ![](img/c8d63a5a618701e1de407d9028376d6b.png)
> 
> x = 5
> **输出:** 2
> 只有节点 1 和节点 2 的权重可以被 5 整除。

**方法:**在树上执行 [dfs](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，对于每个节点，检查它的权重是否能被 x 整除。如果是，则增加计数。
**实施:**

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

long ans = 0;
int x;
vector<int> graph[100];
vector<int> weight(100);

// Function to perform dfs
void dfs(int node, int parent)
{

    // If weight of the current node
    // is divisible by x
    if (weight[node] % x == 0)
        ans += 1;

    for (int to : graph[node]) {
        if (to == parent)
            continue;
        dfs(to, node);
    }
}

// Driver code
int main()
{
    x = 5;

    // Weights of the node
    weight[1] = 5;
    weight[2] = 10;
    weight[3] = 11;
    weight[4] = 8;
    weight[5] = 6;

    // Edges of the tree
    graph[1].push_back(2);
    graph[2].push_back(3);
    graph[2].push_back(4);
    graph[1].push_back(5);

    dfs(1, 1);

    cout << ans;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static long ans = 0;
static int x;
static Vector<Vector<Integer>> graph=new Vector<Vector<Integer>>();
static Vector<Integer> weight=new Vector<Integer>();

// Function to perform dfs
static void dfs(int node, int parent)
{

    // If weight of the current node
    // is divisible by x
    if (weight.get(node) % x == 0)
        ans += 1;

    for (int i = 0; i < graph.get(node).size(); i++)
    {
        if (graph.get(node).get(i) == parent)
            continue;
        dfs(graph.get(node).get(i), node);
    }
}

// Driver code
public static void main(String args[])
{
    x = 5;

    // Weights of the node
    weight.add(0);
    weight.add(5);
    weight.add(10);;
    weight.add(11);;
    weight.add(8);
    weight.add(6);

    for(int i = 0; i < 100; i++)
    graph.add(new Vector<Integer>());

    // Edges of the tree
    graph.get(1).add(2);
    graph.get(2).add(3);
    graph.get(2).add(4);
    graph.get(1).add(5);

    dfs(1, 1);

    System.out.println(ans);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
ans = 0

graph = [[] for i in range(100)]
weight = [0] * 100

# Function to perform dfs
def dfs(node, parent):
    global ans,x

    # If weight of the current node
    # is divisible by x
    if (weight[node] % x == 0):
        ans += 1
    for to in graph[node]:
        if (to == parent):
            continue
        dfs(to, node)

# Driver code
x = 5

# Weights of the node
weight[1] = 5
weight[2] = 10
weight[3] = 11
weight[4] = 8
weight[5] = 6

# Edges of the tree
graph[1].append(2)
graph[2].append(3)
graph[2].append(4)
graph[1].append(5)

dfs(1, 1)
print(ans)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

static long ans = 0;
static int x;
static List<List<int>> graph = new List<List<int>>();
static List<int> weight = new List<int>();

// Function to perform dfs
static void dfs(int node, int parent)
{

    // If weight of the current node
    // is divisible by x
    if (weight[node] % x == 0)
        ans += 1;

    for (int i = 0; i < graph[node].Count; i++)
    {
        if (graph[node][i] == parent)
            continue;
        dfs(graph[node][i], node);
    }
}

// Driver code
public static void Main(String []args)
{
    x = 5;

    // Weights of the node
    weight.Add(0);
    weight.Add(5);
    weight.Add(10);;
    weight.Add(11);;
    weight.Add(8);
    weight.Add(6);

    for(int i = 0; i < 100; i++)
    graph.Add(new List<int>());

    // Edges of the tree
    graph[1].Add(2);
    graph[2].Add(3);
    graph[2].Add(4);
    graph[1].Add(5);

    dfs(1, 1);

    Console.WriteLine(ans);
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

let ans = 0;
let x;

let graph = new Array(100);
let weight = new Array(100);
for(let i = 0; i < 100; i++)
{
    graph[i] = [];
    weight[i] = 0;
}

// Function to perform dfs
function dfs(node, parent)
{
    // If weight of the current node
    // is divisible by x
    if (weight[node] % x == 0)
        ans += 1;

    for(let to=0;to<graph[node].length;to++) {
        if(graph[node][to] == parent)
            continue
        dfs(graph[node][to], node); 
    }
}

// Driver code
    x = 5;

    // Weights of the node
    weight[1] = 5;
    weight[2] = 10;
    weight[3] = 11;
    weight[4] = 8;
    weight[5] = 6;

    // Edges of the tree
    graph[1].push(2);
    graph[2].push(3);
    graph[2].push(4);
    graph[1].push(5);

    dfs(1, 1);

    document.write(ans);

    // This code is contributed by Dharanendra L V.

</script>
```

**Output:** 

```
2
```

**复杂度分析:**

*   **时间复杂度:** O(N)。
    在 DFS 中，树的每个节点都被处理一次，因此当树中总共有 N 个节点时，由于 DFS 而导致的复杂性是 O(N)。因此，时间复杂度为 O(N)。
*   **辅助空间:** O(1)。
    不需要任何额外的空间，所以空间复杂度不变。