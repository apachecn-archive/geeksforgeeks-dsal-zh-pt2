# 具有异或值 K 的二叉树中的子树的计数

> 原文:[https://www . geesforgeks . org/二叉树中具有 xor 值的子树的计数-k/](https://www.geeksforgeeks.org/count-of-subtrees-in-a-binary-tree-having-xor-value-k/)

给定一个值 **K** 和一个 [**二叉树**](https://www.geeksforgeeks.org/binary-tree-data-structure/) ，任务是找出其所有元素的**异或**等于 **K** 的**子树**的数量。
**示例:**

```
Input  K = 5, Tree =
       2
      / \
     1   9
    / \
   10  5
Output: 2
Explanation:
Subtree 1: 
       5
It has only one element i.e. 5.
So XOR of subtree = 5
Subtree 1: 
       2
      / \
     1   9
    / \
   10  5
It has elements 2, 1, 9, 10, 5.
So XOR of subtree = 2 ^ 1 ^ 9 ^ 10 ^ 5 = 5

Input  K = 3, Tree =
       4
      / \
     3   9
    / \
   2   2
Output: 1
Explanation
Subtree:
     3
    / \
   2   2
It has elements 3, 2, 2.
So XOR of subtree = 3 ^ 2 ^ 2 = 3
```

**接近**T2】

1.  使用[预序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)递归遍历树。
2.  对于每个节点，继续计算其子树的异或:T0

> 它的子树的异或=(节点的左子树的异或)^(节点的右子树的异或)^(节点的值)

2.  如果任意子树的异或为 K，递增计数器变量。
3.  将计数器中的值打印为所需计数

以下是上述方法的实现:

## C++

```
// C++ program to find the count of
// subtrees in a Binary Tree
// having XOR value K

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

int rec(Node* root, int& res, int& k)
{
    // Base Case:
    // If node is NULL, return 0
    if (root == NULL) {
        return 0;
    }

    // Calculating the XOR
    // of the current subtree
    int xr = root->data;
    xr ^= rec(root->left, res, k);
    xr ^= rec(root->right, res, k);

    // Increment res
    // if xr is equal to k
    if (xr == k) {
        res++;
    }

    // Return the XOR value
    // of the current subtree
    return xr;
}

// Function to find the required count
int findCount(Node* root, int K)
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
      1   9
     / \
    10  5
    */

    // Create the binary tree
    // by adding nodes to it
    struct Node* root = newNode(2);
    root->left = newNode(1);
    root->right = newNode(9);
    root->left->left = newNode(10);
    root->left->right = newNode(5);

    int K = 5;

    cout << findCount(root, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of
// subtrees in a Binary Tree
// having XOR value K
import java.util.*;

class GFG{

    // A binary tree node
    static class Node
    {
        int data;
        Node left,right;
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
        if (root == null) {
            return 0;
        }

        // Calculating the XOR
        // of the current subtree
        int xr = (root.data);//^rec(root.left)^rec(root.right);
        xr ^= rec(root.left);
        xr ^= rec(root.right);

        // Increment res
        // if xr is equal to k
        if (xr == k) {
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

        // return the count 'res'
        return res;
    }

    // Driver program
    public static void main(String args[])
    {

        /*
            2
        / \
        1 9
        / \
        10 5
        */

        // Create the binary tree
        // by adding nodes to it
        Node root = newNode(2);
        root.left = newNode(1);
        root.right = newNode(9);
        root.left.left =newNode(10);
        root.left.right = newNode(5);

        int K = 5;

        System.out.println(findCount(root, K));   
    }
}

// This code is contributed by AbhiThakur
```

## 蟒蛇 3

```
# Python3 program to find the count of
# subtrees in a Binary Tree
# having XOR value K

# A binary tree node
class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# A utility function to
# allocate a new node
def newNode(data):

    newNode = Node(data)
    return newNode

def rec(root, res, k):

    # Base Case:
    # If node is None, return 0
    if (root == None):
        return [0, res];

    # Calculating the XOR
    # of the current subtree
    xr = root.data;
    tmp,res = rec(root.left, res, k);
    xr^=tmp
    tmp,res = rec(root.right, res, k);
    xr^=tmp

    # Increment res
    # if xr is equal to k
    if (xr == k):
        res += 1

    # Return the XOR value
    # of the current subtree
    return xr, res;

# Function to find the required count
def findCount(root, K):

    # Initialize result variable 'res'
    res = 0;

    # Recursively traverse the tree
    # and compute the count
    tmp,res=rec(root, res, K);

    # return the count 'res'
    return res;

# Driver program
if __name__=='__main__':

    '''
        2
       / \
      1   9
     / \
    10  5
    '''

    # Create the binary tree
    # by adding nodes to it
    root = newNode(2);
    root.left = newNode(1);
    root.right = newNode(9);
    root.left.left = newNode(10);
    root.left.right = newNode(5);

    K = 5;

    print(findCount(root, K))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find the count of
// subtrees in a Binary Tree
// having XOR value K
using System;

public class GFG{

    // A binary tree node
    class Node
    {
        public int data;
        public Node left,right;
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
        if (root == null) {
            return 0;
        }

        // Calculating the XOR
        // of the current subtree
        int xr = (root.data);//^rec(root.left)^rec(root.right);
        xr ^= rec(root.left);
        xr ^= rec(root.right);

        // Increment res
        // if xr is equal to k
        if (xr == k) {
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

        // return the count 'res'
        return res;
    }

    // Driver program
    public static void Main(String []args)
    {

        /*
            2
        / \
        1 9
        / \
        10 5
        */

        // Create the binary tree
        // by adding nodes to it
        Node root = newNode(2);
        root.left = newNode(1);
        root.right = newNode(9);
        root.left.left =newNode(10);
        root.left.right = newNode(5);

        int K = 5;

        Console.WriteLine(findCount(root, K));   
    }
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// JavaScript program to find the count of
// subtrees in a Binary Tree
// having XOR value K

// A binary tree node
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

var res = 0;
var k = 0;

// A utility function to
// allocate a new node
function newNode(data)
{
    var newNode = new Node();
    newNode.data = data;
    newNode.left= null;
    newNode.right = null;
    return newNode;
}

function rec(root)
{
    // Base Case:
    // If node is null, return 0
    if (root == null) {
        return 0;
    }

    // Calculating the XOR
    // of the current subtree
    var xr = (root.data);//^rec(root.left)^rec(root.right);
    xr ^= rec(root.left);
    xr ^= rec(root.right);

    // Increment res
    // if xr is equal to k
    if (xr == k) {
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

    // return the count 'res'
    return res;
}

// Driver program
/*
    2
/ \
1 9
/ \
10 5
*/

// Create the binary tree
// by adding nodes to it
var root = newNode(2);
root.left = newNode(1);
root.right = newNode(9);
root.left.left =newNode(10);
root.left.right = newNode(5);

var K = 5;

document.write(findCount(root, K));   

</script>
```

**Output:** 

```
2
```

**性能分析:**
**时间复杂度**:和上面的方法一样，我们对每个节点只迭代一次，因此需要 **O(N)** 的时间，其中 **N** 是二叉树中的节点数。
**辅助空间复杂度**:和上述方法一样，没有使用额外的空间，因此辅助空间复杂度为 **O(1)** 。