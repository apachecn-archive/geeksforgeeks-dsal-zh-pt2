# 二叉树的最大异或路径

> 原文:[https://www . geeksforgeeks . org/二进制树的最大异或路径/](https://www.geeksforgeeks.org/maximum-xor-path-of-a-binary-tree/)

给定一棵 [**二叉树**](https://www.geeksforgeeks.org/binary-tree-data-structure/) ，任务是找出从根到叶路径中所有节点的所有异或值的最大值。
**例:**

```
Input: 
       2
      / \
     1   4
    / \   
   10  8   
Output: 11
Explanation:
All the paths are: 
2-1-10 XOR-VALUE = 9
2-1-8 XOR-VALUE = 11
2-4 XOR-VALUE = 6

Input: 
        2
      /   \
     1     4
    / \   / \
   10  8 5  10
Output: 12
```

**进场:**

1.  为了解决上面提到的问题，我们必须使用预排序遍历递归地遍历树。对于每个节点，继续计算从根到当前节点的路径的异或。

    > 当前节点路径的异或=(直到父节点的路径的异或)^(当前节点值)

2.  如果该节点是左侧的叶节点，并且当前节点的右子节点为空，那么我们计算最大异或，如

    > 最大异或=最大(最大异或，cur-异或)。

以下是上述方法的实现:

## C++

```
// C++ program to compute the
// Max-Xor value of path from
// the root to leaf of a Binary tree

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

// Function calculate the
// value of max-xor
void Solve(Node* root, int xr,
           int& max_xor)
{

    // Updating the xor value
    // with the xor of the
    // path from root to
    // the node
    xr = xr ^ root->data;

    // Check if node is leaf node
    if (root->left == NULL
        && root->right == NULL) {

        max_xor = max(max_xor, xr);
        return;
    }

    // Check if the left
    // node exist in the tree
    if (root->left != NULL) {
        Solve(root->left, xr,
              max_xor);
    }

    // Check if the right node
    // exist in the tree
    if (root->right != NULL) {
        Solve(root->right, xr,
              max_xor);
    }

    return;
}

// Function to find the
// required count
int findMaxXor(Node* root)
{

    int xr = 0, max_xor = 0;

    // Recursively traverse
    // the tree and compute
    // the max_xor
    Solve(root, xr, max_xor);

    // Return the result
    return max_xor;
}

// Driver code
int main(void)
{
    // Create the binary tree
    struct Node* root = newNode(2);
    root->left = newNode(1);
    root->right = newNode(4);
    root->left->left = newNode(10);
    root->left->right = newNode(8);
    root->right->left = newNode(5);
    root->right->right = newNode(10);

    cout << findMaxXor(root);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to compute the 
# Max-Xor value of path from 
# the root to leaf of a Binary tree 

# Binary tree node
class Node:

    # Function to create a new node
    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# Function calculate the 
# value of max-xor
def Solve(root, xr, max_xor):

    # Updating the xor value 
    # with the xor of the 
    # path from root to 
    # the node
    xr = xr ^ root.data

    # Check if node is leaf node
    if (root.left == None and 
        root.right == None):
        max_xor[0] = max(max_xor[0], xr)

    # Check if the left 
    # node exist in the tree
    if root.left != None:
        Solve(root.left, xr, max_xor)

    # Check if the right node 
    # exist in the tree 
    if root.right != None:
        Solve(root.right, xr, max_xor)

    return

# Function to find the 
# required count 
def findMaxXor(root):

    xr, max_xor = 0, [0]

    # Recursively traverse 
    # the tree and compute 
    # the max_xor 
    Solve(root, xr, max_xor)

    # Return the result
    return max_xor[0]

# Driver code

# Create the binary tree
root = Node(2)
root.left = Node(1)
root.right = Node(4) 
root.left.left = Node(10) 
root.left.right = Node(8) 
root.right.left = Node(5) 
root.right.right = Node(10) 

print(findMaxXor(root))

# This code is contributed by Shivam Singh
```

## java 描述语言

```
<script>

// JavaScript program to compute the
// Max-Xor value of path from
// the root to leaf of a Binary tree

// Binary tree node
class Node {

    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// Function to create a new node
function newNode(data)
{
    var newNode = new Node;

    newNode.data = data;

    newNode.left
        = newNode.right = null;

    return (newNode);
}

// Function calculate the
// value of Math.max-xor
function Solve(root, xr, max_xor)
{

    // Updating the xor value
    // with the xor of the
    // path from root to
    // the node
    xr = xr ^ root.data;

    // Check if node is leaf node
    if (root.left == null
        && root.right == null) {

        max_xor = Math.max(max_xor, xr);
        return max_xor;
    }

    // Check if the left
    // node exist in the tree
    if (root.left != null) {
        max_xor = Solve(root.left, xr,
              max_xor);
    }

    // Check if the right node
    // exist in the tree
    if (root.right != null) {
       max_xor = Solve(root.right, xr,
              max_xor);
    }

    return max_xor;
}

// Function to find the
// required count
function findMaxXor(root)
{

    var xr = 0, max_xor = 0;

    // Recursively traverse
    // the tree and compute
    // the max_xor
    max_xor = Solve(root, xr, max_xor);

    // Return the result
    return max_xor;
}

// Driver code
// Create the binary tree
var root = newNode(2);
root.left = newNode(1);
root.right = newNode(4);
root.left.left = newNode(10);
root.left.right = newNode(8);
root.right.left = newNode(5);
root.right.right = newNode(10);
document.write( findMaxXor(root));

</script>
```

**Output:** 

```
12
```

**时间复杂度:**我们只迭代每个节点一次，因此需要 **O(N)** 时间，其中 N 是二叉树中的节点数。
**辅助空间复杂度:**辅助空间复杂度将为 **O(1)** ，因为没有使用额外空间