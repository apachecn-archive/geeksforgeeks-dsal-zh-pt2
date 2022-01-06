# 二叉树的两个节点连接起来可以形成的最大长度循环

> 原文:[https://www . geesforgeks . org/通过连接二叉树的两个节点可以形成的最大长度循环/](https://www.geeksforgeeks.org/maximum-length-cycle-that-can-be-formed-by-joining-two-nodes-of-a-binary-tree/)

给定一棵二叉树，任务是找到通过连接树的任意两个节点可以形成的循环的最大长度。
**例:**

```
Input: 
            1
           /  \
          2    3
           \     \
            5     6

Output: 5
Cycle can be formed by joining node with value 5 and 6.

Input:
         1
        /  \
       3    4
      / \    
     5   6    
    /     \
   7       8
    \     /
    11   9 

Output: 7
```

**方法:**思路是求给定二叉树的[直径](https://www.geeksforgeeks.org/diameter-of-a-binary-tree-in-on-a-new-method/)，因为最大长度的循环将等于二叉树的直径。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Tree node structure
struct Node {
    int data;
    Node *left, *right;
};

struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;

    return (node);
}

// Function to find height of a tree
int height(Node* root, int& ans)
{
    if (root == NULL)
        return 0;

    int left_height = height(root->left, ans);

    int right_height = height(root->right, ans);

    // Update the answer, because diameter of a
    // tree is nothing but maximum value of
    // (left_height + right_height + 1) for each node
    ans = max(ans, 1 + left_height + right_height);

    return 1 + max(left_height, right_height);
}

// Computes the diameter of binary tree
// with given root
int diameter(Node* root)
{
    if (root == NULL)
        return 0;

    // Variable to store the final answer
    int ans = INT_MIN;

    int height_of_tree = height(root, ans);
    return ans;
}

// Driver code
int main()
{
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);

    printf("%d", diameter(root));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Tree node structure
static class Node
{
    int data;
    Node left, right;
};

static int ans;
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;

    return (node);
}

// Function to find height of a tree
static int height(Node root)
{
    if (root == null)
        return 0;

    int left_height = height(root.left);

    int right_height = height(root.right);

    // Update the answer, because diameter of a
    // tree is nothing but maximum value of
    // (left_height + right_height + 1) for each node
    ans = Math.max(ans, 1 + left_height + right_height);

    return 1 + Math.max(left_height, right_height);
}

// Computes the diameter of binary tree
// with given root
static int diameter(Node root)
{
    if (root == null)
        return 0;

    // Variable to store the final answer
    ans = Integer.MIN_VALUE;

    int height_of_tree = height(root);
    return ans;
}

// Driver code
public static void main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);

    System.out.printf("%d", diameter(root));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Tree node structure
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to find height of a tree
def height(root):

    if root == None:
        return 0

    global ans
    left_height = height(root.left)
    right_height = height(root.right)

    # Update the answer, because diameter of a
    # tree is nothing but maximum value of
    # (left_height + right_height + 1) for each node
    ans = max(ans, 1 + left_height + right_height)

    return 1 + max(left_height, right_height)

# Computes the diameter of
# binary tree with given root
def diameter(root):

    if root == None:
        return 0

    height_of_tree = height(root)
    return ans

# Driver code
if __name__ == "__main__":

    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)

    ans = 0
    print(diameter(root))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Tree node structure
public class Node
{
    public int data;
    public Node left, right;
};

static int ans;
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;

    return (node);
}

// Function to find height of a tree
static int height(Node root)
{
    if (root == null)
        return 0;

    int left_height = height(root.left);

    int right_height = height(root.right);

    // Update the answer, because diameter of a
    // tree is nothing but maximum value of
    // (left_height + right_height + 1) for each node
    ans = Math.Max(ans, 1 + left_height +
                            right_height);

    return 1 + Math.Max(left_height,
                        right_height);
}

// Computes the diameter of binary tree
// with given root
static int diameter(Node root)
{
    if (root == null)
        return 0;

    // Variable to store the final answer
    ans = int.MinValue;

    int height_of_tree = height(root);
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);

    Console.WriteLine("{0}", diameter(root));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    let ans;
    function newNode(data)
    {
        let node = new Node(data);
        return (node);
    }

    // Function to find height of a tree
    function height(root)
    {
        if (root == null)
            return 0;

        let left_height = height(root.left);

        let right_height = height(root.right);

        // Update the answer, because diameter of a
        // tree is nothing but maximum value of
        // (left_height + right_height + 1) for each node
        ans = Math.max(ans, 1 + left_height + right_height);

        return 1 + Math.max(left_height, right_height);
    }

    // Computes the diameter of binary tree
    // with given root
    function diameter(root)
    {
        if (root == null)
            return 0;

        // Variable to store the final answer
        ans = Number.MIN_VALUE;

        let height_of_tree = height(root);
        return ans;
    }

    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);

    document.write(diameter(root));

</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)