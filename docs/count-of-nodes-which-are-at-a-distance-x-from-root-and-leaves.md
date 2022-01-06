# 距根和叶距离为 X 的节点数

> 原文:[https://www . geeksforgeeks . org/根叶距离为 x 的节点数/](https://www.geeksforgeeks.org/count-of-nodes-which-are-at-a-distance-x-from-root-and-leaves/)

给定两个整数 **N** 和 **X** ，其中 **N** 是几乎[完整二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)中的节点数。任务是找到:

1.  距离根的 **X** 距离处的节点数。
2.  距离其子树中任何叶子的 **X** 距离处的节点数。

**注意:**完全二叉树是这样一种二叉树，其中除了可能的最后一级之外，每一级都被完全填充，并且所有节点都尽可能向左。

**示例:**

```
Input: N = 6, X = 0
Output: 
1
3
Complete Binary Tree of 6 nodes is
         1
       /    \  
      2      3 
    /  \    / 
   4    5  6
Nodes that are at 0 distance from root = 1 (root itself).
Nodes that are at 0 distance from any of the leaf = 3 (all the leaves of the tree)

Input: N = 13, X = 1
Output:
2
4
Complete Binary Tree of 13 nodes.
                       1
                  /         \  
                2             3 
              /   \         /   \
            4      5       6     7
          /  \    /  \   /  \  
         8    9  10  11 12  13
Nodes that are at 0 distance from root = 2 (node no. 2 and 3)
Nodes that are at 0 distance from any of the leaf = 4 (node no. 4, 5, 6 and 3)
```

**进场:**

1.  找到距离根 x 距离的节点数很简单。我们只需打印第 x 高度的节点数。我们知道，在一个完整的二叉树中，每一级都是完整的，除了最后一级和所有节点尽可能地靠左。因此，完整二叉树的高度 **h** 计算为**楼(log2(n))** ，其中 **n** 为节点总数。此外，第 I 高度的节点数将为 **2 <sup>i</sup>** 和最后一级(即高度 h)的节点数=**2<sup>h</sup>–(max _ total _ nodes–n)**，其中 **2 <sup>h</sup>** 为高度 **h** 的最大节点数。
2.  找到距离其子树中任何叶子 x 距离的节点数有点棘手。这是关于观察这样一个事实，如果我们有 **l** 个叶节点，那么 **ceil(l/2)** 个节点是 **1** 个离叶单位距离， **ceil(l/4)** 个节点是 **2** 个离叶单位距离。直到**天花板(l/2 <sup>i</sup> )** 节点离树叶的距离为 **i** 单位。我们将首先找到叶节点的数量，并应用上述方法找到距叶 x 距离的节点。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count
// of the required nodes
void countNodes(int N, int X)
{

    // Height of the complete binary
    // tree with n nodes
    int height = floor(log2(N));

    // If X > height then no node
    // can be present at that level
    if (X > height) {
        cout << "0\n0";
        return;
    }

    // Corner case
    if (N == 1) {
        cout << "1\n1";
        return;
    }

    // Maximum total nodes that are possible
    // in complete binary tree with height h
    int max_total_nodes = (1 << (height + 1)) - 1;

    // Nodes at the last level
    int nodes_last_level
        = (1 << height) - (max_total_nodes - N);

    // To store the count of nodes
    // x dist away from root
    int from_root;

    // To store the count of nodes
    // x dist away from leaf
    int from_leaf;

    // If X = h then print nodes at last level
    // else nodes at Xth level
    if (X == height)
        from_root = nodes_last_level;

    // 2^X
    else
        from_root = 1 << X;

    // Number of left leaf nodes at (h-1)th level
    // observe that if nodes are not present at last level
    // then there are a/2 leaf nodes at (h-1)th level
    int left_leaf_nodes
        = ((1 << height) - nodes_last_level) / 2;

    // If X = h then print leaf nodes at the last h level
    // + leaf nodes at (h-1)th level
    if (X == 0) {
        from_leaf = nodes_last_level + left_leaf_nodes;
    }
    else {

        // First calculate nodes for leaves present at
        // height h
        int i = X;

        while (nodes_last_level > 1 && i > 0) {
            nodes_last_level
                = ceil((float)nodes_last_level / (float)2);
            i--;
        }

        from_leaf = nodes_last_level;

        // Then calculate nodes for leaves present at height
        // h-1
        i = X;
        while (left_leaf_nodes > 1 && i > 0) {
            left_leaf_nodes
                = ceil((float)left_leaf_nodes / (float)2);
            i--;
        }

        // Add both the results
        from_leaf += left_leaf_nodes;
    }

    cout << from_root << endl << from_leaf;
}

// Driver code
int main()
{
    int N = 38, X = 3;

    countNodes(N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function to find the count
    // of the required nodes
    static void countNodes(int N, int X)
    {

        // Height of the complete binary
        // tree with n nodes
        int height
            = (int)Math.floor(Math.log(N) / Math.log(2));

        // If X > height then no node
        // can be present at that level
        if (X > height) {
            System.out.println("0\n0");
            return;
        }

        // Corner case
        if (N == 1) {
            System.out.println("1\n1");
            return;
        }

        // Maximum total nodes that are possible
        // in complete binary tree with height h
        int max_total_nodes = (1 << (height + 1)) - 1;

        // Nodes at the last level
        int nodes_last_level
            = (1 << height) - (max_total_nodes - N);

        // To store the count of nodes
        // x dist away from root
        int from_root;

        // To store the count of nodes
        // x dist away from leaf
        int from_leaf;

        // If X = h then print nodes at last level
        // else nodes at Xth level
        if (X == height)
            from_root = nodes_last_level;

        // 2^X
        else
            from_root = 1 << X;

        // Number of left leaf nodes at (h-1)th level
        // observe that if nodes are not present at last
        // level then there are a/2 leaf nodes at (h-1)th
        // level
        int left_leaf_nodes
            = ((1 << height) - nodes_last_level) / 2;

        // If X = h then print leaf nodes at the last h
        // level
        // + leaf nodes at (h-1)th level
        if (X == 0) {
            from_leaf = nodes_last_level + left_leaf_nodes;
        }
        else {

            // First calculate nodes for leaves present at
            // height h
            int i = X;

            while (nodes_last_level > 1 && i > 0) {
                nodes_last_level = (int)Math.ceil(
                    (float)nodes_last_level / (float)2);
                i--;
            }

            from_leaf = nodes_last_level;

            // Then calculate nodes for leaves present at
            // height h-1
            i = X;
            while (left_leaf_nodes > 1 && i > 0) {
                left_leaf_nodes = (int)Math.ceil(
                    (float)left_leaf_nodes / (float)2);
                i--;
            }

            // Add both the results
            from_leaf += left_leaf_nodes;
        }

        System.out.println(from_root + "\n" + from_leaf);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 38, X = 3;
        countNodes(N, X);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import log2, ceil, floor

# Function to find the count
# of the required nodes
def countNodes(N, X):

    # Height of the complete binary
    # tree with n nodes
    height = floor(log2(N))

    # If X > height then no node
    # can be present at that level
    if (X > height):
        print("0\n0")
        return

    # Corner case
    if (N == 1):
        print("1\n1")
        return

    # Maximum total nodes that are possible
    # in complete binary tree with height h
    max_total_nodes = (1 << (height + 1)) - 1

    # Nodes at the last level
    nodes_last_level = (1 << height) - (max_total_nodes - N)

    # To store the count of nodes
    # x dist away from root
    from_root = 0

    # To store the count of nodes
    # x dist away from leaf
    from_leaf = 0

    # If X = h then prnodes at last level
    # else nodes at Xth level
    if (X == height):
        from_root = nodes_last_level

    # 2^X
    else:
        from_root = 1 << X

    # Number of left leaf nodes at (h-1)th level
    # observe that if nodes are not present at last level
    # then there are a/2 leaf nodes at (h-1)th level
    left_leaf_nodes = ((1 << height) - nodes_last_level) // 2

    # If X = h then prleaf nodes at the last h level
    # + leaf nodes at (h-1)th level
    if (X == 0):
        from_leaf = nodes_last_level + left_leaf_nodes
    else:
        # First calculate nodes for leaves present at
        # height h
        i = X

        while (nodes_last_level > 1 and i > 0):
            nodes_last_level = ceil(nodes_last_level / 2)
            i-=1

        from_leaf = nodes_last_level

        # Then calculate nodes for leaves present at height
        # h-1
        i = X
        while (left_leaf_nodes > 1 and i > 0):
            left_leaf_nodes = ceil(left_leaf_nodes / 2)
            i -= 1

        # Add both the results
        from_leaf += left_leaf_nodes

    print(from_root)
    print(from_leaf)

# Driver code
if __name__ == '__main__':
    N, X = 38, 3

    countNodes(N, X)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Function to find the count
// of the required nodes
static void countNodes(int N, int X)
{

    // Height of the complete binary
    // tree with n nodes
    int height = (int)Math.Floor(Math.Log(N) /
                                 Math.Log(2));

    // If X > height then no node
    // can be present at that level
    if (X > height)
    {
        Console.Write("0\n0");
        return;
    }

    // Corner case
    if (N == 1)
    {
        Console.Write("1\n1");
        return;
    }

    // Maximum total nodes that are possible
    // in complete binary tree with height h
    int max_total_nodes = (1 << (height + 1)) - 1;

    // Nodes at the last level
    int nodes_last_level = (1 << height) -
                           (max_total_nodes - N);

    // To store the count of nodes
    // x dist away from root
    int from_root;

    // To store the count of nodes
    // x dist away from leaf
    int from_leaf;

    // If X = h then print nodes at last level
    // else nodes at Xth level
    if (X == height)
        from_root = nodes_last_level;

    // 2^X
    else
        from_root = 1 << X;

    // Number of left leaf nodes at (h-1)th level
    // observe that if nodes are not present at last
    // level then there are a/2 leaf nodes at (h-1)th
    // level
    int left_leaf_nodes = ((1 << height) -
                           nodes_last_level) / 2;

    // If X = h then print leaf nodes at the last h
    // level
    // + leaf nodes at (h-1)th level
    if (X == 0)
    {
        from_leaf = nodes_last_level +
                    left_leaf_nodes;
    }
    else
    {

        // First calculate nodes for leaves present
        // at height h
        int i = X;

        while (nodes_last_level > 1 && i > 0)
        {
            nodes_last_level = (int)Math.Ceiling(
                (float)nodes_last_level / (float)2);

            i--;
        }

        from_leaf = nodes_last_level;

        // Then calculate nodes for leaves present at
        // height h-1
        i = X;
        while (left_leaf_nodes > 1 && i > 0)
        {
            left_leaf_nodes = (int)Math.Ceiling(
                (float)left_leaf_nodes / (float)2);

            i--;
        }

        // Add both the results
        from_leaf += left_leaf_nodes;
    }

    Console.Write(from_root + "\n" + from_leaf);
}

// Driver Code
public static void Main()
{
    int N = 38, X = 3;
    countNodes(N, X);
}
}

// This code is contributed by subham348
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the count
// of the required nodes
function countNodes(N, X)
{

    // Height of the complete binary
    // tree with n nodes
    let height = Math.floor(Math.log(N) /
                            Math.log(2));

    // If X > height then no node
    // can be present at that level
    if (X > height)
    {
        document.write("0<br>0");
        return;
    }

    // Corner case
    if (N == 1)
    {
        document.write("1<br>1");
        return;
    }

    // Maximum total nodes that are possible
    // in complete binary tree with height h
    let max_total_nodes = (1 << (height + 1)) - 1;

    // Nodes at the last level
    let nodes_last_level = (1 << height) -
                           (max_total_nodes - N);

    // To store the count of nodes
    // x dist away from root
    let from_root;

    // To store the count of nodes
    // x dist away from leaf
    let from_leaf;

    // If X = h then print nodes at last level
    // else nodes at Xth level
    if (X == height)
        from_root = nodes_last_level;

    // 2^X
    else
        from_root = 1 << X;

    // Number of left leaf nodes at (h-1)th level
    // observe that if nodes are not present at last
    // level then there are a/2 leaf nodes at (h-1)th
    // level
    let left_leaf_nodes = Math.floor(
        ((1 << height) - nodes_last_level) / 2);

    // If X = h then print leaf nodes at the last h
    // level
    // + leaf nodes at (h-1)th level
    if (X == 0)
    {
        from_leaf = nodes_last_level +
                    left_leaf_nodes;
    }
    else
    {

        // First calculate nodes for leaves
        // present at height h
        let i = X;

        while (nodes_last_level > 1 && i > 0)
        {
            nodes_last_level = Math.floor(Math.ceil(
                nodes_last_level / 2));
            i--;
        }

        from_leaf = nodes_last_level;

        // Then calculate nodes for leaves present at
        // height h-1
        i = X;
        while (left_leaf_nodes > 1 && i > 0)
        {
            left_leaf_nodes = Math.floor(Math.ceil(
                left_leaf_nodes / 2));
            i--;
        }

        // Add both the results
        from_leaf += left_leaf_nodes;
    }
    document.write(from_root + "<br>" + from_leaf);
}

// Driver Code
let N = 38, X = 3;
countNodes(N, X);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
8
3
```

**时间复杂度:** O(log (N))

**辅助空间:** O(1)