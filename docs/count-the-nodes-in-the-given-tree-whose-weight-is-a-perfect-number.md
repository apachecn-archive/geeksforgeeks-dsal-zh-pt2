# 计算给定树中权重为完全数的节点数

> 原文:[https://www . geeksforgeeks . org/计算给定树中的节点数，其权重是一个完美的数字/](https://www.geeksforgeeks.org/count-the-nodes-in-the-given-tree-whose-weight-is-a-perfect-number/)

给定一棵**树**，以及所有节点的**权重**，任务是统计权重为 [**完全数**](https://www.geeksforgeeks.org/perfect-number/) 的节点数量。

> 一个 [**完全数**](https://www.geeksforgeeks.org/perfect-number/) 是一个正整数，等于其[适当因子](https://www.geeksforgeeks.org/sum-of-all-proper-divisors-of-a-natural-number/)之和。

**示例:**

> **输入:**
> 
> ![](img/8f6b999c55f923c56bb2bbe2b7cbea36.png)
> 
> **输出:** 0
> **说明:**
> 不存在权重为完全数的节点。

**方法:**
为了解决这个问题，我们在树上执行[深度优先搜索(DFS)](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 遍历，对于每个节点，[检查其权重是否为完全数](https://www.geeksforgeeks.org/perfect-number/)。每次得到这样的重量，我们就不断地增加计数器。整个树遍历完成后，该计数器的最终值就是答案。
以下是上述方法的实现:

## C++

```
// C++ implementation to Count the nodes in the
// given tree whose weight is a Perfect Number

#include <bits/stdc++.h>
using namespace std;

int ans = 0;
vector<int> graph[100];
vector<int> weight(100);

// Function that returns true if n is perfect
bool isPerfect(long long int n)
{
    // Variable to store sum of divisors
    long long int sum = 1;

    // Find all divisors and add them
    for (long long int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            if (i * i != n)
                sum = sum + i + n / i;
            else
                sum = sum + i;
        }
    }

    // Check if sum of divisors is equal to
    // n, then n is a perfect number
    if (sum == n && n != 1)
        return true;

    return false;
}

// Function to perform dfs
void dfs(int node, int parent)
{

    // If weight of the current node
    // is a perfect number
    if (isPerfect(weight[node]))
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
// Java implementation to Count the nodes in the
// given tree whose weight is a Perfect Number

import java.util.*;

class GFG{

static int ans = 0;
static Vector<Integer> []graph = new Vector[100];
static int []weight = new int[100];

// Function that returns true if n is perfect
static boolean isPerfect(int n)
{
    // Variable to store sum of divisors
    int sum = 1;

    // Find all divisors and add them
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            if (i * i != n)
                sum = sum + i + n / i;
            else
                sum = sum + i;
        }
    }

    // Check if sum of divisors is equal to
    // n, then n is a perfect number
    if (sum == n && n != 1)
        return true;

    return false;
}

// Function to perform dfs
static void dfs(int node, int parent)
{

    // If weight of the current node
    // is a perfect number
    if (isPerfect(weight[node]))
        ans += 1;

    for (int to : graph[node]) {
        if (to == parent)
            continue;
        dfs(to, node);
    }
}

// Driver code
public static void main(String[] args)
{

    for (int i = 0; i < graph.length; i++)
        graph[i] = new Vector<Integer>();

    // Weights of the node
    weight[1] = 5;
    weight[2] = 10;
    weight[3] = 11;
    weight[4] = 8;
    weight[5] = 6;

    // Edges of the tree
    graph[1].add(2);
    graph[2].add(3);
    graph[2].add(4);
    graph[1].add(5);

    dfs(1, 1);
    System.out.print(ans);

}
}

// This code contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation to
# Count the Nodes in the given
# tree whose weight is a Perfect
# Number

graph = [[] for i in range(100)]
weight = [0] * 100
ans = 0

# Function that returns
# True if n is perfect
def isPerfect(n):

    # Variable to store
    # sum of divisors
    sum = 1;

    # Find all divisors
    # and add them
    i = 2;

    while(i * i < n):
        if (n % i == 0):
            if (i * i != n):
                sum = sum + i + n / i;
            else:
                sum = sum + i;
        i += 1;

    # Check if sum of divisors
    # is equal to n, then n is
    # a perfect number
    if (sum == n and n != 1):
        return True;

    return False;

# Function to perform dfs
def dfs(Node, parent):

    # If weight of the current
    # Node is a perfect number
    global ans;

    if (isPerfect(weight[Node])):
        ans += 1;

    for to in graph[Node]:
        if (to == parent):
            continue;
        dfs(to, Node);

# Driver code
# Weights of the Node
weight[1] = 5;
weight[2] = 10;
weight[3] = 11;
weight[4] = 8;
weight[5] = 6;

# Edges of the tree
graph[1].append(2);
graph[2].append(3);
graph[2].append(4);
graph[1].append(5);

dfs(1, 1);
print(ans);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation to count the
// nodes in the given tree whose
// weight is a Perfect Number
using System;
using System.Collections.Generic;

class GFG{

static int ans = 0;
static List<int> []graph = new List<int>[100];
static int []weight = new int[100];

// Function that returns true
// if n is perfect
static bool isPerfect(int n)
{

    // Variable to store sum of
    // divisors
    int sum = 1;

    // Find all divisors and add them
    for(int i = 2; i * i <= n; i++)
    {
       if (n % i == 0)
       {
           if (i * i != n)
               sum = sum + i + n / i;
           else
               sum = sum + i;
       }
    }

    // Check if sum of divisors is equal
    // to n, then n is a perfect number
    if (sum == n && n != 1)
        return true;
    return false;
}

// Function to perform dfs
static void dfs(int node, int parent)
{

    // If weight of the current node
    // is a perfect number
    if (isPerfect(weight[node]))
        ans += 1;

    foreach(int to in graph[node])
    {
        if (to == parent)
            continue;
        dfs(to, node);
    }
}

// Driver code
public static void Main(String[] args)
{

    for(int i = 0; i < graph.Length; i++)
       graph[i] = new List<int>();

    // Weights of the node
    weight[1] = 5;
    weight[2] = 10;
    weight[3] = 11;
    weight[4] = 8;
    weight[5] = 6;

    // Edges of the tree
    graph[1].Add(2);
    graph[2].Add(3);
    graph[2].Add(4);
    graph[1].Add(5);

    dfs(1, 1);
    Console.Write(ans);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript implementation to Count the nodes in the
// given tree whose weight is a Perfect Number

var ans = 0;
var graph = Array.from(Array(100), ()=>Array());
var weight = Array.from(Array(100), ()=>Array());

// Function that returns true if n is perfect
function isPerfect(n)
{
    // Variable to store sum of divisors
    var sum = 1;

    // Find all divisors and add them
    for (var i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            if (i * i != n)
                sum = sum + i + n / i;
            else
                sum = sum + i;
        }
    }

    // Check if sum of divisors is equal to
    // n, then n is a perfect number
    if (sum == n && n != 1)
        return true;

    return false;
}

// Function to perform dfs
function dfs( node,  parent)
{

    // If weight of the current node
    // is a perfect number
    if (isPerfect(weight[node]))
        ans += 1;

    graph[node].forEach(to => {

        if (to != parent)
            dfs(to, node);
    });
}

// Driver code
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
document.write( ans);

</script>
```

**Output:** 

```
1
```

**<u>复杂度分析:</u>**

**时间复杂度** : O(N*logV)，其中 V 是树中节点的最大权重

在 dfs 中，树的每个节点都被处理一次，因此如果树中总共有 N 个节点，由于 DFS 而导致的复杂性是 O(N)。此外，在处理每个节点时，为了检查节点值是否是一个完美的数字，调用了 isPerfect(V)函数，其中 V 是节点的权重，该函数的复杂度为 O(logV)，因此对于每个节点，都会增加 O(logV)的复杂度。因此，时间复杂度为 O(N*logV)。

**辅助空间** : O(1)。

不需要任何额外的空间，因此空间复杂度是恒定的。