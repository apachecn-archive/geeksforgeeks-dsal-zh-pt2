# 具有按位“或”值 K 的二叉树中子树的计数

> 原文:[https://www . geesforgeks . org/二叉树中具有按位或值的子树的计数-k/](https://www.geeksforgeeks.org/count-of-subtrees-in-a-binary-tree-having-bitwise-or-value-k/)

给定一个值 **K** 和一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是找出所有元素的**位“或”**等于 K 的**子树**的数量

**示例:**

```
Input: K = 5, Tree = 2
                    / \
                   1   1
                  / \   \
                 10  5   4

Output:  2

Explanation: 
Subtree 1: 
       5
It has only one element i.e. 5.
So bitwise OR of subtree = 5

Subtree 2:
      1
       \
        4
it has 2 elements and bitwise OR of them is also 5

Input: K = 3, Tree =   4
                      / \
                     3   9
                    / \
                   2   2

Output:  1
```

**进场:**

*   使用预排序遍历递归遍历树。
*   对于每个节点，继续计算其子树的按位或，如下所示:

> 其子树的按位或=(节点左子树的按位或)|(节点右子树的按位或)|(节点值)

*   如果任何子树的按位“或”是 K，则递增计数器变量。
*   将计数器中的值打印为所需计数。

## C++

```
// C++ program to find the count of
// subtrees in a Binary Tree
// having bitwise OR value K

#include <bits/stdc++.h>
using namespace std;

// A binary tree node
struct Node {
    int data;
    struct Node *left, *right;
};

// A utility function to
// allocate a new node
struct Node* newNode(int data)
{
    struct Node* newNode = new Node;
    newNode->data = data;
    newNode->left
        = newNode->right = NULL;
    return (newNode);
}

// Recursive Function to compute the count
int rec(Node* root, int& res, int& k)
{
    // Base Case:
    // If node is NULL, return 0
    if (root == NULL) {
        return 0;
    }

    // Calculating the bitwise OR
    // of the current subtree
    int orr = root->data;
    orr |= rec(root->left, res, k);
    orr |= rec(root->right, res, k);

    // Increment res
    // if xr is equal to k
    if (orr == k) {
        res++;
    }

    // Return the bitwise OR value
    // of the current subtree
    return orr;
}

// Function to find the required count
int FindCount(Node* root, int K)
{
    // Initialize result variable 'res'
    int res = 0;

    // Recursively traverse the tree
    // and compute the count
    rec(root, res, K);

    // return the count 'res'
    return res;
}

// Driver program
int main(void)
{

    /*
       2
      / \
     1   1
    / \   \
   10  5   4
    */

    // Create the binary tree
    // by adding nodes to it
    struct Node* root = newNode(2);
    root->left = newNode(1);
    root->right = newNode(1);
    root->right->right = newNode(4);
    root->left->left = newNode(10);
    root->left->right = newNode(5);

    int K = 5;

    cout << FindCount(root, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of
// subtrees in a Binary Tree
// having bitwise OR value K
import java.io.*;
class GFG
{

    // A binary tree node
    static class Node
    {
        public int data;
        public Node left, right;
    };
    static int res;
    static int k;

    // A utility function to
    // allocate a new node
    static Node newNode(int data)
    {
        Node newNode = new Node();
        newNode.data = data;
        newNode.left = null;
        newNode.right = null;
        return newNode;
    }
    static int rec(Node root)
    {

        // Base Case:
        // If node is null, return 0
        if (root == null)
        {
            return 0;
        }

        // Calculating the XOR
        // of the current subtree
        int xr = (root.data);
        xr |= rec(root.left);
        xr |= rec(root.right);

        // Increment res
        // if xr is equal to k
        if (xr == k)
        {
            res++;
        }

        // Return the XOR value
        // of the current subtree
        return xr;
    }

    // Function to find the required count
    static int findCount(Node root, int K)
    {

        // Initialize result variable 'res'
        res = 0;
        k = K;

        // Recursively traverse the tree
        // and compute the count
        rec(root);

        // Return the count 'res'
        return res;
    }

    // Driver code
    public static void main (String[] args)
    {
        /*
         2
        / \
       1   1
      / \   \
    10   5   4
    */

        // Create the binary tree
        // by adding nodes to it
        Node root = newNode(2);
        root.left = newNode(1);
        root.right = newNode(1);
        root.right.right = newNode(4);
        root.left.left =newNode(10);
        root.left.right = newNode(5);
        int K = 5;
        System.out.println(findCount(root, K));
    }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program to find the count of
# subtrees in a Binary Tree
# having bitwise OR value K

# A binary tree node
class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# A utility function to
# allocate a new node
def newNode(data):

    temp = Node(data)
    return temp

# Recursive Function to compute the count
def rec(root, res, k):

    # Base Case:
    # If node is NULL, return 0
    if (root == None):
        return [0, res];

    # Calculating the bitwise OR
    # of the current subtree
    orr = root.data;
    tmp, res = rec(root.left, res, k);
    orr |= tmp
    tmp, res = rec(root.right, res, k);
    orr |= tmp

    # Increment res
    # if xr is equal to k
    if (orr == k):
        res += 1

    # Return the bitwise OR value
    # of the current subtree
    return orr, res;

# Function to find the required count
def FindCount(root, K):

    # Initialize result variable 'res'
    res = 0;

    # Recursively traverse the tree
    # and compute the count
    tmp,res = rec(root, res, K);

    # return the count 'res'
    return res;

# Driver program
if __name__=='__main__':

    '''
       2
      / \
     1   1
    / \   \
   10  5   4
    '''

    # Create the binary tree
    # by adding nodes to it
    root = newNode(2);
    root.left = newNode(1);
    root.right = newNode(1);
    root.right.right = newNode(4);
    root.left.left = newNode(10);
    root.left.right = newNode(5);

    K = 5;

    print(FindCount(root, K))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find the count of
// subtrees in a Binary Tree
// having bitwise OR value K
using System;

class GFG{

// A binary tree node
class Node
{
    public int data;
    public Node left, right;
};

static int res;
static int k;

// A utility function to
// allocate a new node
static Node newNode(int data)
{
    Node newNode = new Node();
    newNode.data = data;
    newNode.left= null;
    newNode.right = null;
    return newNode;
}

static int rec(Node root)
{

    // Base Case:
    // If node is null, return 0
    if (root == null)
    {
        return 0;
    }

    // Calculating the XOR
    // of the current subtree
    int xr = (root.data);
    xr |= rec(root.left);
    xr |= rec(root.right);

    // Increment res
    // if xr is equal to k
    if (xr == k)
    {
        res++;
    }

    // Return the XOR value
    // of the current subtree
    return xr;
}

// Function to find the required count
static int findCount(Node root, int K)
{

    // Initialize result variable 'res'
    res = 0;
    k = K;

    // Recursively traverse the tree
    // and compute the count
    rec(root);

    // Return the count 'res'
    return res;
}

// Driver code
public static void Main(String []args)
{

    /*
         2
        / \
       1   1
      / \   \
    10   5   4
    */

    // Create the binary tree
    // by adding nodes to it
    Node root = newNode(2);
    root.left = newNode(1);
    root.right = newNode(1);
    root.right.right = newNode(4);
    root.left.left =newNode(10);
    root.left.right = newNode(5);

    int K = 5;

    Console.WriteLine(findCount(root, K));
}
}

// This code is contributed by mohit kumar
```

## java 描述语言

```
<script>

// Javascript program to find the count of
// subtrees in a Binary Tree having bitwise
// OR value K

// Structure of node
class Node
{

    // Utility function to
    // create a new node
    constructor(key)
    {
        this.data = key;
        this.left = this.right = null;
    }
}

let res, k;

function rec(root)
{

    // Base Case:
    // If node is null, return 0
    if (root == null)
    {
        return 0;
    }

    // Calculating the XOR
    // of the current subtree
    let xr = (root.data);
    xr |= rec(root.left);
    xr |= rec(root.right);

    // Increment res
    // if xr is equal to k
    if (xr == k)
    {
        res++;
    }

    // Return the XOR value
    // of the current subtree
    return xr;
}

// Function to find the required count
function findCount(root, K)
{

    // Initialize result variable 'res'
    res = 0;
    k = K;

    // Recursively traverse the tree
    // and compute the count
    rec(root);

    // Return the count 'res'
    return res;
}

// Driver code
/*
         2
        / \
       1   1
      / \   \
    10   5   4
    */

// Create the binary tree
// by adding nodes to it
let root = new Node(2);
root.left = new Node(1);
root.right = new Node(1);
root.right.right = new Node(4);
root.left.left =new Node(10);
root.left.right = new Node(5);

let K = 5;

document.write(findCount(root, K));

// This code is contributed by patel2127

</script>
```

**Output:**

```
2
```

**时间复杂度:**和上面的方法一样，我们只迭代每个节点一次，因此需要 **O(N)** 时间，其中 N 是二叉树中的节点数。

**辅助空间复杂度:**由于在上面的方法中没有使用额外的空间，因此辅助空间复杂度将是 **O(1)** 。