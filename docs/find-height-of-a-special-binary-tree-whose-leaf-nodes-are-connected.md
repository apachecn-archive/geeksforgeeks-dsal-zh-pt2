# 求叶节点相连的特殊二叉树的高度

> 原文:[https://www . geeksforgeeks . org/find-一种特殊高度的二叉树，它的叶子节点是相连的/](https://www.geeksforgeeks.org/find-height-of-a-special-binary-tree-whose-leaf-nodes-are-connected/)

给定一棵特殊的二叉树，它的叶节点连接起来形成一个循环的双链表，求它的高度。

例如，

```
         1 
       /   \ 
      2      3 
    /  \ 
   4    5
  /   
 6 
```

在上面的二叉树中，6、5 和 3 是叶节点，它们形成了一个循环双链表。这里，叶节点的左指针将作为循环双链表的前一个指针，其右指针将作为循环双链表的下一个指针。

这个想法是遵循与我们寻找正常二叉树高度相似的方法。我们递归地计算一个节点的左右子树的高度，并将该节点的高度指定为两个子树的最大高度加 1。但是对于普通的二叉树，叶子节点的左右子节点都是空的。但是，这里的叶节点是一个循环双链表节点。因此，对于一个叶节点，我们检查节点的左边右边是否指向该节点，它的右边左边是否也指向该节点本身。

以下是上述想法的实施–

## C++

```
// C++ program to calculate height of a special tree
// whose leaf nodes forms a circular doubly linked list
#include <bits/stdc++.h>
using namespace std;

// A binary tree Node
struct Node {
    int data;
    Node *left, *right;
};

// function to check if given node is a leaf node or node
bool isLeaf(Node* node)
{
    // If given node's left's right is pointing to given
    // node and its right's left is pointing to the node
    // itself then it's a leaf
    return node->left && node->left->right == node
           && node->right && node->right->left == node;
}

/* Compute the height of a tree -- the number of
Nodes along the longest path from the root node
down to the farthest leaf node.*/
int maxDepth(Node* node)
{
    // if node is NULL, return 0
    if (node == NULL)
        return 0;

    // if node is a leaf node, return 1
    if (isLeaf(node))
        return 1;

    // compute the depth of each subtree and take maximum
    return 1
           + max(maxDepth(node->left),
                 maxDepth(node->right));
}

// Helper function that allocates a new tree node
Node* newNode(int data)
{
    Node* node = new Node;
    node->data = data;
    node->left = NULL;
    node->right = NULL;

    return node;
}

// Driver code
int main()
{
    Node* root = newNode(1);

    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->left->left->left = newNode(6);

    // Given tree contains 3 leaf nodes
    Node* L1 = root->left->left->left;
    Node* L2 = root->left->right;
    Node* L3 = root->right;

    // create circular doubly linked list out of
    // leaf nodes of the tree

    // set next pointer of linked list
    L1->right = L2, L2->right = L3, L3->right = L1;

    // set prev pointer of linked list
    L3->left = L2, L2->left = L1, L1->left = L3;

    // calculate height of the tree
    cout << "Height of tree is " << maxDepth(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to calculate height of a special tree
// whose leaf nodes forms a circular doubly linked list
import java.io.*;
import java.util.*;

// User defined node class
class Node {
    int data;
    Node left, right;
    // Constructor to create a new tree node
    Node(int key)
    {
        data = key;
        left = right = null;
    }
}

class GFG {

    // function to check if given node is a leaf node or
    // node
    static boolean isLeaf(Node node)
    {
        // If given node's left's right is pointing to given
        // node and its right's left is pointing to the node
        // itself then it's a leaf
        return (node.left != null && node.left.right == node
                && node.right != null
                && node.right.left == node);
    }
    /* Compute the height of a tree -- the number of
    Nodes along the longest path from the root node
    down to the farthest leaf node.*/
    static int maxDepth(Node node)
    {
        // if node is NULL, return 0
        if (node == null)
            return 0;

        // if node is a leaf node, return 1
        if (isLeaf(node))
            return 1;

        // compute the depth of each subtree and take
        // maximum
        return 1
            + Math.max(maxDepth(node.left),
                       maxDepth(node.right));
    }

    // Driver code
    public static void main(String args[])
    {
        Node root = new Node(1);

        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.left.left.left = new Node(6);

        // Given tree contains 3 leaf nodes
        Node L1 = root.left.left.left;
        Node L2 = root.left.right;
        Node L3 = root.right;

        // create circular doubly linked list out of
        // leaf nodes of the tree

        // set next pointer of linked list
        L1.right = L2;
        L2.right = L3;
        L3.right = L1;

        // set prev pointer of linked list
        L3.left = L2;
        L2.left = L1;
        L1.left = L3;

        // calculate height of the tree
        System.out.println("Height of tree is "
                           + maxDepth(root));
    }
}
// This code is contributed by rachana soma
```

## 蟒蛇 3

```
""" program to Delete a Tree """

# Helper function that allocates a new
# node with the given data and None
# left and right poers.

class newNode:

    # Construct to create a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# function to check if given node is a leaf node or node

def isLeaf(node):

    # If given node's left's right is pointing to given node
    # and its right's left is pointing to the node itself
    # then it's a leaf
    return node.left and node.left.right == node and \
        node.right and node.right.left == node

""" Compute the height of a tree -- the number of 
Nodes along the longest path from the root node 
down to the farthest leaf node."""

def maxDepth(node):

    # if node is None, return 0
    if (node == None):
        return 0

    # if node is a leaf node, return 1
    if (isLeaf(node)):
        return 1

    # compute the depth of each subtree and take maximum
    return 1 + max(maxDepth(node.left), maxDepth(node.right))

# Driver Code
if __name__ == '__main__':
    root = newNode(1)

    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.left.left.left = newNode(6)

    # Given tree contains 3 leaf nodes
    L1 = root.left.left.left
    L2 = root.left.right
    L3 = root.right

    # create circular doubly linked list out of
    # leaf nodes of the tree

    # set next pointer of linked list
    L1.right = L2
    L2.right = L3
    L3.right = L1

    # set prev pointer of linked list
    L3.left = L2
    L2.left = L1
    L1.left = L3

    # calculate height of the tree
    print("Height of tree is ", maxDepth(root))

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# implementation to calculate height of a special tree
// whose leaf nodes forms a circular doubly linked list
using System;

// User defined node class
public class Node {
    public int data;
    public Node left, right;
    // Constructor to create a new tree node
    public Node(int key)
    {
        data = key;
        left = right = null;
    }
}

public class GFG {

    // function to check if given node is a leaf node or
    // node
    static bool isLeaf(Node node)
    {
        // If given node's left's right is pointing to given
        // node and its right's left is pointing to the node
        // itself then it's a leaf
        return (node.left != null && node.left.right == node
                && node.right != null
                && node.right.left == node);
    }
    /* Compute the height of a tree -- the number of
    Nodes along the longest path from the root node
    down to the farthest leaf node.*/
    static int maxDepth(Node node)
    {
        // if node is NULL, return 0
        if (node == null)
            return 0;

        // if node is a leaf node, return 1
        if (isLeaf(node))
            return 1;

        // compute the depth of each subtree and take
        // maximum
        return 1
            + Math.Max(maxDepth(node.left),
                       maxDepth(node.right));
    }

    // Driver code
    public static void Main(String[] args)
    {
        Node root = new Node(1);

        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.left.left.left = new Node(6);

        // Given tree contains 3 leaf nodes
        Node L1 = root.left.left.left;
        Node L2 = root.left.right;
        Node L3 = root.right;

        // create circular doubly linked list out of
        // leaf nodes of the tree

        // set next pointer of linked list
        L1.right = L2;
        L2.right = L3;
        L3.right = L1;

        // set prev pointer of linked list
        L3.left = L2;
        L2.left = L1;
        L1.left = L3;

        // calculate height of the tree
        Console.WriteLine("Height of tree is "
                          + maxDepth(root));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation to calculate height of a special tree
// whose leaf nodes forms a circular doubly linked list
class Node
{
    constructor(key)
    {
        this.data = key;
        this.left = this.right = null;
    }
}

// function to check if given node is a leaf node or
    // node
function isLeaf(node)
{

    // If given node's left's right is pointing to given
        // node and its right's left is pointing to the node
        // itself then it's a leaf
        return (node.left != null && node.left.right == node
                && node.right != null
                && node.right.left == node);
}

/* Compute the height of a tree -- the number of
    Nodes along the longest path from the root node
    down to the farthest leaf node.*/
function maxDepth(node)
{

     // if node is NULL, return 0
        if (node == null)
            return 0;

        // if node is a leaf node, return 1
        if (isLeaf(node))
            return 1;

        // compute the depth of each subtree and take
        // maximum
        return 1
            + Math.max(maxDepth(node.left),
                       maxDepth(node.right));
}

// Driver code
let root = new Node(1);

root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
root.left.left.left = new Node(6);

// Given tree contains 3 leaf nodes
let L1 = root.left.left.left;
let L2 = root.left.right;
let L3 = root.right;

// create circular doubly linked list out of
// leaf nodes of the tree

// set next pointer of linked list
L1.right = L2;
L2.right = L3;
L3.right = L1;

// set prev pointer of linked list
L3.left = L2;
L2.left = L1;
L1.left = L3;

// calculate height of the tree
document.write("Height of tree is "
                   + maxDepth(root));

// This code is contributed by rag2127
</script>
```

**输出:**

```
Height of tree is 4
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。