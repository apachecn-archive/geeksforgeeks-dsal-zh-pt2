# 有根树中一组节点的最低共同祖先

> 原文:[https://www . geesforgeks . org/根树中一组节点的最低共同祖先/](https://www.geeksforgeeks.org/lowest-common-ancestor-for-a-set-of-nodes-in-a-rooted-tree/)

给定一棵有 **N** 个节点的根树，任务是为该树的一组给定节点 **V** 找到 [**最低共同祖先**](https://www.geeksforgeeks.org/lowest-common-ancestor-binary-tree-set-1/?ref=lbp) 。
**举例:**

```
Input:    
                   1
                /  |  \
               2   3   4
             /  \  |   |
            5   6  7   10
                  / \
                 8   9
V[] = {7, 3, 8, 9}
Output: 3

Input:   
                   1
                /  |  \
               2   3   4
             /  \  |   |
            5   6  7   10
                  / \
                 8   9
V[] = {4, 6, 7}
Output: 1
```

**进场:**我们可以观察到

1.  任何一组节点的[最低共同祖先](https://www.geeksforgeeks.org/tag/lca/)将具有小于或等于该组中所有节点的进入时间和大于或等于(如果该组中存在生命周期评价，则等于)该组中所有节点的离开时间。
2.  因此，为了解决这个问题，我们需要使用[深度优先搜索遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)从根节点开始遍历整个树，并存储每个节点的时间、超时和级别。
3.  时间小于或等于集合中所有节点的节点，以及时间大于或等于集合中所有节点且具有最大可能级别的节点就是答案。

以下是上述方法的实现:

## C++

```
// C++ Program to find the LCA
// in a rooted tree for a given
// set of nodes

#include <bits/stdc++.h>
using namespace std;

// Set time 1 initially
int T = 1;
void dfs(int node, int parent,
         vector<int> g[],
         int level[], int t_in[],
         int t_out[])
{

    // Case for root node
    if (parent == -1) {
        level[node] = 1;
    }
    else {
        level[node] = level[parent] + 1;
    }

    // In-time for node
    t_in[node] = T;
    for (auto i : g[node]) {
        if (i != parent) {
            T++;
            dfs(i, node, g,
                level, t_in, t_out);
        }
    }
    T++;

    // Out-time for the node
    t_out[node] = T;
}

int findLCA(int n, vector<int> g[],
            vector<int> v)
{

    // level[i]--> Level of node i
    int level[n + 1];

    // t_in[i]--> In-time of node i
    int t_in[n + 1];

    // t_out[i]--> Out-time of node i
    int t_out[n + 1];

    // Fill the level, in-time
    // and out-time of all nodes
    dfs(1, -1, g,
        level, t_in, t_out);

    int mint = INT_MAX, maxt = INT_MIN;
    int minv = -1, maxv = -1;
    for (auto i = v.begin(); i != v.end(); i++) {
        // To find minimum in-time among
        // all nodes in LCA set
        if (t_in[*i] < mint) {
            mint = t_in[*i];
            minv = *i;
        }
        // To find maximum in-time among
        // all nodes in LCA set
        if (t_out[*i] > maxt) {
            maxt = t_out[*i];
            maxv = *i;
        }
    }

    // Node with same minimum
    // and maximum out time
    // is LCA for the set
    if (minv == maxv) {
        return minv;
    }

    // Take the minimum level as level of LCA
    int lev = min(level[minv], level[maxv]);
    int node, l = INT_MIN;
    for (int i = 1; i <= n; i++) {
        // If i-th node is at a higher level
        // than that of the minimum among
        // the nodes of the given set
        if (level[i] > lev)
            continue;

        // Compare in-time, out-time
        // and level of i-th node
        // to the respective extremes
        // among all nodes of the given set
        if (t_in[i] <= mint
            && t_out[i] >= maxt
            && level[i] > l) {
            node = i;
            l = level[i];
        }
    }

    return node;
}

// Driver code
int main()
{
    int n = 10;
    vector<int> g[n + 1];
    g[1].push_back(2);
    g[2].push_back(1);
    g[1].push_back(3);
    g[3].push_back(1);
    g[1].push_back(4);
    g[4].push_back(1);
    g[2].push_back(5);
    g[5].push_back(2);
    g[2].push_back(6);
    g[6].push_back(2);
    g[3].push_back(7);
    g[7].push_back(3);
    g[4].push_back(10);
    g[10].push_back(4);
    g[8].push_back(7);
    g[7].push_back(8);
    g[9].push_back(7);
    g[7].push_back(9);

    vector<int> v = { 7, 3, 8 };

    cout << findLCA(n, g, v) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the LCA
// in a rooted tree for a given
// set of nodes
import java.util.*;
class GFG
{

// Set time 1 initially
static int T = 1;
static void dfs(int node, int parent,
         Vector<Integer> g[],
         int level[], int t_in[],
         int t_out[])
{

    // Case for root node
    if (parent == -1)
    {
        level[node] = 1;
    }
    else
    {
        level[node] = level[parent] + 1;
    }

    // In-time for node
    t_in[node] = T;
    for (int i : g[node])
    {
        if (i != parent)
        {
            T++;
            dfs(i, node, g,
                level, t_in, t_out);
        }
    }
    T++;

    // Out-time for the node
    t_out[node] = T;
}

static int findLCA(int n, Vector<Integer> g[],
            Vector<Integer> v)
{

    // level[i]-. Level of node i
    int []level = new int[n + 1];

    // t_in[i]-. In-time of node i
    int []t_in = new int[n + 1];

    // t_out[i]-. Out-time of node i
    int []t_out = new int[n + 1];

    // Fill the level, in-time
    // and out-time of all nodes
    dfs(1, -1, g,
        level, t_in, t_out);

    int mint = Integer.MAX_VALUE, maxt = Integer.MIN_VALUE;
    int minv = -1, maxv = -1;
    for (int i =0; i <v.size(); i++)
    {

        // To find minimum in-time among
        // all nodes in LCA set
        if (t_in[v.get(i)] < mint)
        {
            mint = t_in[v.get(i)];
            minv = v.get(i);
        }
        // To find maximum in-time among
        // all nodes in LCA set
        if (t_out[v.get(i)] > maxt)
        {
            maxt = t_out[v.get(i)];
            maxv = v.get(i);
        }
    }

    // Node with same minimum
    // and maximum out time
    // is LCA for the set
    if (minv == maxv)
    {
        return minv;
    }

    // Take the minimum level as level of LCA
    int lev = Math.min(level[minv], level[maxv]);
    int node = 0, l = Integer.MIN_VALUE;
    for (int i = 1; i <= n; i++)
    {

        // If i-th node is at a higher level
        // than that of the minimum among
        // the nodes of the given set
        if (level[i] > lev)
            continue;

        // Compare in-time, out-time
        // and level of i-th node
        // to the respective extremes
        // among all nodes of the given set
        if (t_in[i] <= mint
            && t_out[i] >= maxt
            && level[i] > l)
        {
            node = i;
            l = level[i];
        }
    }

    return node;
}

// Driver code
public static void main(String[] args)
{
    int n = 10;
    Vector<Integer> []g = new Vector[n + 1];
    for (int i = 0; i < g.length; i++)
        g[i] = new Vector<Integer>();
    g[1].add(2);
    g[2].add(1);
    g[1].add(3);
    g[3].add(1);
    g[1].add(4);
    g[4].add(1);
    g[2].add(5);
    g[5].add(2);
    g[2].add(6);
    g[6].add(2);
    g[3].add(7);
    g[7].add(3);
    g[4].add(10);
    g[10].add(4);
    g[8].add(7);
    g[7].add(8);
    g[9].add(7);
    g[7].add(9);
    Vector<Integer> v = new Vector<>();
    v.add(7);
    v.add(3);
    v.add(8);
    System.out.print(findLCA(n, g, v) +"\n");
}
}

// This code is contributed by aashish1995.
```

## 蟒蛇 3

```
# Python Program to find the LCA
# in a rooted tree for a given
# set of nodes
from typing import List
from sys import maxsize
INT_MAX = maxsize
INT_MIN = -maxsize

# Set time 1 initially
T = 1

def dfs(node: int, parent: int, g: List[List[int]], level: List[int],
        t_in: List[int], t_out: List[int]) -> None:
    global T

    # Case for root node
    if (parent == -1):
        level[node] = 1
    else:
        level[node] = level[parent] + 1

    # In-time for node
    t_in[node] = T
    for i in g[node]:
        if (i != parent):
            T += 1
            dfs(i, node, g, level, t_in, t_out)
    T += 1

    # Out-time for the node
    t_out[node] = T

def findLCA(n: int, g: List[List[int]], v: List[int]) -> int:

    # level[i]--> Level of node i
    level = [0 for _ in range(n + 1)]

    # t_in[i]--> In-time of node i
    t_in = [0 for _ in range(n + 1)]

    # t_out[i]--> Out-time of node i
    t_out = [0 for _ in range(n + 1)]

    # Fill the level, in-time
    # and out-time of all nodes
    dfs(1, -1, g, level, t_in, t_out)
    mint = INT_MAX
    maxt = INT_MIN
    minv = -1
    maxv = -1
    for i in v:

        # To find minimum in-time among
        # all nodes in LCA set
        if (t_in[i] < mint):
            mint = t_in[i]
            minv = i

        # To find maximum in-time among
        # all nodes in LCA set
        if (t_out[i] > maxt):
            maxt = t_out[i]
            maxv = i

    # Node with same minimum
    # and maximum out time
    # is LCA for the set
    if (minv == maxv):
        return minv

    # Take the minimum level as level of LCA
    lev = min(level[minv], level[maxv])
    node = 0
    l = INT_MIN
    for i in range(n):

        # If i-th node is at a higher level
        # than that of the minimum among
        # the nodes of the given set
        if (level[i] > lev):
            continue

        # Compare in-time, out-time
        # and level of i-th node
        # to the respective extremes
        # among all nodes of the given set
        if (t_in[i] <= mint and t_out[i] >= maxt and level[i] > l):
            node = i
            l = level[i]
    return node

# Driver code
if __name__ == "__main__":
    n = 10
    g = [[] for _ in range(n + 1)]
    g[1].append(2)
    g[2].append(1)
    g[1].append(3)
    g[3].append(1)
    g[1].append(4)
    g[4].append(1)
    g[2].append(5)
    g[5].append(2)
    g[2].append(6)
    g[6].append(2)
    g[3].append(7)
    g[7].append(3)
    g[4].append(10)
    g[10].append(4)
    g[8].append(7)
    g[7].append(8)
    g[9].append(7)
    g[7].append(9)

    v = [7, 3, 8]
    print(findLCA(n, g, v))

# This code is contributed by sanjeev2552
```

## C#

```
// C# Program to find the LCA
// in a rooted tree for a given
// set of nodes
using System;
using System.Collections.Generic;
public class GFG
{

  // Set time 1 initially
  static int T = 1;
  static void dfs(int node, int parent,
                  List<int> []g,
                  int []level, int []t_in,
                  int []t_out)
  {

    // Case for root node
    if (parent == -1)
    {
      level[node] = 1;
    }
    else
    {
      level[node] = level[parent] + 1;
    }

    // In-time for node
    t_in[node] = T;
    foreach (int i in g[node])
    {
      if (i != parent)
      {
        T++;
        dfs(i, node, g,
            level, t_in, t_out);
      }
    }
    T++;

    // Out-time for the node
    t_out[node] = T;
  }

  static int findLCA(int n, List<int> []g,
                     List<int> v)
  {

    // level[i]-. Level of node i
    int []level = new int[n + 1];

    // t_in[i]-. In-time of node i
    int []t_in = new int[n + 1];

    // t_out[i]-. Out-time of node i
    int []t_out = new int[n + 1];

    // Fill the level, in-time
    // and out-time of all nodes
    dfs(1, -1, g,
        level, t_in, t_out);

    int mint = int.MaxValue, maxt = int.MinValue;
    int minv = -1, maxv = -1;
    for (int i = 0; i < v.Count; i++)
    {

      // To find minimum in-time among
      // all nodes in LCA set
      if (t_in[v[i]] < mint)
      {
        mint = t_in[v[i]];
        minv = v[i];
      }

      // To find maximum in-time among
      // all nodes in LCA set
      if (t_out[v[i]] > maxt)
      {
        maxt = t_out[v[i]];
        maxv = v[i];
      }
    }

    // Node with same minimum
    // and maximum out time
    // is LCA for the set
    if (minv == maxv)
    {
      return minv;
    }

    // Take the minimum level as level of LCA
    int lev = Math.Min(level[minv], level[maxv]);
    int node = 0, l = int.MinValue;
    for (int i = 1; i <= n; i++)
    {

      // If i-th node is at a higher level
      // than that of the minimum among
      // the nodes of the given set
      if (level[i] > lev)
        continue;

      // Compare in-time, out-time
      // and level of i-th node
      // to the respective extremes
      // among all nodes of the given set
      if (t_in[i] <= mint
          && t_out[i] >= maxt
          && level[i] > l)
      {
        node = i;
        l = level[i];
      }
    }
    return node;
  }

  // Driver code
  public static void Main(String[] args)
  {
    int n = 10;
    List<int> []g = new List<int>[n + 1];
    for (int i = 0; i < g.Length; i++)
      g[i] = new List<int>();
    g[1].Add(2);
    g[2].Add(1);
    g[1].Add(3);
    g[3].Add(1);
    g[1].Add(4);
    g[4].Add(1);
    g[2].Add(5);
    g[5].Add(2);
    g[2].Add(6);
    g[6].Add(2);
    g[3].Add(7);
    g[7].Add(3);
    g[4].Add(10);
    g[10].Add(4);
    g[8].Add(7);
    g[7].Add(8);
    g[9].Add(7);
    g[7].Add(9);
    List<int> v = new List<int>();
    v.Add(7);
    v.Add(3);
    v.Add(8);
    Console.Write(findLCA(n, g, v) +"\n");
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript Program to find the LCA
    // in a rooted tree for a given
    // set of nodes

    // Set time 1 initially
    let T = 1;
    function dfs(node, parent, g, level, t_in, t_out)
    {

        // Case for root node
        if (parent == -1)
        {
            level[node] = 1;
        }
        else
        {
            level[node] = level[parent] + 1;
        }

        // In-time for node
        t_in[node] = T;
        for (let i = 0; i < g[node].length; i++)
        {
            if (g[node][i] != parent)
            {
                T++;
                dfs(g[node][i], node, g, level, t_in, t_out);
            }
        }
        T++;

        // Out-time for the node
        t_out[node] = T;
    }

    function findLCA(n, g, v)
    {

        // level[i]-. Level of node i
        let level = new Array(n + 1);

        // t_in[i]-. In-time of node i
        let t_in = new Array(n + 1);

        // t_out[i]-. Out-time of node i
        let t_out = new Array(n + 1);

        // Fill the level, in-time
        // and out-time of all nodes
        dfs(1, -1, g, level, t_in, t_out);

        let mint = Number.MAX_VALUE, maxt = Number.MIN_VALUE;
        let minv = -1, maxv = -1;
        for (let i =0; i < v.length; i++)
        {

            // To find minimum in-time among
            // all nodes in LCA set
            if (t_in[v[i]] < mint)
            {
                mint = t_in[v[i]];
                minv = v[i];
            }
            // To find maximum in-time among
            // all nodes in LCA set
            if (t_out[v[i]] > maxt)
            {
                maxt = t_out[v[i]];
                maxv = v[i];
            }
        }

        // Node with same minimum
        // and maximum out time
        // is LCA for the set
        if (minv == maxv)
        {
            return minv;
        }

        // Take the minimum level as level of LCA
        let lev = Math.min(level[minv], level[maxv]);
        let node = 0, l = Number.MIN_VALUE;
        for (let i = 1; i <= n; i++)
        {

            // If i-th node is at a higher level
            // than that of the minimum among
            // the nodes of the given set
            if (level[i] > lev)
                continue;

            // Compare in-time, out-time
            // and level of i-th node
            // to the respective extremes
            // among all nodes of the given set
            if (t_in[i] <= mint
                && t_out[i] >= maxt
                && level[i] > l)
            {
                node = i;
                l = level[i];
            }
        }

        return node;
    }

    let n = 10;
    let g = new Array(n + 1);
    for (let i = 0; i < g.length; i++)
        g[i] = [];
    g[1].push(2);
    g[2].push(1);
    g[1].push(3);
    g[3].push(1);
    g[1].push(4);
    g[4].push(1);
    g[2].push(5);
    g[5].push(2);
    g[2].push(6);
    g[6].push(2);
    g[3].push(7);
    g[7].push(3);
    g[4].push(10);
    g[10].push(4);
    g[8].push(7);
    g[7].push(8);
    g[9].push(7);
    g[7].push(9);
    let v = [];
    v.push(7);
    v.push(3);
    v.push(8);
    document.write(findLCA(n, g, v) +"</br>");

</script>
```

**Output:** 

```
3
```

**时间复杂度:***O(N)*
T5】空间复杂度: *O(N)*