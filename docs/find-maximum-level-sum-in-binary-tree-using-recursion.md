# 用递归求二叉树中的最大级和

> 原文:[https://www . geeksforgeeks . org/find-最大级别-二进制树求和-使用递归/](https://www.geeksforgeeks.org/find-maximum-level-sum-in-binary-tree-using-recursion/)

给定一个有正节点和负节点的二叉树，任务是找到其中的最大和级别并打印最大和。
**例:**

```
Input:
      4
    /   \
   2     -5
  / \    / \
-1   3 -2   6
Output: 6
Sum of all nodes of the 1st level is 4.
Sum of all nodes of the 2nd level is -3.
Sum of all nodes of the 3rd level is 6.
Hence, the maximum sum is 6.

Input:
      1
    /   \
   2      3
 /  \      \
4    5      8
          /   \
         6     7  
Output: 17
```

**方法:**在给定的二叉树中找到最大级别，然后创建一个数组 **sum[]** ，其中 **sum[i]** 将存储级别为 **i** 的元素的总和。
现在，编写一个递归函数，该函数以树的一个节点及其级别为参数，更新当前级别的总和，然后递归调用更新级别比当前级别多一级的子级(这是因为子级比它们的父级多一级)。最后，打印 **sum[]** 数组中的最大值。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// A binary tree node has data, pointer to
// the left child and the right child
struct Node {
    int data;
    struct Node *left, *right;
};

// Helper function that allocates a
// new node with the given data and
// NULL left and right pointers
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Function to return the maximum
// levels in the given tree
int maxLevel(struct Node* root)
{
    if (root == NULL)
        return 0;
    return (1 + max(maxLevel(root->left),
                    maxLevel(root->right)));
}

// Function to find the maximum sum of a
// level in the tree using recursion
void maxLevelSum(struct Node* root, int max_level,
                 int sum[], int current)
{
    // Base case
    if (root == NULL)
        return;

    // Add current node's data to
    // its level's sum
    sum[current] += root->data;

    // Recursive call for the left child
    maxLevelSum(root->left, max_level, sum,
                current + 1);

    // Recursive call for the right child
    maxLevelSum(root->right, max_level, sum,
                current + 1);
}

// Function to find the maximum sum of a
// level in the tree using recursion
int maxLevelSum(struct Node* root)
{

    // Maximum levels in the given tree
    int max_level = maxLevel(root);

    // To store the sum of every level
    int sum[max_level + 1] = { 0 };

    // Recursive function call to
    // update the sum[] array
    maxLevelSum(root, max_level, sum, 1);

    // To store the maximum sum for a level
    int maxSum = 0;

    // For every level of the tree, update
    // the maximum sum of a level so far
    for (int i = 1; i <= max_level; i++)
        maxSum = max(maxSum, sum[i]);

    // Return the maximum sum
    return maxSum;
}

// Driver code
int main()
{
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->right = newNode(8);
    root->right->right->left = newNode(6);
    root->right->right->right = newNode(7);

    /* Constructed Binary tree is:
                1
               / \
              2   3
             / \   \
            4   5   8
                   / \
                  6   7   */

    cout << maxLevelSum(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// A binary tree node has data, pointer to
// the left child and the right child
static class Node
{
    int data;
    Node left, right;
};

// Helper function that allocates a
// new node with the given data and
// null left and right pointers
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Function to return the maximum
// levels in the given tree
static int maxLevel( Node root)
{
    if (root == null)
        return 0;
    return (1 + Math.max(maxLevel(root.left),
                     maxLevel(root.right)));
}

// Function to find the maximum sum of a
// level in the tree using recursion
static void maxLevelSum(Node root, int max_level,
                        int sum[], int current)
{
    // Base case
    if (root == null)
        return;

    // Add current node's data to
    // its level's sum
    sum[current] += root.data;

    // Recursive call for the left child
    maxLevelSum(root.left, max_level, sum,
                current + 1);

    // Recursive call for the right child
    maxLevelSum(root.right, max_level, sum,
                current + 1);
}

// Function to find the maximum sum of a
// level in the tree using recursion
static int maxLevelSum( Node root)
{

    // Maximum levels in the given tree
    int max_level = maxLevel(root);

    // To store the sum of every level
    int sum[] = new int[max_level + 1];

    // Recursive function call to
    // update the sum[] array
    maxLevelSum(root, max_level, sum, 1);

    // To store the maximum sum for a level
    int maxSum = 0;

    // For every level of the tree, update
    // the maximum sum of a level so far
    for (int i = 1; i <= max_level; i++)
        maxSum = Math.max(maxSum, sum[i]);

    // Return the maximum sum
    return maxSum;
}

// Driver code
public static void main(String args[])
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.right = newNode(8);
    root.right.right.left = newNode(6);
    root.right.right.right = newNode(7);

    /* Constructed Binary tree is:
                1
            / \
            2 3
            / \ \
            4 5 8
                / \
                6 7 */

    System.out.println(maxLevelSum(root));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of above algorithm

# Utility class to create a node
class Node:
    def __init__(self, key):
        self.val = key
        self.left = self.right = None

# Helper function that allocates a
# new node with the given data and
# None left and right pointers
def newNode(data):

    node = Node(0)
    node.data = data
    node.left = node.right = None
    return (node)

# Function to return the maximum
# levels in the given tree
def maxLevel( root):

    if (root == None):
        return 0
    return (1 + max(maxLevel(root.left),
                    maxLevel(root.right)))

sum = []

# Function to find the maximum sum of a
# level in the tree using recursion
def maxLevelSum_( root, max_level , current):

    global sum

    # Base case
    if (root == None):
        return

    # Add current node's data to
    # its level's sum
    sum[current] += root.data

    # Recursive call for the left child
    maxLevelSum_(root.left, max_level,
                current + 1)

    # Recursive call for the right child
    maxLevelSum_(root.right, max_level,
                current + 1)

# Function to find the maximum sum of a
# level in the tree using recursion
def maxLevelSum( root):

    global sum

    # Maximum levels in the given tree
    max_level = maxLevel(root)

    # To store the sum of every level
    i = 0
    sum = [None] * (max_level + 2)
    while(i <= max_level + 1):
        sum[i] = 0
        i = i + 1

    # Recursive function call to
    # update the sum[] array
    maxLevelSum_(root, max_level, 1)

    # To store the maximum sum for a level
    maxSum = 0

    # For every level of the tree, update
    # the maximum sum of a level so far
    i = 1
    while ( i <= max_level ):
        maxSum = max(maxSum, sum[i])
        i = i + 1

    # Return the maximum sum
    return maxSum

# Driver code
root = newNode(1)
root.left = newNode(2)
root.right = newNode(3)
root.left.left = newNode(4)
root.left.right = newNode(5)
root.right.right = newNode(8)
root.right.right.left = newNode(6)
root.right.right.right = newNode(7)

# Constructed Binary tree is:
#             1
#             / \
#             2 3
#         / \ \
#         4 5 8
#                 / \
#                 6 7

print( maxLevelSum(root))

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// A binary tree node has data,
// pointer to the left child
// and the right child
public class Node
{
    public int data;
    public Node left, right;
};

// Helper function that allocates a
// new node with the given data and
// null left and right pointers
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Function to return the maximum
// levels in the given tree
static int maxLevel( Node root)
{
    if (root == null)
        return 0;
    return (1 + Math.Max(maxLevel(root.left),
                         maxLevel(root.right)));
}

// Function to find the maximum sum of a
// level in the tree using recursion
static void maxLevelSum(Node root, int max_level,
                        int []sum, int current)
{
    // Base case
    if (root == null)
        return;

    // Add current node's data to
    // its level's sum
    sum[current] += root.data;

    // Recursive call for the left child
    maxLevelSum(root.left, max_level,
                sum, current + 1);

    // Recursive call for the right child
    maxLevelSum(root.right, max_level,
                sum, current + 1);
}

// Function to find the maximum sum of a
// level in the tree using recursion
static int maxLevelSum( Node root)
{

    // Maximum levels in the given tree
    int max_level = maxLevel(root);

    // To store the sum of every level
    int []sum = new int[max_level + 1];

    // Recursive function call to
    // update the sum[] array
    maxLevelSum(root, max_level, sum, 1);

    // To store the maximum sum for a level
    int maxSum = 0;

    // For every level of the tree, update
    // the maximum sum of a level so far
    for (int i = 1; i <= max_level; i++)
        maxSum = Math.Max(maxSum, sum[i]);

    // Return the maximum sum
    return maxSum;
}

// Driver code
public static void Main(String []args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.right = newNode(8);
    root.right.right.left = newNode(6);
    root.right.right.right = newNode(7);

    /* Constructed Binary tree is:
                1
            / \
            2 3
            / \ \
            4 5 8
                / \
                6 7 */

    Console.WriteLine(maxLevelSum(root));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// A binary tree node has data, pointer to
// the left child and the right child
class Node
{
    constructor()
    {
        this.data=0;
        this.left=this.right=null;
    }
}

// Helper function that allocates a
// new node with the given data and
// null left and right pointers
function newNode(data)
{
    let node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Function to return the maximum
// levels in the given tree
function maxLevel(root)
{
    if (root == null)
        return 0;
    return (1 + Math.max(maxLevel(root.left),maxLevel(root.right)));
}

// Function to find the maximum sum of a
// level in the tree using recursion
function maxLevelSum(root,max_level,sum,current)
{
    // Base case
    if (root == null)
        return;

    // Add current node's data to
    // its level's sum
    sum[current] += root.data;

    // Recursive call for the left child
    maxLevelSum(root.left, max_level, sum,
                current + 1);

    // Recursive call for the right child
    maxLevelSum(root.right, max_level, sum,
                current + 1);
}

// Function to find the maximum sum of a
// level in the tree using recursion
function _maxLevelSum(root)
{
    // Maximum levels in the given tree
    let max_level = maxLevel(root);

    // To store the sum of every level
    let sum = new Array(max_level + 1);
    for(let i=0;i<max_level+1;i++)
        sum[i]=0;

    // Recursive function call to
    // update the sum[] array
    maxLevelSum(root, max_level, sum, 1);

    // To store the maximum sum for a level
    let maxSum = 0;

    // For every level of the tree, update
    // the maximum sum of a level so far
    for (let i = 1; i <= max_level; i++)
        maxSum = Math.max(maxSum, sum[i]);

    // Return the maximum sum
    return maxSum;
}

// Driver code
let root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.left = newNode(4);
root.left.right = newNode(5);
root.right.right = newNode(8);
root.right.right.left = newNode(6);
root.right.right.right = newNode(7);

/* Constructed Binary tree is:
                1
            / \
            2 3
            / \ \
            4 5 8
                / \
                6 7 */

document.write(_maxLevelSum(root));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
17
```