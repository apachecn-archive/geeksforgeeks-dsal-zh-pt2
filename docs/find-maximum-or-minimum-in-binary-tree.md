# 求二叉树中的最大值(或最小值)

> 原文:[https://www . geesforgeks . org/find-二进制树中的最大值或最小值/](https://www.geeksforgeeks.org/find-maximum-or-minimum-in-binary-tree/)

给定一棵二叉树，找出其中的最大(或最小)元素。例如，以下二叉树中的最大值为 9。

![1T](img/ae2af2a037bc95a8e26f7645a87a1dbc.png)

在二叉查找树，我们可以通过遍历右指针直到到达最右边的节点来找到最大值。但是在二叉树中，我们必须访问每个节点来计算最大值。所以我们的想法是遍历给定的树，对于每个节点返回最大 3 个值。

1.  节点的数据。
2.  节点左子树中的最大值。
3.  节点右子树中的最大值。

下面是上述方法的实现。

## C++

```
// C++ program to find maximum and
// minimum in a Binary Tree
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// A tree node
class Node {
public:
    int data;
    Node *left, *right;

    /* Constructor that allocates a new
    node with the given data and NULL
    left and right pointers. */
    Node(int data)
    {
        this->data = data;
        this->left = NULL;
        this->right = NULL;
    }
};

// Returns maximum value in a given
// Binary Tree
int findMax(Node* root)
{
    // Base case
    if (root == NULL)
        return INT_MIN;

    // Return maximum of 3 values:
    // 1) Root's data 2) Max in Left Subtree
    // 3) Max in right subtree
    int res = root->data;
    int lres = findMax(root->left);
    int rres = findMax(root->right);
    if (lres > res)
        res = lres;
    if (rres > res)
        res = rres;
    return res;
}

// Driver Code
int main()
{
    Node* NewRoot = NULL;
    Node* root = new Node(2);
    root->left = new Node(7);
    root->right = new Node(5);
    root->left->right = new Node(6);
    root->left->right->left = new Node(1);
    root->left->right->right = new Node(11);
    root->right->right = new Node(9);
    root->right->right->left = new Node(4);

    // Function call
    cout << "Maximum element is " << findMax(root) << endl;

    return 0;
}

// This code is contributed by
// rathbhupendra
```

## C

```
// C program to find maximum and minimum in a Binary Tree
#include <limits.h>
#include <stdio.h>
#include <stdlib.h>

// A tree node
struct Node {
    int data;
    struct Node *left, *right;
};

// A utility function to create a new node
struct Node* newNode(int data)
{
    struct Node* node
        = (struct Node*)malloc(sizeof(struct Node));
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Returns maximum value in a given Binary Tree
int findMax(struct Node* root)
{
    // Base case
    if (root == NULL)
        return INT_MIN;

    // Return maximum of 3 values:
    // 1) Root's data 2) Max in Left Subtree
    // 3) Max in right subtree
    int res = root->data;
    int lres = findMax(root->left);
    int rres = findMax(root->right);
    if (lres > res)
        res = lres;
    if (rres > res)
        res = rres;
    return res;
}

// Driver code
int main(void)
{
    struct Node* NewRoot = NULL;
    struct Node* root = newNode(2);
    root->left = newNode(7);
    root->right = newNode(5);
    root->left->right = newNode(6);
    root->left->right->left = newNode(1);
    root->left->right->right = newNode(11);
    root->right->right = newNode(9);
    root->right->right->left = newNode(4);

    // Function call
    printf("Maximum element is %d \n", findMax(root));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to Find maximum (or minimum) in
// Binary Tree

// A binary tree node
class Node {
    int data;
    Node left, right;

    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

class BinaryTree {
    Node root;

    // Returns the max value in a binary tree
    static int findMax(Node node)
    {
        if (node == null)
            return Integer.MIN_VALUE;

        int res = node.data;
        int lres = findMax(node.left);
        int rres = findMax(node.right);

        if (lres > res)
            res = lres;
        if (rres > res)
            res = rres;
        return res;
    }

    /* Driver code */
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(2);
        tree.root.left = new Node(7);
        tree.root.right = new Node(5);
        tree.root.left.right = new Node(6);
        tree.root.left.right.left = new Node(1);
        tree.root.left.right.right = new Node(11);
        tree.root.right.right = new Node(9);
        tree.root.right.right.left = new Node(4);

        // Function call
        System.out.println("Maximum element is "
                           + tree.findMax(tree.root));
    }
}

// This code is contributed by Kamal Rawal
```

## 蟒蛇 3

```
# Python3 program to find maximum
# and minimum in a Binary Tree

# A class to create a new node

class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# Returns maximum value in a
# given Binary Tree

def findMax(root):

    # Base case
    if (root == None):
        return float('-inf')

    # Return maximum of 3 values:
    # 1) Root's data 2) Max in Left Subtree
    # 3) Max in right subtree
    res = root.data
    lres = findMax(root.left)
    rres = findMax(root.right)
    if (lres > res):
        res = lres
    if (rres > res):
        res = rres
    return res

# Driver Code
if __name__ == '__main__':
    root = newNode(2)
    root.left = newNode(7)
    root.right = newNode(5)
    root.left.right = newNode(6)
    root.left.right.left = newNode(1)
    root.left.right.right = newNode(11)
    root.right.right = newNode(9)
    root.right.right.left = newNode(4)

    # Function call
    print("Maximum element is",
          findMax(root))

# This code is contributed by PranchalK
```

## C#

```
// C# code to Find maximum (or minimum) in
// Binary Tree
using System;

// A binary tree node
public class Node {
    public int data;
    public Node left, right;

    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

public class BinaryTree {
    public Node root;

    // Returns the max value in a binary tree
    public static int findMax(Node node)
    {
        if (node == null) {
            return int.MinValue;
        }

        int res = node.data;
        int lres = findMax(node.left);
        int rres = findMax(node.right);

        if (lres > res) {
            res = lres;
        }
        if (rres > res) {
            res = rres;
        }
        return res;
    }

    /* Driver code */
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(2);
        tree.root.left = new Node(7);
        tree.root.right = new Node(5);
        tree.root.left.right = new Node(6);
        tree.root.left.right.left = new Node(1);
        tree.root.left.right.right = new Node(11);
        tree.root.right.right = new Node(9);
        tree.root.right.right.left = new Node(4);

        // Function call
        Console.WriteLine("Maximum element is "
                          + BinaryTree.findMax(tree.root));
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

    // Javascript code to Find maximum (or minimum)
    // in Binary Tree

    let root;

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Returns the max value in a binary tree
    function findMax(node)
    {
        if (node == null)
            return Number.MIN_VALUE;

        let res = node.data;
        let lres = findMax(node.left);
        let rres = findMax(node.right);

        if (lres > res)
            res = lres;
        if (rres > res)
            res = rres;
        return res;
    }

    root = new Node(2);
    root.left = new Node(7);
    root.right = new Node(5);
    root.left.right = new Node(6);
    root.left.right.left = new Node(1);
    root.left.right.right = new Node(11);
    root.right.right = new Node(9);
    root.right.right.left = new Node(4);

    // Function call
    document.write("Maximum element is "
                       + findMax(root));

</script>
```

**Output**

```
Maximum element is 11
```

**Output**

```
Maximum element is 11
```

同样，我们可以通过比较三个值来找到二叉树中的最小元素。下面是在二叉树中寻找最小值的函数。

## C

```
// Returns minimum value in a given Binary Tree
int findMin(struct Node* root)
{
    // Base case
    if (root == NULL)
      return INT_MAX;

    // Return minimum of 3 values:
    // 1) Root's data 2) Max in Left Subtree
    // 3) Max in right subtree
    int res = root->data;
    int lres = findMin(root->left);
    int rres = findMin(root->right);
    if (lres < res)
      res = lres;
    if (rres < res)
      res = rres;
    return res;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Returns the min value in a binary tree
static int findMin(Node node)
{
    if (node == null)
        return Integer.MAX_VALUE;

    int res = node.data;
    int lres = findMin(node.left);
    int rres = findMin(node.right);

    if (lres < res)
        res = lres;
    if (rres < res)
        res = rres;
    return res;
}
```

## 蟒蛇 3

```
# Returns the min value in a binary tree

def find_min_in_BT(root):
    if root is None:
        return float('inf')
    res = root.data
    lres = find_min_in_BT(root.leftChild)
    rres = find_min_in_BT(root.rightChild)
    if lres < res:
        res = lres
    if rres < res:
        res = rres
    return res

# This code is contributed by Subhajit Nandi
```

## C#

```
// Returns the min value in a binary tree
public static int findMin(Node node)
{
    if (node == null)
        return int.MaxValue;

    int res = node.data;
    int lres = findMin(node.left);
    int rres = findMin(node.right);

    if (lres < res)
        res = lres;
    if (rres < res)
        res = rres;
    return res;
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

      // Returns the min value in a binary tree
      function findMin(node) {
        if (node == null) return 2147483647;

        var res = node.data;
        var lres = findMin(node.left);
        var rres = findMin(node.right);

        if (lres < res) res = lres;
        if (rres < res) res = rres;
        return res;
      }

</script>
```

## C++

```
int findMin(Node *root)
    {
        //code
        if(root==NULL)
     {
         return INT_MAX;
     }
       int res=root->data;
       int left=findMin(root->left);
       int right=findMin(root->right);
       if(left<res)
       {
           res=left;
       }
       if(right<res)
       {
           res=right;
       }
       return res;
    }
```

**<u>复杂度分析:</u>**

**时间复杂度:** O(N)。
在递归函数调用中，树的每个节点都被处理一次，因此如果树中总共有 N 个节点，函数的复杂度为 O(N)。因此，时间复杂度为 O(N)。

**空间复杂度:** O(N)。
递归调用正在发生。每个节点处理一次，考虑堆栈空间，空间复杂度为 O(N)。

？list = plqm 7 alhxfyshcxd 7r 1j0ky 9 ZG _ gbb 1 dbk〖t0〗]

本文由**希曼舒·古普塔**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。