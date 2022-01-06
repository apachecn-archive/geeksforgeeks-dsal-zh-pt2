# 求二叉树中所有右节点的最大值

> 原文:[https://www . geeksforgeeks . org/find-二叉树中所有正确节点中的最大值/](https://www.geeksforgeeks.org/find-maximum-among-all-right-nodes-in-binary-tree/)

给定一棵二叉树。任务是在二叉树的所有右子节点中找到最大值。
**注意**:如果树不包含任何右子节点或者是空的，打印-1。
T4【示例】T5:

```
Input : 
           7
         /    \
        6       5
       / \     / \
      4  3     2  1 
Output : 5
All possible right child nodes are: {3, 5, 1}
out of which 5 is of the maximum value.

Input :
            1
         /    \
        2       3
       /       / \
      4       5   6
        \    /  \ 
         7  8    9 
Output : 9
```

其思想是递归遍历树，以便遍历每个节点:

*   检查是否存在正确的子节点。
*   如果是，将其值存储在临时变量中。
*   返回最大值(当前节点的右子节点的值，递归调用左子树，递归调用右子树)。

以下是上述方法的实现:

## C++

```
// CPP program to print maximum element
// among all right child nodes
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node {
    int data;
    struct Node *left, *right;
};

// Utility function to create a new tree node
Node* newNode(int data)
{
    Node* temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Function to find maximum element
// among all right child nodes using
// Inorder Traversal
int maxOfRightElement(Node* root)
{
    // Temp variable
    int res = INT_MIN;

    // If tree is empty
    if (root == NULL)
        return -1;

    // If right child exists
    if (root->right != NULL)
        res = root->right->data;

    // Return maximum of three values
    // 1) Recursive max in right subtree
    // 2) Value in right child node
    // 3) Recursive max in left subtree
    return max({ maxOfRightElement(root->right),
                 res,
                 maxOfRightElement(root->left) });
}

// Driver Code
int main()
{
    // Create binary tree
    // as shown below

    /*   7
        / \
       6   5
      / \ / \
      4 3 2 1  */
    Node* root = newNode(7);
    root->left = newNode(6);
    root->right = newNode(5);
    root->left->left = newNode(4);
    root->left->right = newNode(3);
    root->right->left = newNode(2);
    root->right->right = newNode(1);

    cout << maxOfRightElement(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print maximum element
// among all right child nodes
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
      static int maxOfRightElement(Node root)
      {
             // Temp variable
             int res = Integer.MIN_VALUE;

             // If tree is empty
             if (root == null)
                 return -1;

              // If right child exists
              if (root.right != null)
                  res = root.right.data;

              // Return maximum of three values
              // 1) Recursive max in right subtree
              // 2) Value in right child node
              // 3) Recursive max in left subtree
              return Math.max(maxOfRightElement(root.right),
                     Math.max(res,maxOfRightElement(root.left)));
      }
      // Driver code
      public static void main(String args[])
      {
           // Create binary tree
          // as shown below

          /*   7
              / \
             6   5
            / \ / \
            4 3 2  1  */

          Node root = new Node(7);
          root.left = new Node(6);
          root.right = new Node(5);
          root.left.left = new Node(4);
          root.left.right = new Node(3);
          root.right.left = new Node(2);
          root.right.right = new Node(1);

          System.out.println(maxOfRightElement(root));
       }
}
// This code is contributed by rachana soma
```

## 蟒蛇 3

```
# Python3 program to print maximum element
# among all right child nodes

# Tree node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Utility function to create a new tree node
def newNode(data):

    temp = Node(0)
    temp.data = data
    temp.left = temp.right = None
    return temp

# Function to find maximum element
# among all right child nodes using
# Inorder Traversal
def maxOfRightElement(root):

    # Temp variable
    res = -999999

    # If tree is empty
    if (root == None):
        return -1

    # If right child exists
    if (root.right != None):
        res = root.right.data

    # Return maximum of three values
    # 1) Recursive max in right subtree
    # 2) Value in right child node
    # 3) Recursive max in left subtree
    return max( maxOfRightElement(root.right),
                res,
                maxOfRightElement(root.left) )

# Driver Code

# Create binary tree
# as shown below
#     7
# / \
# 6 5
# / \ / \
# 4 3 2 1
root = newNode(7)
root.left = newNode(6)
root.right = newNode(5)
root.left.left = newNode(4)
root.left.right = newNode(3)
root.right.left = newNode(2)
root.right.right = newNode(1)

print (maxOfRightElement(root))

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation to print maximum element
// among all right child nodes
using System;

// User defined node class
public class Node
{
    public int data;
    public Node left, right;

    // Constructor to create a new tree node
    public Node(int key)
    {
        data = key;
        left = right = null;
    }
}

public class GFG
{
    static int maxOfRightElement(Node root)
    {
            // Temp variable
            int res = int.MinValue;

            // If tree is empty
            if (root == null)
                return -1;

            // If right child exists
            if (root.right != null)
                res = root.right.data;

            // Return maximum of three values
            // 1) Recursive max in right subtree
            // 2) Value in right child node
            // 3) Recursive max in left subtree
            return Math.Max(maxOfRightElement(root.right),
                    Math.Max(res,maxOfRightElement(root.left)));
    }

    // Driver code
    public static void Main(String []args)
    {
        // Create binary tree
        // as shown below

        /* 7
            / \
            6 5
            / \ / \
            4 3 2 1 */

        Node root = new Node(7);
        root.left = new Node(6);
        root.right = new Node(5);
        root.left.left = new Node(4);
        root.left.right = new Node(3);
        root.right.left = new Node(2);
        root.right.right = new Node(1);

        Console.WriteLine(maxOfRightElement(root));
    }
}

// This code is contributed 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript implementation to print maximum element
    // among all right child nodes

    // User defined node class
    class Node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.data = key;
        }
    }

    function maxOfRightElement(root)
    {
      // Temp variable
      let res = Number.MIN_VALUE;

      // If tree is empty
      if (root == null)
        return -1;

      // If right child exists
      if (root.right != null)
        res = root.right.data;

      // Return maximum of three values
      // 1) Recursive max in right subtree
      // 2) Value in right child node
      // 3) Recursive max in left subtree
      return Math.max(maxOfRightElement(root.right),
                      Math.max(res,maxOfRightElement(root.left)));
    }

    // Create binary tree
    // as shown below

    /*   7
                / \
               6   5
              / \ / \
              4 3 2  1  */

    let root = new Node(7);
    root.left = new Node(6);
    root.right = new Node(5);
    root.left.left = new Node(4);
    root.left.right = new Node(3);
    root.right.left = new Node(2);
    root.right.right = new Node(1);

    document.write(maxOfRightElement(root));

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(n)
***辅助空间** : O(n)*