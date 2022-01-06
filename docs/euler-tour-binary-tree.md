# 二叉树欧拉游

> 原文:[https://www.geeksforgeeks.org/euler-tour-binary-tree/](https://www.geeksforgeeks.org/euler-tour-binary-tree/)

给定一个二叉树，其中每个节点最多可以有两个子节点，任务是找到二叉树的欧拉之旅。欧拉漫游由指向树中最顶端节点的指针表示。如果树为空，则根的值为空。
示例:

> 输入:
> 
> ![](img/04281a82f60049b469618610ce545360.png)
> 
> 输出:1 5 4 2 4 3 4 5 1

**进场:**

> ![](img/7f6906e6c73e267c3d3c6c9ba95d0863.png)
> 
> (1)首先从根节点 1 开始，**欧拉[0]=1**
> (2)转到左节点即节点 5，**欧拉[1]=5**
> (3)转到左节点即节点 4，**欧拉[2]=4**
> (4)转到左节点即节点 2，**欧拉[3]=2**
> (5)转到左节点即 e，NULL，即 节点 4 **欧拉[6]=4**
> (8)所有子节点被发现，转到父节点 5 **欧拉[7]=5**
> (9)所有子节点被发现，转到父节点 1 **欧拉[8]=1**

[树的欧拉旅行](https://www.geeksforgeeks.org/euler-tour-tree/)已经讨论过了，它可以应用于由邻接表表示的 N 元树。如果二叉树用经典的结构化方式用链接和节点来表示，那么首先需要将树转换成邻接表表示，然后如果我们想应用原文章中讨论的方法，我们可以找到欧拉旅行。但这增加了程序的空间复杂性。在这篇文章中，讨论了一个广义的空间优化版本，它可以直接应用于由结构节点表示的二叉树。
此方法:
(1)不使用访问数组也能工作。
(2)需要恰好 2*N-1 个顶点来存储欧拉漫游。

## C++

```
// C++ program to find euler tour of binary tree
#include <bits/stdc++.h>
using namespace std;

/* A tree node structure */
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

/* Utility function to create a new Binary Tree node */
struct Node* newNode(int data)
{
    struct Node* temp = new struct Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Find Euler Tour
void eulerTree(struct Node* root, vector<int> &Euler)
{
    // store current node's data
    Euler.push_back(root->data);

    // If left node exists
    if (root->left)
    {
        // traverse left subtree
        eulerTree(root->left, Euler);

        // store parent node's data
        Euler.push_back(root->data);
    }

    // If right node exists
    if (root->right)
    {
        // traverse right subtree
        eulerTree(root->right, Euler);

        // store parent node's data
        Euler.push_back(root->data);
    }
}

// Function to print Euler Tour of tree
void printEulerTour(Node *root)
{
    // Stores Euler Tour
    vector<int> Euler;

    eulerTree(root, Euler);

    for (int i = 0; i < Euler.size(); i++)
        cout << Euler[i] << " ";
}

/* Driver function to test above functions */
int main()
{
    // Constructing tree given in the above figure
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->right->left->right = newNode(8);

    // print Euler Tour
    printEulerTour(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find euler tour of binary tree
import java.util.*;

class GFG
{

    /* A tree node structure */
    static class Node
    {
        int data;
        Node left;
        Node right;
    };

    /* Utility function to create a new Binary Tree node */
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.left = temp.right = null;
        return temp;
    }

    // Find Euler Tour
    static Vector<Integer> eulerTree(Node root, Vector<Integer> Euler)
    {
        // store current node's data
        Euler.add(root.data);

        // If left node exists
        if (root.left != null)
        {
            // traverse left subtree
            Euler = eulerTree(root.left, Euler);

            // store parent node's data
            Euler.add(root.data);
        }

        // If right node exists
        if (root.right != null)
        {
            // traverse right subtree
            Euler = eulerTree(root.right, Euler);

            // store parent node's data
            Euler.add(root.data);
        }
        return Euler;
    }

    // Function to print Euler Tour of tree
    static void printEulerTour(Node root)
    {
        // Stores Euler Tour
        Vector<Integer> Euler = new Vector<Integer>();

        Euler = eulerTree(root, Euler);

        for (int i = 0; i < Euler.size(); i++)
            System.out.print(Euler.get(i) + " ");
    }

    /* Driver function to test above functions */
    public static void main(String[] args)
    {
        // Constructing tree given in the above figure
        Node root = newNode(1);
        root.left = newNode(2);
        root.right = newNode(3);
        root.left.left = newNode(4);
        root.left.right = newNode(5);
        root.right.left = newNode(6);
        root.right.right = newNode(7);
        root.right.left.right = newNode(8);

        // print Euler Tour
        printEulerTour(root);

    }
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# program to find euler tour of binary tree
using System;
using System.Collections.Generic;

class GFG
{

    /* A tree node structure */
    public class Node
    {
        public int data;
        public Node left;
        public Node right;
    };

    /* Utility function to create a new Binary Tree node */
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.left = temp.right = null;
        return temp;
    }

    // Find Euler Tour
    static List<int> eulerTree(Node root, List<int> Euler)
    {
        // store current node's data
        Euler.Add(root.data);

        // If left node exists
        if (root.left != null)
        {
            // traverse left subtree
            Euler = eulerTree(root.left, Euler);

            // store parent node's data
            Euler.Add(root.data);
        }

        // If right node exists
        if (root.right != null)
        {
            // traverse right subtree
            Euler = eulerTree(root.right, Euler);

            // store parent node's data
            Euler.Add(root.data);
        }
        return Euler;
    }

    // Function to print Euler Tour of tree
    static void printEulerTour(Node root)
    {
        // Stores Euler Tour
        List<int> Euler = new List<int>();

        Euler = eulerTree(root, Euler);

        for (int i = 0; i < Euler.Count; i++)
            Console.Write(Euler[i] + " ");
    }

    /* Driver function to test above functions */
    public static void Main(String[] args)
    {
        // Constructing tree given in the above figure
        Node root = newNode(1);
        root.left = newNode(2);
        root.right = newNode(3);
        root.left.left = newNode(4);
        root.left.right = newNode(5);
        root.right.left = newNode(6);
        root.right.right = newNode(7);
        root.right.left.right = newNode(8);

        // print Euler Tour
        printEulerTour(root);

    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find euler tour of binary tree
/* A tree node structure */
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

/* Utility function to create a new Binary Tree node */
function newNode(data)
{
    var temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}
// Find Euler Tour
function eulerTree(root, Euler)
{
    // store current node's data
    Euler.push(root.data);

    // If left node exists
    if (root.left != null)
    {
        // traverse left subtree
        Euler = eulerTree(root.left, Euler);

        // store parent node's data
        Euler.push(root.data);
    }

    // If right node exists
    if (root.right != null)
    {
        // traverse right subtree
        Euler = eulerTree(root.right, Euler);

        // store parent node's data
        Euler.push(root.data);
    }
    return Euler;
}

// Function to print Euler Tour of tree
function printEulerTour(root)
{

    // Stores Euler Tour
    var Euler = [];
    Euler = eulerTree(root, Euler);
    for (var i = 0; i < Euler.length; i++)
        document.write(Euler[i] + " ");
}

/* Driver function to test above functions */
// Constructing tree given in the above figure
var root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.left = newNode(4);
root.left.right = newNode(5);
root.right.left = newNode(6);
root.right.right = newNode(7);
root.right.left.right = newNode(8);

// print Euler Tour
printEulerTour(root);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
1 2 4 2 5 2 1 3 6 8 6 3 7 3 1
```

**时间复杂度:** O(2*N-1)，其中 N 为树中的节点数。
**辅助空间:** O(2*N-1)，其中 N 为树中节点数。