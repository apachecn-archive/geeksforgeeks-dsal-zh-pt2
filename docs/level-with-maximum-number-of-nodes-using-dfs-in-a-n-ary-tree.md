# N 元树中使用 DFS 的最大节点数级别

> 原文:[https://www . geeksforgeeks . org/最大节点数级别-使用 n 叉树中的 DFS/](https://www.geeksforgeeks.org/level-with-maximum-number-of-nodes-using-dfs-in-a-n-ary-tree/)

给定一个 **N 元**树，任务是打印具有最大节点数的级别。
**例:**

```
Input : For example, consider the following tree
          1               - Level 1
       /     \
      2       3           - Level 2
    /   \       \
   4     5       6        - Level 3
        /  \     /
       7    8   9         - Level 4

Output : Level-3 and Level-4
```

**进场:**

*   将所有连接节点插入二维向量树。
*   在树上运行 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) ，使高度【节点】= 1 +高度【父节点】
*   完成 DFS 遍历后，对于每个节点的级别，将*计数[]* 数组增加 1。
*   从**第一个**级迭代到**最后一个**级，找到节点数最多的一级。
*   从第一层到最后一层重新遍历，并打印具有相同最大节点数的所有层。

下面是上述方法的实现。

## C++

```
// C++ program to print the level
// with maximum number of nodes

#include <bits/stdc++.h>
using namespace std;

// Function for DFS in a tree
void dfs(int node, int parent, int height[], int vis[],
         vector<int> tree[])
{
    // calculate the level of every node
    height[node] = 1 + height[parent];

    // mark every node as visited
    vis[node] = 1;

    // iterate in the subtree
    for (auto it : tree[node]) {

        // if the node is not visited
        if (!vis[it]) {

            // call the dfs function
            dfs(it, node, height, vis, tree);
        }
    }
}

// Function to insert edges
void insertEdges(int x, int y, vector<int> tree[])
{
    tree[x].push_back(y);
    tree[y].push_back(x);
}

// Function to print all levels
void printLevelswithMaximumNodes(int N, int vis[], int height[])
{
    int mark[N + 1];
    memset(mark, 0, sizeof mark);

    int maxLevel = 0;
    for (int i = 1; i <= N; i++) {

        // count number of nodes
        // in every level
        if (vis[i])
            mark[height[i]]++;

        // find the maximum height of tree
        maxLevel = max(height[i], maxLevel);
    }

    int maxi = 0;

    for (int i = 1; i <= maxLevel; i++) {
        maxi = max(mark[i], maxi);
    }

    // print even number of nodes
    cout << "The levels with maximum number of nodes are: ";
    for (int i = 1; i <= maxLevel; i++) {
        if (mark[i] == maxi)
            cout << i << " ";
    }
}

// Driver Code
int main()
{
    // Construct the tree

    /* 1
     /  \
    2    3
    / \   \
   4   5   6
      / \  /
     7   8 9  */

    const int N = 9;

    vector<int> tree[N + 1];

    insertEdges(1, 2, tree);
    insertEdges(1, 3, tree);
    insertEdges(2, 4, tree);
    insertEdges(2, 5, tree);
    insertEdges(5, 7, tree);
    insertEdges(5, 8, tree);
    insertEdges(3, 6, tree);
    insertEdges(6, 9, tree);

    int height[N + 1];
    int vis[N + 1] = { 0 };

    height[0] = 0;

    // call the dfs function
    dfs(1, 0, height, vis, tree);

    // Function to print
    printLevelswithMaximumNodes(N, vis, height);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the level
// with maximum number of nodes
import java.util.*;

class GFG
{
    static int N = 9;

// Function for DFS in a tree
static void dfs(int node, int parent, int height[], int vis[],
        Vector<Integer> tree[])
{
    // calculate the level of every node
    height[node] = 1 + height[parent];

    // mark every node as visited
    vis[node] = 1;

    // iterate in the subtree
    for (int it : tree[node])
    {

        // if the node is not visited
        if (vis[it] != 1)
        {

            // call the dfs function
            dfs(it, node, height, vis, tree);
        }
    }
}

// Function to insert edges
static void insertEdges(int x, int y, Vector<Integer> tree[])
{
    tree[x].add(y);
    tree[y].add(x);
}

// Function to print all levels
static void printLevelswithMaximumNodes(int N, int vis[], int height[])
{
    int []mark = new int[N + 1];

    int maxLevel = 0;
    for (int i = 1; i <= N; i++) {

        // count number of nodes
        // in every level
        if (vis[i] == 1)
            mark[height[i]]++;

        // find the maximum height of tree
        maxLevel = Math.max(height[i], maxLevel);
    }

    int maxi = 0;

    for (int i = 1; i <= maxLevel; i++)
    {
        maxi = Math.max(mark[i], maxi);
    }

    // print even number of nodes
    System.out.print("The levels with maximum number of nodes are: ");
    for (int i = 1; i <= maxLevel; i++)
    {
        if (mark[i] == maxi)
            System.out.print(i+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    // Construct the tree

    /* 1
    / \
    2 3
    / \ \
4 5 6
    / \ /
    7 8 9 */

    Vector<Integer> []tree = new Vector[N + 1];
    for(int i= 0; i < N + 1; i++)
        tree[i] = new Vector<Integer>();
    insertEdges(1, 2, tree);
    insertEdges(1, 3, tree);
    insertEdges(2, 4, tree);
    insertEdges(2, 5, tree);
    insertEdges(5, 7, tree);
    insertEdges(5, 8, tree);
    insertEdges(3, 6, tree);
    insertEdges(6, 9, tree);

    int height[] = new int[N + 1];
    int vis[] = new int[N + 1];

    height[0] = 0;

    // call the dfs function
    dfs(1, 0, height, vis, tree);

    // Function to print
    printLevelswithMaximumNodes(N, vis, height);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to print the level
# with the maximum number of nodes

# Function for DFS in a tree
def dfs(node, parent, height, vis, tree):

    # calculate the level of every node
    height[node] = 1 + height[parent]

    # mark every node as visited
    vis[node] = 1

    # iterate in the subtree
    for it in tree[node]:

        # if the node is not visited
        if vis[it] == 0:

            # call the dfs function
            dfs(it, node, height, vis, tree)

# Function to insert edges
def insertEdges(x, y, tree):

    tree[x].append(y)
    tree[y].append(x)

# Function to print all levels
def printLevelswithMaximumNodes(N, vis, height):

    mark = [0] * (N + 1)

    maxLevel = 0
    for i in range (1, N + 1):

        # count number of nodes
        # in every level
        if vis[i] == 1:
            mark[height[i]] += 1

        # find the maximum height of tree
        maxLevel = max(height[i], maxLevel)

    maxi = 0

    for i in range(1, maxLevel + 1):
        maxi = max(mark[i], maxi)

    # print even number of nodes
    print("The levels with maximum number",
                "of nodes are:", end = " ")
    for i in range(1, maxLevel + 1):
        if mark[i] == maxi:
            print(i, end = " ")

# Driver Code
if __name__ == "__main__":

    # Construct the tree
    N = 9

    # Create an empty 2-D list
    tree = [[] for i in range(N + 1)]

    insertEdges(1, 2, tree)
    insertEdges(1, 3, tree)
    insertEdges(2, 4, tree)
    insertEdges(2, 5, tree)
    insertEdges(5, 7, tree)
    insertEdges(5, 8, tree)
    insertEdges(3, 6, tree)
    insertEdges(6, 9, tree)

    height = [None] * (N + 1)
    vis = [0] * (N + 1)

    height[0] = 0

    # call the dfs function
    dfs(1, 0, height, vis, tree)

    # Function to print
    printLevelswithMaximumNodes(N, vis, height)

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to print the level
// with maximum number of nodes
using System;
using System.Collections.Generic;

public class GFG
{
    static int N = 9;

// Function for DFS in a tree
static void dfs(int node, int parent, int []height, int []vis,
        List<int> []tree)
{
    // calculate the level of every node
    height[node] = 1 + height[parent];

    // mark every node as visited
    vis[node] = 1;

    // iterate in the subtree
    foreach (int it in tree[node])
    {

        // if the node is not visited
        if (vis[it] != 1)
        {

            // call the dfs function
            dfs(it, node, height, vis, tree);
        }
    }
}

// Function to insert edges
static void insertEdges(int x, int y, List<int> []tree)
{
    tree[x].Add(y);
    tree[y].Add(x);
}

// Function to print all levels
static void printLevelswithMaximumNodes(int N, int []vis, int []height)
{
    int []mark = new int[N + 1];

    int maxLevel = 0;
    for (int i = 1; i <= N; i++) {

        // count number of nodes
        // in every level
        if (vis[i] == 1)
            mark[height[i]]++;

        // find the maximum height of tree
        maxLevel = Math.Max(height[i], maxLevel);
    }

    int maxi = 0;

    for (int i = 1; i <= maxLevel; i++)
    {
        maxi = Math.Max(mark[i], maxi);
    }

    // print even number of nodes
    Console.Write("The levels with maximum number of nodes are: ");
    for (int i = 1; i <= maxLevel; i++)
    {
        if (mark[i] == maxi)
            Console.Write(i+ " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    // Construct the tree

    /* 1
    / \
    2 3
    / \ \
4 5 6
    / \ /
    7 8 9 */

    List<int> []tree = new List<int>[N + 1];
    for(int i= 0; i < N + 1; i++)
        tree[i] = new List<int>();
    insertEdges(1, 2, tree);
    insertEdges(1, 3, tree);
    insertEdges(2, 4, tree);
    insertEdges(2, 5, tree);
    insertEdges(5, 7, tree);
    insertEdges(5, 8, tree);
    insertEdges(3, 6, tree);
    insertEdges(6, 9, tree);

    int []height = new int[N + 1];
    int []vis = new int[N + 1];

    height[0] = 0;

    // call the dfs function
    dfs(1, 0, height, vis, tree);

    // Function to print
    printLevelswithMaximumNodes(N, vis, height);

}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript program to print the level
    // with maximum number of nodes

    let N = 9;

    let tree = new Array(N + 1);

      let height = new Array(N + 1);
    height.fill(0);
    let vis = new Array(N + 1);
    vis.fill(0);

    // Function for DFS in a tree
    function dfs(node, parent, tree)
    {
        // calculate the level of every node
        height[node] = 1 + height[parent];

        // mark every node as visited
        vis[node] = 1;

        // iterate in the subtree
        for (let it = 0; it < tree[node].length; it++)
        {

            // if the node is not visited
            if (vis[tree[node][it]] != 1)
            {

                // call the dfs function
                dfs(tree[node][it], node, tree);
            }
        }
    }

    // Function to insert edges
    function insertEdges(x, y, tree)
    {
        tree[x].push(y);
        tree[y].push(x);
    }

    // Function to print all levels
    function printLevelswithMaximumNodes(N)
    {
        let mark = new Array(N + 1);
        mark.fill(0);

        let maxLevel = 0;
        for (let i = 1; i <= N; i++) {

            // count number of nodes
            // in every level
            if (vis[i] == 1)
                mark[height[i]]++;

            // find the maximum height of tree
            maxLevel = Math.max(height[i], maxLevel);
        }

        let maxi = 0;

        for (let i = 1; i <= maxLevel; i++)
        {
            maxi = Math.max(mark[i], maxi);
        }

        // print even number of nodes
        document.write(
        "The levels with maximum number of nodes are: "
        );
        for (let i = 1; i <= maxLevel; i++)
        {
            if (mark[i] == maxi)
                document.write(i+ " ");
        }
    }

    // Construct the tree

    /* 1
    / \
    2 3
    / \ \
4 5 6
    / \ /
    7 8 9 */

    for(let i= 0; i < N + 1; i++)
    {
        tree[i] = [];
    }
    insertEdges(1, 2, tree);
    insertEdges(1, 3, tree);
    insertEdges(2, 4, tree);
    insertEdges(2, 5, tree);
    insertEdges(5, 7, tree);
    insertEdges(5, 8, tree);
    insertEdges(3, 6, tree);
    insertEdges(6, 9, tree);

    height[0] = 0;

    // call the dfs function
    dfs(1, 0, tree);

    // Function to print
    printLevelswithMaximumNodes(N);

</script>
```

**Output:** 

```
The levels with maximum number of nodes are: 3 4
```

**时间复杂度**:O(N)
T3】辅助空间 : O(N)