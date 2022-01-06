# 要添加到树中的最大边数，使其保持二部图

> 原文:[https://www . geesforgeks . org/maximum-number-edges-add-tree-stars-bipartite-graph/](https://www.geeksforgeeks.org/maximum-number-edges-added-tree-stays-bipartite-graph/)

一棵树总是一个[二部图](https://www.geeksforgeeks.org/bipartite-graph/)，因为我们总是可以用交替的层次分成两个不相交的集合。换句话说，我们总是用两种颜色给它上色，这样交替的层次就有相同的颜色。任务是计算可以添加到树中的最大边数，使其保持二分图。
**例:**

```
Input : Tree edges as vertex pairs 
        1 2
        1 3
Output : 0
Explanation :
The only edge we can add is from node 2 to 3.
But edge 2, 3 will result in odd cycle, hence 
violation of Bipartite Graph property.

Input : Tree edges as vertex pairs 
        1 2
        1 3
        2 4
        3 5
Output : 2
Explanation : On colouring the graph, {1, 4, 5} 
and {2, 3} form two different sets. Since, 1 is 
connected from both 2 and 3, we are left with 
edges 4 and 5\. Since, 4 is already connected to
2 and 5 to 3, only options remain {4, 3} and 
{5, 2}.
```

1)对图做一个简单的 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) (或 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) )遍历，用两种颜色上色。
2)着色时，还要记录用这两种颜色着色的节点数。让两个计数分别为 count_color <sub>0</sub> 和 count_color <sub>1</sub> 。
3)现在我们知道一个二部图可以拥有的最大边数是 count _ color<sub>0</sub>x count _ color<sub>1</sub>。
4)我们还知道有 n 个节点的树有 n-1 条边。
5)所以我们的答案是 count _ color<sub>0</sub>x count _ color<sub>1</sub>–(n-1)。
以下是执行:

## C++

```
// CPP code to print maximum edges such that
// Tree remains a Bipartite graph
#include <bits/stdc++.h>
using namespace std;

// To store counts of nodes with two colors
long long count_color[2];

void dfs(vector<int> adj[], int node, int parent, int color)
{
    // Increment count of nodes with current
    // color
    count_color[color]++;

    // Traversing adjacent nodes
    for (int i = 0; i < adj[node].size(); i++) {

        // Not recurring for the parent node
        if (adj[node][i] != parent)
            dfs(adj, adj[node][i], node, !color);
    }
}

// Finds maximum number of edges that can be added
// without violating Bipartite property.
int findMaxEdges(vector<int> adj[], int n)
{
    // Do a DFS to count number of nodes
    // of each color
    dfs(adj, 1, 0, 0);

    return count_color[0] * count_color[1] - (n - 1);
}

// Driver code
int main()
{
    int n = 5;
    vector<int> adj[n + 1];
    adj[1].push_back(2);
    adj[1].push_back(3);
    adj[2].push_back(4);
    adj[3].push_back(5);
    cout << findMaxEdges(adj, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to print maximum edges such that
// Tree remains a Bipartite graph
import java.util.*;

class GFG
{

// To store counts of nodes with two colors
static long []count_color = new long[2];

static void dfs(Vector<Integer> adj[], int node,
                      int parent, boolean color)
{
    // Increment count of nodes with current
    // color
    count_color[color == false ? 0 : 1]++;

    // Traversing adjacent nodes
    for (int i = 0; i < adj[node].size(); i++)
    {

        // Not recurring for the parent node
        if (adj[node].get(i) != parent)
            dfs(adj, adj[node].get(i), node, !color);
    }
}

// Finds maximum number of edges that can be added
// without violating Bipartite property.
static int findMaxEdges(Vector<Integer> adj[], int n)
{
    // Do a DFS to count number of nodes
    // of each color
    dfs(adj, 1, 0, false);

    return (int) (count_color[0] *
                  count_color[1] - (n - 1));
}

// Driver code
public static void main(String[] args)
{
    int n = 5;
    Vector<Integer>[] adj = new Vector[n + 1];
    for (int i = 0; i < n + 1; i++)
        adj[i] = new Vector<Integer>();

    adj[1].add(2);
    adj[1].add(3);
    adj[2].add(4);
    adj[3].add(5);
    System.out.println(findMaxEdges(adj, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 code to print maximum edges such
# that Tree remains a Bipartite graph
def dfs(adj, node, parent, color):

    # Increment count of nodes with
    # current color
    count_color[color] += 1

    # Traversing adjacent nodes
    for i in range(len(adj[node])):

        # Not recurring for the parent node
        if (adj[node][i] != parent):
            dfs(adj, adj[node][i],
                         node, not color)

# Finds maximum number of edges that
# can be added without violating
# Bipartite property.
def findMaxEdges(adj, n):

    # Do a DFS to count number of
    # nodes of each color
    dfs(adj, 1, 0, 0)

    return (count_color[0] *
            count_color[1] - (n - 1))

# Driver code

# To store counts of nodes with
# two colors
count_color = [0, 0]
n = 5
adj = [[] for i in range(n + 1)]
adj[1].append(2)
adj[1].append(3)
adj[2].append(4)
adj[3].append(5)
print(findMaxEdges(adj, n))

# This code is contributed by PranchalK
```

