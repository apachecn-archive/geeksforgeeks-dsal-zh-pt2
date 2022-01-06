# 空值二叉树的最大宽度

> 原文:[https://www . geesforgeks . org/空值二叉树的最大宽度/](https://www.geeksforgeeks.org/maximum-width-of-a-binary-tree-with-null-value/)

给定一个由 **N** 节点组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是找到给定树的[最大宽度，其中最大宽度被定义为给定树的每一级所有宽度的最大值。](https://www.geeksforgeeks.org/maximum-width-of-a-binary-tree/)

> 任何级别的树的宽度定义为该级别的两个极端节点之间的节点数，包括中间的空节点。

**示例:**

> **输入:**
> 1
> /\
> 2 3
> /\ \
> 4 5 8
> /\
> 6 7
> **输出:** 4
> **说明:**
> 级别 1 的宽度为 1
> 级别 2 的宽度为 2
> 级别 3 的宽度为 4(因为它在 5 和 8 之间有一个空节点)
> 级别 4 的宽度为 2
> 
> 因此，树的最大宽度是所有宽度的最大值，即 max{1，2，4，2} = 4。
> 
> **输入:**
> **1
> /
> 2
> /
> 3
> **输出:** 1**

****方法:**给定的问题可以通过将[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)表示为[堆](https://www.geeksforgeeks.org/binary-heap/)的数组表示来解决。假设一个节点的索引为 **i** ，那么其子节点的索引为 **(2*i + 1)** 、 **(2*i + 2)** 。现在，对于每一级，找到每一级中最左边的节点和最右边的节点的位置，然后它们之间的差将给出该级的宽度。按照以下步骤解决此问题:**

*   **初始化两个 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) ，比如说 **HMMax** 和 **HMMin** ，存储每一级最左边节点和最右边节点的位置**
*   **创建一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/) **getMaxWidthHelper(root，lvl，i)** ，该函数获取树的根、树的初始起始级别 **0** ，以及树的根节点的初始位置 **0** ，并执行以下步骤:

    *   如果树根为**空**，则返回。
    *   将最左边的节点索引存储在 **HMMin** 中的 **lvl** 级。
    *   将最右边的节点索引存储在 **HMMax** 中的 **lvl** 级。
    *   [通过将 **lvl** 的值更新为 **lvl + 1** 和 **i** 至 **(2*i + 1)** ，递归调用左侧子树的](https://www.geeksforgeeks.org/recursion/)。
    *   [通过将 **lvl** 的值更新为 **lvl + 1** 和 **i** 至 **(2*i + 2)** ，递归调用右子树的](https://www.geeksforgeeks.org/recursion/)。** 
*   **调用函数 **getMaxWidthHelper(根，0，0)** 填充 HashMap。**
*   **完成上述步骤后，在所有可能的等级值 **L** 中打印**的最大值(HMMax(L)–HMMin(L)+1)**。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Tree Node structure
struct Node
{
    int data;
    Node *left, *right;

    // Constructor
    Node(int item)
    {
        data = item;
        left = right = NULL;
    }
};

Node *root;
int maxx = 0;

// Stores the position of leftmost
// and rightmost node in each level
map<int, int> hm_min;
map<int, int> hm_max;

// Function to store the min and the
// max index of each nodes in hashmaps
void getMaxWidthHelper(Node *node,
                       int lvl, int i)
{

    // Base Case
    if (node == NULL)
    {
        return;
    }

    // Stores rightmost node index
    // in the hm_max
    if (hm_max[lvl])
    {
        hm_max[lvl] = max(i, hm_max[lvl]);
    }
    else
    {
        hm_max[lvl] = i;
    }

    // Stores leftmost node index
    // in the hm_min
    if (hm_min[lvl])
    {
        hm_min[lvl] = min(i, hm_min[lvl]);
    }

    // Otherwise
    else
    {
        hm_min[lvl] = i;
    }

    // If the left child of the node
    // is not empty, traverse next
    // level with index = 2*i + 1
    getMaxWidthHelper(node->left, lvl + 1,
                                2 * i + 1);

    // If the right child of the node
    // is not empty, traverse next
    // level with index = 2*i + 2
    getMaxWidthHelper(node->right, lvl + 1,
                                 2 * i + 2);
}

// Function to find the maximum
// width of the tree
int getMaxWidth(Node *root)
{

    // Helper function to fill
    // the hashmaps
    getMaxWidthHelper(root, 0, 0);

    // Traverse to each level and
    // find the maximum width
    for(auto lvl : hm_max)
    {
        maxx = max(maxx, hm_max[lvl.second] -
                         hm_min[lvl.second] + 1);
    }

    // Return the result
    return maxx;
}

// Driver Code
int main()
{

    /*
    Constructed binary tree is:
          1
        /  \
       2    3
     /  \    \
    4   5     8
             /  \
            6   7
     */
    root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->right = new Node(8);
    root->right->right->left = new Node(6);
    root->right->right->right = new Node(7);

    // Function Call
    cout << (getMaxWidth(root));
}

// This code is contributed by mohit kumar 29
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach

import java.util.*;

// Tree Node structure
class Node {
    int data;
    Node left, right;

    // Constructor
    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

// Driver Code
public class Main {

    Node root;
    int maxx = 0;

    // Stores the position of leftmost
    // and rightmost node in each level
    HashMap<Integer, Integer> hm_min
        = new HashMap<>();
    HashMap<Integer, Integer> hm_max
        = new HashMap<>();

    // Function to store the min and the
    // max index of each nodes in hashmaps
    void getMaxWidthHelper(Node node,
                           int lvl, int i)
    {
        // Base Case
        if (node == null) {
            return;
        }

        // Stores rightmost node index
        // in the hm_max
        if (hm_max.containsKey(lvl)) {
            hm_max.put(lvl,
                       Math.max(
                           i, hm_max.get(lvl)));
        }
        else {
            hm_max.put(lvl, i);
        }

        // Stores leftmost node index
        // in the hm_min
        if (hm_min.containsKey(lvl)) {
            hm_min.put(lvl,
                       Math.min(
                           i, hm_min.get(lvl)));
        }

        // Otherwise
        else {
            hm_min.put(lvl, i);
        }

        // If the left child of the node
        // is not empty, traverse next
        // level with index = 2*i + 1
        getMaxWidthHelper(node.left, lvl + 1,
                          2 * i + 1);

        // If the right child of the node
        // is not empty, traverse next
        // level with index = 2*i + 2
        getMaxWidthHelper(node.right, lvl + 1,
                          2 * i + 2);
    }

    // Function to find the maximum
    // width of the tree
    int getMaxWidth(Node root)
    {
        // Helper function to fill
        // the hashmaps
        getMaxWidthHelper(root, 0, 0);

        // Traverse to each level and
        // find the maximum width
        for (Integer lvl : hm_max.keySet()) {
            maxx
                = Math.max(
                    maxx,
                    hm_max.get(lvl)
                        - hm_min.get(lvl) + 1);
        }

        // Return the result
        return maxx;
    }

    // Driver Code
    public static void main(String args[])
    {
        Main tree = new Main();

        /*
        Constructed binary tree is:
              1
            /  \
           2    3
         /  \    \
        4   5     8
                 /  \
                6   7
         */
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.right = new Node(8);
        tree.root.right.right.left = new Node(6);
        tree.root.right.right.right = new Node(7);

        // Function Call
        System.out.println(
            tree.getMaxWidth(
                tree.root));
    }
}
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Tree Node structure
class Node:
    def __init__(self, item):
        self.data = item
        self.left = None
        self.right = None

maxx = 0

# Stores the position of leftmost
# and rightmost node in each level
hm_min = {}
hm_max = {}

# Function to store the min and the
# max index of each nodes in hashmaps
def getMaxWidthHelper(node, lvl, i):
    # Base Case
    if (node == None):
        return
    # Stores rightmost node index
    # in the hm_max
    if (lvl in hm_max):
        hm_max[lvl] = max(i, hm_max[lvl])
    else:
        hm_max[lvl] = i

    # Stores leftmost node index
    # in the hm_min
    if (lvl in hm_min):
        hm_min[lvl] = min(i, hm_min[lvl])

    # Otherwise
    else:
        hm_min[lvl] = i

    # If the left child of the node
    # is not empty, traverse next
    # level with index = 2*i + 1
    getMaxWidthHelper(node.left, lvl + 1, 2 * i + 1)

    # If the right child of the node
    # is not empty, traverse next
    # level with index = 2*i + 2
    getMaxWidthHelper(node.right, lvl + 1, 2 * i + 2)

# Function to find the maximum
# width of the tree
def getMaxWidth(root):
    global maxx
    # Helper function to fill
    # the hashmaps
    getMaxWidthHelper(root, 0, 0)

    # Traverse to each level and
    # find the maximum width
    for lvl in hm_max.keys():
        maxx = max(maxx, hm_max[lvl] - hm_min[lvl] + 1)

    # Return the result
    return maxx

"""
Constructed binary tree is:
      1
    /  \
   2    3
 /  \    \
4   5     8
         /  \
        6   7
"""
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
root.right.right = Node(8)
root.right.right.left = Node(6)
root.right.right.right = Node(7)

# Function Call
print(getMaxWidth(root))

# This code is contributed by decode2207.
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // A Binary Tree Node
    class Node
    {
        public int data;
        public Node left;
        public Node right;

        public Node(int item)
        {
            data = item;
            left = right = null;
        }
    };

    static int maxx = 0;

    // Stores the position of leftmost
    // and rightmost node in each level
    static Dictionary<int, int> hm_min = new Dictionary<int, int>();
    static Dictionary<int, int> hm_max = new Dictionary<int, int>();

    // Function to store the min and the
    // max index of each nodes in hashmaps
    static void getMaxWidthHelper(Node node,
                           int lvl, int i)
    {
        // Base Case
        if (node == null) {
            return;
        }

        // Stores rightmost node index
        // in the hm_max
        if (hm_max.ContainsKey(lvl)) {
            hm_max[lvl] = Math.Max(i, hm_max[lvl]);
        }
        else {
            hm_max[lvl] = i;
        }

        // Stores leftmost node index
        // in the hm_min
        if (hm_min.ContainsKey(lvl)) {
            hm_min[lvl] = Math.Min(i, hm_min[lvl]);
        }

        // Otherwise
        else {
            hm_min[lvl] = i;
        }

        // If the left child of the node
        // is not empty, traverse next
        // level with index = 2*i + 1
        getMaxWidthHelper(node.left, lvl + 1,
                          2 * i + 1);

        // If the right child of the node
        // is not empty, traverse next
        // level with index = 2*i + 2
        getMaxWidthHelper(node.right, lvl + 1,
                          2 * i + 2);
    }

    // Function to find the maximum
    // width of the tree
    static int getMaxWidth(Node root)
    {
        // Helper function to fill
        // the hashmaps
        getMaxWidthHelper(root, 0, 0);

        // Traverse to each level and
        // find the maximum width
        foreach (KeyValuePair<int, int> lvl in hm_max) {
            maxx = Math.Max(maxx, hm_max[lvl.Key] - hm_min[lvl.Key] + 1);
        }

        // Return the result
        return maxx;
    }

  // Driver code
  static void Main()
  {

    /*
    Constructed binary tree is:
          1
        /  \
       2    3
     /  \    \
    4   5     8
             /  \
            6   7
     */
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right.right = new Node(8);
    root.right.right.left = new Node(6);
    root.right.right.right = new Node(7);

    // Function Call
    Console.Write(getMaxWidth(root));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

// Tree Node structure
class Node
{
    constructor(item)
    {
        this.data=item;
        this.left=this.right=null;
    }
}

// Driver Code
let root;
let maxx = 0;

// Stores the position of leftmost
    // and rightmost node in each level
let hm_min=new Map();
let hm_max=new Map();

// Function to store the min and the
    // max index of each nodes in hashmaps
function getMaxWidthHelper(node,lvl,i)
{
    // Base Case
        if (node == null) {
            return;
        }

        // Stores rightmost node index
        // in the hm_max
        if (hm_max.has(lvl)) {
            hm_max.set(lvl,
                       Math.max(
                           i, hm_max.get(lvl)));
        }
        else {
            hm_max.set(lvl, i);
        }

        // Stores leftmost node index
        // in the hm_min
        if (hm_min.has(lvl)) {
            hm_min.set(lvl,
                       Math.min(
                           i, hm_min.get(lvl)));
        }

        // Otherwise
        else {
            hm_min.set(lvl, i);
        }

        // If the left child of the node
        // is not empty, traverse next
        // level with index = 2*i + 1
        getMaxWidthHelper(node.left, lvl + 1,
                          2 * i + 1);

        // If the right child of the node
        // is not empty, traverse next
        // level with index = 2*i + 2
        getMaxWidthHelper(node.right, lvl + 1,
                          2 * i + 2);
}

// Function to find the maximum
    // width of the tree
function getMaxWidth(root)
{
    // Helper function to fill
        // the hashmaps
        getMaxWidthHelper(root, 0, 0);

        // Traverse to each level and
        // find the maximum width
        for (let [lvl, value] of hm_max.entries()) {
            maxx
                = Math.max(
                    maxx,
                    hm_max.get(lvl)
                        - hm_min.get(lvl) + 1);
        }

        // Return the result
        return maxx;
}

// Driver Code
root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
root.right.right = new Node(8);
root.right.right.left = new Node(6);
root.right.right.right = new Node(7);

// Function Call
document.write(getMaxWidth(root));

// This code is contributed by unknown2108

</script>
```

****Output:** 

```
4
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**