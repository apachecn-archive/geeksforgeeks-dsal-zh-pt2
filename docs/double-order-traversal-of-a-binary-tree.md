# 二叉树的双顺序遍历

> 原文:[https://www . geesforgeks . org/二叉树的双顺序遍历/](https://www.geeksforgeeks.org/double-order-traversal-of-a-binary-tree/)

给定一个由 **N** 节点组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是打印它的**双顺序遍历。**

> **双顺序遍历**是一种[树遍历技术](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)，其中每个节点按照以下顺序遍历两次:
> 
> *   访问节点。
> *   遍历左子树。
> *   访问节点。
> *   遍历右子树。

**示例:**

```
Input:
        1
      /   \
     7     3
    / \   /
   4   5 6
Output: 1 7 4 4 7 5 5 1 3 6 6 3 

Input:
        1
      /   \
     7     3
    / \     \
   4   5     6
Output: 1 7 4 4 7 5 5 1 3 3 6 6
```

**方法:**
想法是在给定的二叉树上递归执行[有序遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/)，并在遍历过程中递归调用左子树后访问顶点和**时打印节点值。**

按照以下步骤解决问题:

*   从**根开始[以便遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。**
*   如果**当前节点**不存在，只需从中返回即可。
*   否则:
    *   打印**当前节点**的值。
    *   递归遍历**左子树。**
    *   再次打印**当前节点**。
    *   递归遍历**右子树。**
*   重复以上步骤，直到访问了树中的所有节点。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <iostream>
using namespace std;

// Node Structure
struct node {
    char data;
    struct node *left, *right;
};

// Function to create new node
struct node* newNode(char ch)
{
    // Allocate a new node in memory
    struct node* Node = new node();
    Node->data = ch;
    Node->left = NULL;
    Node->right = NULL;
    return Node;
}

// Function to print Double Order traversal
void doubleOrderTraversal(struct node* root)
{
    if (!root)
        return;

    // Print Node Value
    cout << root->data << " ";

    // Traverse Left Subtree
    doubleOrderTraversal(root->left);

    // Print Node Value
    cout << root->data << " ";

    // Traverse Right SubTree
    doubleOrderTraversal(root->right);
}

// Driver Code
int main()
{
    struct node* root = newNode('1');
    root->left = newNode('7');
    root->right = newNode('3');
    root->left->left = newNode('4');
    root->left->right = newNode('5');
    root->right->right = newNode('6');

    doubleOrderTraversal(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Node Structure
static class node
{
    char data;
    node left, right;
};

// Function to create new node
static node newNode(char ch)
{

    // Allocate a new node in memory
    node n = new node();
    n.data = ch;
    n.left = null;
    n.right = null;
    return n;
}

// Function to print Double Order traversal
static void doubleOrderTraversal(node root)
{
    if (root == null)
        return;

    // Print Node Value
    System.out.print(root.data + " ");

    // Traverse Left Subtree
    doubleOrderTraversal(root.left);

    // Print Node Value
    System.out.print(root.data + " ");

    // Traverse Right SubTree
    doubleOrderTraversal(root.right);
}

// Driver Code
public static void main(String[] args)
{
    node root = newNode('1');
    root.left = newNode('7');
    root.right = newNode('3');
    root.left.left = newNode('4');
    root.left.right = newNode('5');
    root.right.right = newNode('6');

    doubleOrderTraversal(root);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Node Structure
class Node:

    # Initialise new node
    def __init__(self, ch):

        self.data = ch
        self.left = None
        self.right = None

# Function to print Double Order traversal
def doubleOrderTraveersal(root):

    if not root:
        return

    # Print node value
    print(root.data, end = " ")

    # Traverse left subtree
    doubleOrderTraveersal(root.left)

    # Print node value
    print(root.data, end = " ")

    # Traverse right subtree
    doubleOrderTraveersal(root.right)

# Driver code
if __name__ == '__main__':

    root = Node(1)
    root.left = Node(7)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right.right = Node(6)

    doubleOrderTraveersal(root)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Node Structure
class node
{
    public char data;
    public node left, right;
};

// Function to create new node
static node newNode(char ch)
{

    // Allocate a new node in memory
    node n = new node();
    n.data = ch;
    n.left = null;
    n.right = null;
    return n;
}

// Function to print Double Order traversal
static void doubleOrderTraversal(node root)
{
    if (root == null)
        return;

    // Print Node Value
    Console.Write(root.data + " ");

    // Traverse Left Subtree
    doubleOrderTraversal(root.left);

    // Print Node Value
    Console.Write(root.data + " ");

    // Traverse Right SubTree
    doubleOrderTraversal(root.right);
}

// Driver Code
public static void Main(String[] args)
{
    node root = newNode('1');
    root.left = newNode('7');
    root.right = newNode('3');
    root.left.left = newNode('4');
    root.left.right = newNode('5');
    root.right.right = newNode('6');

    doubleOrderTraversal(root);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Node Structure
class node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// Function to create new node
function newNode(ch)
{

    // Allocate a new node in memory
    var n = new node();
    n.data = ch;
    n.left = null;
    n.right = null;
    return n;
}

// Function to print Double Order traversal
function doubleOrderTraversal(root)
{
    if (root == null)
        return;

    // Print Node Value
    document.write(root.data + " ");

    // Traverse Left Subtree
    doubleOrderTraversal(root.left);

    // Print Node Value
    document.write(root.data + " ");

    // Traverse Right SubTree
    doubleOrderTraversal(root.right);
}

// Driver Code
var root = newNode('1');
root.left = newNode('7');
root.right = newNode('3');
root.left.left = newNode('4');
root.left.right = newNode('5');
root.right.right = newNode('6');
doubleOrderTraversal(root);

</script>
```

**Output:** 

```
1 7 4 4 7 5 5 1 3 3 6 6
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*