## C#

```
// C# code to print maximum edges such that
// Tree remains a Bipartite graph
using System;
using System.Collections.Generic;

class GFG
{

// To store counts of nodes with two colors
static long []count_color = new long[2];

static void dfs(List<int> []adj, int node,
                     int parent, bool color)
{
    // Increment count of nodes with current
    // color
    count_color[color == false ? 0 : 1]++;

    // Traversing adjacent nodes
    for (int i = 0; i < adj[node].Count; i++)
    {

        // Not recurring for the parent node
        if (adj[node][i] != parent)
            dfs(adj, adj[node][i], node, !color);
    }
}

// Finds maximum number of edges that can be added
// without violating Bipartite property.
static int findMaxEdges(List<int> []adj, int n)
{
    // Do a DFS to count number of nodes
    // of each color
    dfs(adj, 1, 0, false);

    return (int) (count_color[0] *
                  count_color[1] - (n - 1));
}

// Driver code
public static void Main(String[] args)
{
    int n = 5;
    List<int> []adj = new List<int>[n + 1];
    for (int i = 0; i < n + 1; i++)
        adj[i] = new List<int>();

    adj[1].Add(2);
    adj[1].Add(3);
    adj[2].Add(4);
    adj[3].Add(5);
    Console.WriteLine(findMaxEdges(adj, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript code to print maximum edges such that
    // Tree remains a Bipartite graph

    // To store counts of nodes with two colors
    let count_color = new Array(2);
    count_color.fill(0);

    function dfs(adj, node, parent, color)
    {
        // Increment count of nodes with current
        // color
        count_color[color == false ? 0 : 1]++;

        // Traversing adjacent nodes
        for (let i = 0; i < adj[node].length; i++)
        {

            // Not recurring for the parent node
            if (adj[node][i] != parent)
                dfs(adj, adj[node][i], node, !color);
        }
    }

    // Finds maximum number of edges that can be added
    // without violating Bipartite property.
    function findMaxEdges(adj, n)
    {
        // Do a DFS to count number of nodes
        // of each color
        dfs(adj, 1, 0, false);

        return (count_color[0] * count_color[1] - (n - 1));
    }

    let n = 5;
    let adj = [];
    for (let i = 0; i < n + 1; i++)
        adj.push([]);

    adj[1].push(2);
    adj[1].push(3);
    adj[2].push(4);
    adj[3].push(5);
    document.write(findMaxEdges(adj, n));

// This code is contributed by suresh07.
</script>
```

**输出:**

```
2
```

**时间复杂度:** O(n)
本文由 [**罗希特·塔普利亚尔**](https://www.hackerrank.com/rohit_thapliyal) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。