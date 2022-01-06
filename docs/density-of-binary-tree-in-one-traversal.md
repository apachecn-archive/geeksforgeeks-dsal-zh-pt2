# 二叉树一次遍历的密度

> 原文:[https://www . geeksforgeeks . org/二叉树遍历密度/](https://www.geeksforgeeks.org/density-of-binary-tree-in-one-traversal/)

给定一棵二叉树，通过遍历它找到它的密度。

```
Density of Binary Tree = Size / Height 
```

**示例:**

```
Input: Root of following tree
   10
  /   \
 20   30

Output: 1.5
Height of given tree = 2
Size of given tree = 3

Input: Root of following tree
     10
    /   
   20   
 /
30
Output: 1
Height of given tree = 3
Size of given tree = 3 
```

二叉树的密度表示二叉树有多平衡。例如，偏斜树的密度最小，而完美树的密度最大。
**我们强烈建议你尽量减少浏览器，先自己试试这个。**
基于两次遍历的方法很简单。首先使用一次遍历找到高度，然后使用另一次遍历找到大小。最后返回两个值的比值。
在一次遍历中，我们计算二叉树的大小，同时找到它的高度。下面是 C++实现。

## C++

```
//C++ program to find density of a binary tree
#include<bits/stdc++.h>

// A binary tree node
struct Node
{
    int data;
    Node *left, *right;
};

// Helper function to allocates a new node
Node* newNode(int data)
{
    Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

// Function to compute height and
// size of a binary tree
int heighAndSize(Node* node, int &size)
{
    if (node==NULL)
        return 0;

    // compute height of each subtree
    int l = heighAndSize(node->left, size);
    int r = heighAndSize(node->right, size);

    //increase size by 1
    size++;

    //return larger of the two
    return (l > r) ? l + 1 : r + 1;
}

//function to calculate density of a binary tree
float density(Node* root)
{
    if (root == NULL)
        return 0;

    int size = 0; // To store size

    // Finds height and size
    int _height = heighAndSize(root, size);

    return (float)size/_height;
}

// Driver code to test above methods
int main()
{
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);

    printf("Density of given binary tree is %f",
           density(root));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find density of Binary Tree

// A binary tree node
class Node
{
    int data;
    Node left, right;

    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

// Class to implement pass by reference of size
class Size
{
    // variable to calculate size of tree
    int size = 0;
}

class BinaryTree
{
    Node root;

    // Function to compute height and
    // size of a binary tree
    int heighAndSize(Node node, Size size)
    {
        if (node == null)
            return 0;

        // compute height of each subtree
        int l = heighAndSize(node.left, size);
        int r = heighAndSize(node.right, size);

        //increase size by 1
        size.size++;

        //return larger of the two
        return (l > r) ? l + 1 : r + 1;
    }

    //function to calculate density of a binary tree
    float density(Node root)
    {
        Size size = new Size();
        if (root == null)
            return 0;

        // Finds height and size
        int _height = heighAndSize(root, size);

        return (float) size.size / _height;
    }

    // Driver code to test above methods
    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);

        System.out.println("Density of given Binary Tree is : "
                + tree.density(tree.root));
    }

}

// This code has been contributed by Mayank Jaiswal(mayank_24)
```

## 蟒蛇 3

```
# Python3 program to find density
# of a binary tree

# A binary tree node
# Helper function to allocates a new node
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# Function to compute height and
# size of a binary tree
def heighAndSize(node, size):

    if (node == None) :
        return 0

    # compute height of each subtree
    l = heighAndSize(node.left, size)
    r = heighAndSize(node.right, size)

    #increase size by 1
    size[0] += 1

    # return larger of the two
    return l + 1 if(l > r) else r + 1

# function to calculate density
# of a binary tree
def density(root):

    if (root == None) :
        return 0

    size = [0] # To store size

    # Finds height and size
    _height = heighAndSize(root, size)

    return size[0] / _height

# Driver Code
if __name__ == '__main__':
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)

    print("Density of given binary tree is ",
                               density(root))

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// C# program to find density
// of Binary Tree
using System;

// A binary tree node
class Node
{
    public int data;
    public Node left, right;

    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

// Class to implement pass
// by reference of size
class Size
{
    // variable to calculate
    // size of tree
    public int size = 0;
}

class BinaryTree
{
Node root;

// Function to compute height
// and size of a binary tree
int heighAndSize(Node node,
                 Size size)
{
    if (node == null)
        return 0;

    // compute height of each subtree
    int l = heighAndSize(node.left, size);
    int r = heighAndSize(node.right, size);

    //increase size by 1
    size.size++;

    //return larger of the two
    return (l > r) ? l + 1 : r + 1;
}

// function to calculate density
// of a binary tree
float density(Node root)
{
    Size size = new Size();
    if (root == null)
        return 0;

    // Finds height and size
    int _height = heighAndSize(root, size);

    return (float) size.size / _height;
}

// Driver code
static public void Main(String []args)
{
    BinaryTree tree = new BinaryTree();
    tree.root = new Node(1);
    tree.root.left = new Node(2);
    tree.root.right = new Node(3);

    Console.WriteLine("Density of given " +
                      "Binary Tree is : " +
                  tree.density(tree.root));
}
}

// This code is contributed
// by Arnab Kundu
```

## java 描述语言

```
<script>

// javascript program to find density
// of Binary Tree

// A binary tree node
class Node
{
  constructor(data)
  {
    this.data = data;
    this.left = null;
    this.right = null;
  }
}

// Class to implement pass
// by reference of size
class Size
{
  constructor()
  {
    // variable to calculate
    // size of tree
    this.size = 0;
  }
}

var root = null;

// Function to compute height
// and size of a binary tree
function heighAndSize(node, size)
{
    if (node == null)
        return 0;

    // compute height of each subtree
    var l = heighAndSize(node.left, size);
    var r = heighAndSize(node.right, size);

    //increase size by 1
    size.size++;

    //return larger of the two
    return (l > r) ? l + 1 : r + 1;
}

// function to calculate density
// of a binary tree
function density(root)
{
    var size = new Size();
    if (root == null)
        return 0;

    // Finds height and size
    var _height = heighAndSize(root, size);

    return size.size / _height;
}

// Driver code
root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
document.write("Density of given " +
                  "Binary Tree is : " +
              density(root));

// This code is contributed by itsok.

</script>
```

**输出:**

```
Density of given binary tree is 1.5
```

https://www.youtube.com/watch?v=g

-sapoyroff

**参考:**
[http://www . EEM . anadolu . edu . tr/egermen/EEM %20480/icerik/EEM %20480% 20 算法% 20 和% 20 复杂度%20Week%208.pdf](http://www.eem.anadolu.edu.tr/egermen/EEM%20480/icerik/EEM%20480%20Algorithms%20and%20Complexity%20Week%208.pdf)
本文由 **Aditya Goel** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。