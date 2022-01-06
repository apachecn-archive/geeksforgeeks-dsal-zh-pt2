# 计算给定异或值的二叉树从根到叶的路径数

> 原文:[https://www . geesforgeks . org/count-给定 xor 值的二叉树从根到叶的路径数/](https://www.geeksforgeeks.org/count-the-number-of-paths-from-root-to-leaf-of-a-binary-tree-with-given-xor-value/)

给定一个**值 K 和一棵二叉树**，我们必须找出从根节点到叶节点的路径总数，其所有节点沿路径异或等于 K。
**示例:**

```
Input: K = 6
       2
      / \
     1   4
    / \   
   10  5   
Output: 2
Explanation:
Subtree 1: 
   2
    \
     4
This particular path has 2 nodes, 2 and 4 
and (2 xor 4) = 6.

Subtree 2:
        2
       /
      1
       \
        5
This particular path has 3 nodes; 2, 1 and 5 
and (2 xor 1 xor 5) = 6.
```

**方法:**
为了解决上面提到的问题，我们必须使用预序遍历递归地遍历树。对于每个节点，继续计算从根到当前节点的路径的异或。

> 当前节点路径的异或=(直到父节点的路径的异或)^(当前节点值)

如果节点是左边的叶节点，并且当前节点的右边的子节点为空，那么我们检查路径的异或值是否为 K，如果是，那么我们增加计数，否则我们什么也不做。最后，打印计数中的值。
以下是上述方法的实现:

## C++

```
// C++ program to Count the number of
// path from the root to leaf of a
// Binary tree with given XOR value

#include <bits/stdc++.h>
using namespace std;

// Binary tree node
struct Node {
    int data;

    struct Node *left, *right;
};

// Function to create a new node
struct Node* newNode(int data)
{
    struct Node* newNode = new Node;

    newNode->data = data;

    newNode->left
        = newNode->right = NULL;

    return (newNode);
}

void Count(Node* root, int xr, int& res, int& k)
{

    // updating the xor value
    // with the xor of the path from
    // root to the node
    xr = xr ^ root->data;

    // check if node is leaf node
    if (root->left == NULL && root->right == NULL) {

        if (xr == k) {
            res++;
        }
        return;
    }

    // check if the left
    // node exist in the tree
    if (root->left != NULL) {
        Count(root->left, xr, res, k);
    }

    // check if the right node
    // exist in the tree
    if (root->right != NULL) {
        Count(root->right, xr, res, k);
    }

    return;
}

// Function to find the required count
int findCount(Node* root, int K)
{

    int res = 0, xr = 0;

    // recursively traverse the tree
    // and compute the count
    Count(root, xr, res, K);

    // return the result
    return res;
}

// Driver code
int main(void)
{
    // Create the binary tree
    struct Node* root = newNode(2);
    root->left = newNode(1);
    root->right = newNode(4);
    root->left->left = newNode(10);
    root->left->right = newNode(5);

    int K = 6;

    cout << findCount(root, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Count the number of
// path from the root to leaf of a
// Binary tree with given XOR value
import java.util.*;

class GFG{

// Binary tree node
static class Node {
    int data;

    Node left, right;
};
static int res, k;

// Function to create a new node
static Node newNode(int data)
{
    Node newNode = new Node();

    newNode.data = data;

    newNode.left
        = newNode.right = null;

    return (newNode);
}

static void Count(Node root, int xr)
{

    // updating the xor value
    // with the xor of the path from
    // root to the node
    xr = xr ^ root.data;

    // check if node is leaf node
    if (root.left == null && root.right == null) {

        if (xr == k) {
            res++;
        }
        return;
    }

    // check if the left
    // node exist in the tree
    if (root.left != null) {
        Count(root.left, xr);
    }

    // check if the right node
    // exist in the tree
    if (root.right != null) {
        Count(root.right, xr);
    }

    return;
}

// Function to find the required count
static int findCount(Node root, int K)
{

    int xr = 0;
    res = 0;
    k = K;

    // recursively traverse the tree
    // and compute the count
    Count(root, xr);

    // return the result
    return res;
}

// Driver code
public static void main(String[] args)
{
    // Create the binary tree
    Node root = newNode(2);
    root.left = newNode(1);
    root.right = newNode(4);
    root.left.left = newNode(10);
    root.left.right = newNode(5);

    int K = 6;

    System.out.print(findCount(root, K));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to Count
# the number of path from
# the root to leaf of a
# Binary tree with given XOR value

# Binary tree node
class Node:
    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

def Count(root : Node,
          xr : int) -> None:

    global K, res

    # Updating the xor value
    # with the xor of the path from
    # root to the node
    xr = xr ^ root.data

    # Check if node is leaf node
    if (root.left is None and
        root.right is None):
        if (xr == K):
            res += 1

        return

    # Check if the left
    # node exist in the tree
    if (root.left):
        Count(root.left, xr)

    # Check if the right node
    # exist in the tree
    if (root.right):
        Count(root.right, xr)

    return

# Function to find the
# required count
def findCount(root : Node) -> int:

    global K, res
    xr = 0

    # Recursively traverse the tree
    # and compute the count
    Count(root, xr)

    # return the result
    return res

# Driver code
if __name__ == "__main__":

    # Create the binary tree
    root = Node(2)
    root.left = Node(1)
    root.right = Node(4)
    root.left.left = Node(10)
    root.left.right = Node(5)

    K = 6
    res = 0
    print(findCount(root))

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to Count the number of
// path from the root to leaf of a
// Binary tree with given XOR value
using System;

class GFG{

// Binary tree node
class Node {
    public int data;

    public Node left, right;
};
static int res, k;

// Function to create a new node
static Node newNode(int data)
{
    Node newNode = new Node();

    newNode.data = data;

    newNode.left
        = newNode.right = null;

    return (newNode);
}

static void Count(Node root, int xr)
{

    // updating the xor value
    // with the xor of the path from
    // root to the node
    xr = xr ^ root.data;

    // check if node is leaf node
    if (root.left == null && root.right == null) {

        if (xr == k) {
            res++;
        }
        return;
    }

    // check if the left
    // node exist in the tree
    if (root.left != null) {
        Count(root.left, xr);
    }

    // check if the right node
    // exist in the tree
    if (root.right != null) {
        Count(root.right, xr);
    }

    return;
}

// Function to find the required count
static int findCount(Node root, int K)
{

    int xr = 0;
    res = 0;
    k = K;

    // recursively traverse the tree
    // and compute the count
    Count(root, xr);

    // return the result
    return res;
}

// Driver code
public static void Main(String[] args)
{
    // Create the binary tree
    Node root = newNode(2);
    root.left = newNode(1);
    root.right = newNode(4);
    root.left.left = newNode(10);
    root.left.right = newNode(5);

    int K = 6;

    Console.Write(findCount(root, K));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to Count the number of
// path from the root to leaf of a
// Binary tree with given XOR value

// Binary tree node
class Node {

    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

var res, k;

// Function to create a new node
function newNode(data)
{
    var newNode = new Node();

    newNode.data = data;

    newNode.left
        = newNode.right = null;

    return (newNode);
}

function Count(root, xr)
{

    // updating the xor value
    // with the xor of the path from
    // root to the node
    xr = xr ^ root.data;

    // check if node is leaf node
    if (root.left == null && root.right == null) {

        if (xr == k) {
            res++;
        }
        return;
    }

    // check if the left
    // node exist in the tree
    if (root.left != null) {
        Count(root.left, xr);
    }

    // check if the right node
    // exist in the tree
    if (root.right != null) {
        Count(root.right, xr);
    }

    return;
}

// Function to find the required count
function findCount(root, K)
{

    var xr = 0;
    res = 0;
    k = K;

    // recursively traverse the tree
    // and compute the count
    Count(root, xr);

    // return the result
    return res;
}

// Driver code
// Create the binary tree
var root = newNode(2);
root.left = newNode(1);
root.right = newNode(4);
root.left.left = newNode(10);
root.left.right = newNode(5);

var K = 6;

document.write(findCount(root, K));

</script>
```

**Output:** 

```
2
```

**时间复杂度:**和上面的方法一样，我们只迭代每个节点一次，因此需要 O(N)个时间，其中 N 是二叉树中的节点数。
**辅助空间:**由于在上面的方法中没有使用额外的空间，因此辅助空间的复杂性将为 0(1)。