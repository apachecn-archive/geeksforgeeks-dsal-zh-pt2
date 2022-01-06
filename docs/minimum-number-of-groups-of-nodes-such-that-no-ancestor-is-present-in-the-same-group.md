# 节点组的最小数量，使得同一组中不存在祖先

> 原文:[https://www . geeksforgeeks . org/最小节点组数-同一组中不存在祖先/](https://www.geeksforgeeks.org/minimum-number-of-groups-of-nodes-such-that-no-ancestor-is-present-in-the-same-group/)

给定一个由 **N 个**节点组成的树。任务是形成最小数量的节点组，使得每个节点恰好属于一个组，并且其祖先都不在同一组中。每个节点的父节点是给定的(-1，如果节点没有父节点)。
**例:**

> **输入:** par[] = {-1，1，2，1，4 }
> T3】输出: 3
> 这三组可以是:
> 组 1: {1}
> 组 2: {2，4}
> 组 3: {3，5}
> **输入:** par[] = {-1，1，1，2，2，5，6}
> **输出:** 5

**方法:**可以通过将同一级别的节点分组在一起来进行分组(一个节点和它的任何祖先不能在同一级别)。所以最小的组数将是树的最大深度。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the depth of the tree
int findDepth(int x, vector<int> child[])
{
    int mx = 0;

    // Find the maximum depth of all its children
    for (auto ch : child[x])
        mx = max(mx, findDepth(ch, child));

    // Add 1 for the depth of the current node
    return mx + 1;
}

// Function to return
// the minimum number of groups required
int minimumGroups(int n, int par[])
{
    vector<int> child[n + 1];

    // For every node create a list of its children
    for (int i = 1; i <= n; i++)
        if (par[i] != -1)
            child[par[i]].push_back(i);
    int res = 0;

    for (int i = 1; i <= n; i++)

        // If the node is root
        // perform dfs starting with this node
        if (par[i] == -1)
            res = max(res, findDepth(i, child));

    return res;
}

// Driver code
main()
{
    int par[] = { 0, -1, 1, 1, 2, 2, 5, 6 };
    int n = sizeof(par) / sizeof(par[0]) - 1;
    cout << minimumGroups(n, par);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the depth of the tree
    static int findDepth(int x, Vector<Integer> child[])
    {
        int mx = 0;

        // Find the maximum depth of all its children
        for (Integer ch : child[x])
            mx = Math.max(mx, findDepth(ch, child));

        // Add 1 for the depth of the current node
        return mx + 1;
    }

    // Function to return
    // the minimum number of groups required
    static int minimumGroups(int n, int par[])
    {
        Vector<Integer>[] child = new Vector[n + 1];
        for (int i = 0; i <= n; i++)
        {
            child[i] = new Vector<Integer>();
        }

        // For every node create a list of its children
        for (int i = 1; i <= n; i++)
            if (par[i] != -1)
                child[par[i]].add(i);
        int res = 0;

        for (int i = 1; i <= n; i++)

            // If the node is root
            // perform dfs starting with this node
            if (par[i] == -1)
                res = Math.max(res, findDepth(i, child));

        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        int par[] = { 0, -1, 1, 1, 2, 2, 5, 6 };
        int n = par.length - 1;
        System.out.print(minimumGroups(n, par));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the depth of the tree
def findDepth(x, child):
    mx = 0

    # Find the maximum depth
    # of all its children
    for ch in child[x]:
        mx = max(mx, findDepth(ch, child))

    # Add 1 for the depth
    # of the current node
    return mx + 1

# Function to return the minimum 
# number of groups required
def minimumGroups(n, par):
    child = [[] for i in range(n + 1)]

    # For every node create a list
    # of its children
    for i in range(0, n):
        if (par[i] != -1):
            child[par[i]].append(i)
    res = 0
    for i in range(0, n):

        # If the node is root
        # perform dfs starting with this node
        if(par[i] == -1):
            res = max(res, findDepth(i, child))
    return res

# Driver Code
array = [0, -1, 1, 1, 2, 2, 5, 6]
print(minimumGroups(len(array), array))

# This code is contributed
# by SidharthPanicker
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return the depth of the tree
    static int findDepth(int x, List<int> []child)
    {
        int mx = 0;

        // Find the maximum depth of all its children
        foreach (int ch in child[x])
            mx = Math.Max(mx, findDepth(ch, child));

        // Add 1 for the depth of the current node
        return mx + 1;
    }

    // Function to return
    // the minimum number of groups required
    static int minimumGroups(int n, int []par)
    {
        List<int>[] child = new List<int>[n + 1];
        for (int i = 0; i <= n; i++)
        {
            child[i] = new List<int>();
        }

        // For every node create a list of its children
        for (int i = 1; i <= n; i++)
            if (par[i] != -1)
                child[par[i]].Add(i);
        int res = 0;

        for (int i = 1; i <= n; i++)

            // If the node is root
            // perform dfs starting with this node
            if (par[i] == -1)
                res = Math.Max(res, findDepth(i, child));

        return res;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []par = { 0, -1, 1, 1, 2, 2, 5, 6 };
        int n = par.Length - 1;
        Console.Write(minimumGroups(n, par));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the depth of the tree
function findDepth(x, child)
{
    var mx = 0;

    // Find the maximum depth of all its children
    child[x].forEach(ch => {

        mx = Math.max(mx, findDepth(ch, child));
    });

    // Add 1 for the depth of the current node
    return mx + 1;
}

// Function to return
// the minimum number of groups required
function minimumGroups(n, par)
{
    var child = Array.from(Array(n+1), ()=>Array());

    // For every node create a list of its children
    for (var i = 1; i <= n; i++)
        if (par[i] != -1)
            child[par[i]].push(i);
    var res = 0;

    for (var i = 1; i <= n; i++)

        // If the node is root
        // perform dfs starting with this node
        if (par[i] == -1)
            res = Math.max(res, findDepth(i, child));

    return res;
}

// Driver code
var par = [0, -1, 1, 1, 2, 2, 5, 6 ];
var n = par.length - 1;
document.write( minimumGroups(n, par));

// This code is contributed by famously.
</script>
```

**Output:** 

```
5
```