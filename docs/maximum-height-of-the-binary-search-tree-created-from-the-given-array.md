# 从给定数组创建的二叉查找树的最大高度

> 原文:[https://www . geeksforgeeks . org/从给定数组创建的二进制搜索树的最大高度/](https://www.geeksforgeeks.org/maximum-height-of-the-binary-search-tree-created-from-the-given-array/)

给定一个数组**arr[]****N**整数，任务是制作两个二分搜索法树。一个从数组的左侧遍历，另一个从右侧遍历，找出哪棵树的高度更高。
**例:**

```
Input: arr[] = {2, 1, 3, 4}
Output: 0
BST starting from first index           BST starting from last index 
    2                                             4
   / \                                           /
  1   3                                         3
       \                                       /
        4                                     1
                                               \
                                                2

Input: arr[] = {1, 2, 6, 3, 5}
Output: 1
```

**先决条件:** [在二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)中插入节点[找到二叉树](https://www.geeksforgeeks.org/write-a-c-program-to-find-the-maximum-depth-or-height-of-a-tree/)的高度。
**进场:**

*   创建一个二叉查找树，同时插入从数组的第一个元素开始到最后一个元素的节点，找到这个创建的树的高度，说 **leftHeight** 。
*   创建另一个二叉查找树，同时插入从数组的最后一个元素开始直到第一个元素的节点，并找到这个创建的树的高度，说 **rightHeight** 。
*   打印这些计算高度的最大值，即**最大值(左高度，右高度)**

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

struct node {
    int key;
    struct node *left, *right;
};

// A utility function to create a new BST node
struct node* newNode(int item)
{
    struct node* temp = (struct node*)malloc(sizeof(struct node));
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

/* A utility function to insert a new node with given key in BST */
struct node* insert(struct node* node, int key)
{
    /* If the tree is empty, return a new node */
    if (node == NULL)
        return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node->key)
        node->left = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);

    /* return the (unchanged) node pointer */
    return node;
}

/* Compute the "maxDepth" of a tree -- the number of
    nodes along the longest path from the root node
    down to the farthest leaf node.*/
int maxDepth(node* node)
{
    if (node == NULL)
        return 0;
    else {
        /* compute the depth of each subtree */
        int lDepth = maxDepth(node->left);
        int rDepth = maxDepth(node->right);

        /* use the larger one */
        if (lDepth > rDepth)
            return (lDepth + 1);
        else
            return (rDepth + 1);
    }
}

// Function to return the maximum
// heights among the BSTs
int maxHeight(int a[], int n)
{
    // Create a BST starting from
    // the first element
    struct node* rootA = NULL;
    rootA = insert(rootA, a[0]);
    for (int i = 1; i < n; i++)
        insert(rootA, a[i]);

    // Create another BST starting
    // from the last element
    struct node* rootB = NULL;
    rootB = insert(rootB, a[n - 1]);
    for (int i = n - 2; i >= 0; i--)
        insert(rootB, a[i]);

    // Find the heights of both the trees
    int A = maxDepth(rootA) - 1;
    int B = maxDepth(rootB) - 1;

    return max(A, B);
}

// Driver code
int main()
{
    int a[] = { 2, 1, 3, 4 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << maxHeight(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static class node
{
    int key;
    node left, right;
};

// A utility function to create a new BST node
static node newNode(int item)
{
    node temp = new node();
    temp.key = item;
    temp.left = temp.right = null;
    return temp;
}

/* A utility function to insert
a new node with given key in BST */
static node insert(node node, int key)
{
    /* If the tree is empty,
    return a new node */
    if (node == null)
        return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node.key)
        node.left = insert(node.left, key);
    else if (key > node.key)
        node.right = insert(node.right, key);

    /* return the (unchanged) node pointer */
    return node;
}

/* Compute the "maxDepth" of a tree --
the number of nodes along the longest path
from the root node down to the farthest leaf node.*/
static int maxDepth(node node)
{
    if (node == null)
        return 0;
    else
    {

        /* compute the depth of each subtree */
        int lDepth = maxDepth(node.left);
        int rDepth = maxDepth(node.right);

        /* use the larger one */
        if (lDepth > rDepth)
            return (lDepth + 1);
        else
            return (rDepth + 1);
    }
}

// Function to return the maximum
// heights among the BSTs
static int maxHeight(int a[], int n)
{
    // Create a BST starting from
    // the first element
    node rootA = null;
    rootA = insert(rootA, a[0]);
    for (int i = 1; i < n; i++)
        rootA = insert(rootA, a[i]);

    // Create another BST starting
    // from the last element
    node rootB = null;
    rootB = insert(rootB, a[n - 1]);
    for (int i = n - 2; i >= 0; i--)
        rootB =insert(rootB, a[i]);

    // Find the heights of both the trees
    int A = maxDepth(rootA) - 1;
    int B = maxDepth(rootB) - 1;

    return Math.max(A, B);
}

// Driver code
public static void main(String args[])
{
    int a[] = { 2, 1, 3, 4 };
    int n = a.length;

    System.out.println(maxHeight(a, n));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python implementation of the approach

class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

# A utility function to insert
# a new node with given key in BST */
def insert(node: Node, key: int) -> Node:

    # If the tree is empty,
    # return a new node */
    if node is None:
        return Node(key)
    # Otherwise, recur down the tree
    if key < node.key:
        node.left = insert(node.left, key)
    elif key > node.key:
        node.right = insert(node.right, key)

    # return the (unchanged) node pointer
    return node

# Compute the "maxDepth" of a tree --
# the number of nodes along the longest path
# from the root node down to the farthest leaf node.*/
def maxDepth(node: Node) -> int:
    if node is None:
        return 0
    else:

        # compute the depth of each subtree
        lDepth = maxDepth(node.left)
        rDepth = maxDepth(node.right)

        # use the larger one
        if lDepth > rDepth:
            return lDepth + 1
        else:
            return rDepth + 1

# Function to return the maximum
# heights among the BSTs
def maxHeight(a: list, n: int) -> int:

    # Create a BST starting from
    # the first element
    rootA = Node(a[0])
    for i in range(1, n):
        rootA = insert(rootA, a[i])

    # Create another BST starting
    # from the last element
    rootB = Node(a[n - 1])
    for i in range(n - 2, -1, -1):
        rootB = insert(rootB, a[i])

    # Find the heights of both the trees
    A = maxDepth(rootA) - 1
    B = maxDepth(rootB) - 1

    return max(A, B)

# Driver Code
if __name__ == "__main__":
    a = [2, 1, 3, 4]
    n = len(a)

    print(maxHeight(a, n))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    public class node
    {
        public int key;
        public node left, right;
    };

    // A utility function to create a new BST node
    static node newNode(int item)
    {
        node temp = new node();
        temp.key = item;
        temp.left = temp.right = null;
        return temp;
    }

    /* A utility function to insert
    a new node with given key in BST */
    static node insert(node node, int key)
    {
        /* If the tree is empty,
        return a new node */
        if (node == null)
            return newNode(key);

        /* Otherwise, recur down the tree */
        if (key < node.key)
            node.left = insert(node.left, key);
        else if (key > node.key)
            node.right = insert(node.right, key);

        /* return the (unchanged) node pointer */
        return node;
    }

    /* Compute the "maxDepth" of a tree --
    the number of nodes along the longest path
    from the root node down to the farthest leaf node.*/
    static int maxDepth(node node)
    {
        if (node == null)
            return 0;
        else
        {

            /* compute the depth of each subtree */
            int lDepth = maxDepth(node.left);
            int rDepth = maxDepth(node.right);

            /* use the larger one */
            if (lDepth > rDepth)
                return (lDepth + 1);
            else
                return (rDepth + 1);
        }
    }

    // Function to return the maximum
    // heights among the BSTs
    static int maxHeight(int []a, int n)
    {
        // Create a BST starting from
        // the first element
        node rootA = null;
        rootA = insert(rootA, a[0]);
        for (int i = 1; i < n; i++)
            rootA = insert(rootA, a[i]);

        // Create another BST starting
        // from the last element
        node rootB = null;
        rootB = insert(rootB, a[n - 1]);
        for (int i = n - 2; i >= 0; i--)
            rootB =insert(rootB, a[i]);

        // Find the heights of both the trees
        int A = maxDepth(rootA) - 1;
        int B = maxDepth(rootB) - 1;

        return Math.Max(A, B);
    }

    // Driver code
    public static void Main()
    {
        int []a = { 2, 1, 3, 4 };
        int n = a.Length;

        Console.WriteLine(maxHeight(a, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
class node
{
    constructor()
    {
        this.key = 0;
        this.left = null;
        this.right = null;
    }
};

// A utility function to create a new BST node
function newNode(item)
{
    var temp = new node();
    temp.key = item;
    temp.left = temp.right = null;
    return temp;
}

/* A utility function to insert
a new node with given key in BST */
function insert(node, key)
{
    /* If the tree is empty,
    return a new node */
    if (node == null)
        return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node.key)
        node.left = insert(node.left, key);
    else if (key > node.key)
        node.right = insert(node.right, key);

    /* return the (unchanged) node pointer */
    return node;
}

/* Compute the "maxDepth" of a tree --
the number of nodes along the longest path
from the root node down to the farthest leaf node.*/
function maxDepth(node)
{
    if (node == null)
        return 0;
    else
    {

        /* compute the depth of each subtree */
        var lDepth = maxDepth(node.left);
        var rDepth = maxDepth(node.right);

        /* use the larger one */
        if (lDepth > rDepth)
            return (lDepth + 1);
        else
            return (rDepth + 1);
    }
}

// Function to return the maximum
// heights among the BSTs
function maxHeight(a, n)
{
    // Create a BST starting from
    // the first element
    var rootA = null;
    rootA = insert(rootA, a[0]);
    for (var i = 1; i < n; i++)
        rootA = insert(rootA, a[i]);

    // Create another BST starting
    // from the last element
    var rootB = null;
    rootB = insert(rootB, a[n - 1]);
    for (var i = n - 2; i >= 0; i--)
        rootB =insert(rootB, a[i]);

    // Find the heights of both the trees
    var A = maxDepth(rootA) - 1;
    var B = maxDepth(rootB) - 1;

    return Math.max(A, B);
}

// Driver code
var a = [2, 1, 3, 4];
var n = a.length;
document.write(maxHeight(a, n));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
3
```