# 不使用递归、堆栈或队列，在二叉树中寻找最大和最小元素

> 原文:[https://www . geesforgeks . org/find-不使用递归或堆栈或队列的二叉树中的最大和最小元素/](https://www.geeksforgeeks.org/find-maximum-and-minimum-element-in-binary-tree-without-using-recursion-or-stack-or-queue/)

给定一棵二叉树。任务是在不使用递归或堆栈或队列的情况下找出二叉树中的最大和最小元素，即空间复杂度应为 0(1)。

**示例:**

```
Input : 
                       12
                     /     \
                   13       10
                          /     \
                       14       15
                      /   \     /  \
                     21   24   22   23

Output : Max element : 24
         Min element : 10

Input : 
                       12
                     /     \
                  19        82
                 /        /     \
               41       15       95
                 \     /         /  \
                  2   21        7   16

Output : Max element : 95
         Min element : 2
```

**先决条件:** [无递归无堆栈有序树遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion-and-without-stack/)

**进场:**
1。将当前初始化为根
2。取最大和最小变量
3。当电流不为空时

*   如果当前没有左子
    *   如果需要，用当前数据更新变量最大值和最小值
    *   向右，即当前=当前->向右
*   其他
    *   使当前成为当前左子树中最右边
        节点的右子节点
    *   转到这个左边的子对象，即当前=当前->左边

下面是上述方法的实现:

## C++

```
// C++ program find maximum and minimum element
#include <bits/stdc++.h>
using namespace std;

// A Tree node
struct Node {
    int key;
    struct Node *left, *right;
};

// Utility function to create a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// Function to print a maximum and minimum element
// in a tree without recursion without stack
void printMinMax(Node* root)
{

    if (root == NULL)
    {
        cout << "Tree is empty";
        return;
    }

    Node* current = root;

    Node* pre;

    // Max variable for storing maximum value   
    int max_value = INT_MIN;

    // Min variable for storing minimum value   
    int min_value = INT_MAX;

    while (current != NULL)
    {
        // If left child does nor exists
        if (current->left == NULL)
        {
            max_value = max(max_value, current->key);
            min_value = min(min_value, current->key);

            current = current->right;
        }
        else
        {

            // Find the inorder predecessor of current
            pre = current->left;
            while (pre->right != NULL && pre->right !=
                                                 current)
                pre = pre->right;

            // Make current as the right child
            // of its inorder predecessor
            if (pre->right == NULL)
            {
                pre->right = current;
                current = current->left;
            }

            // Revert the changes made in the 'if' part to
            // restore the original tree i.e., fix the
            // right child of predecessor
            else
            {
                pre->right = NULL;

                max_value = max(max_value, current->key);
                min_value = min(min_value, current->key);

                current = current->right;
            } // End of if condition pre->right == NULL

        } // End of if condition current->left == NULL

    } // End of while

    // Finally print max and min value
    cout << "Max Value is : " << max_value << endl;
    cout << "Min Value is : " << min_value << endl;
}

// Driver Code
int main()
{
    /* 15
      /  \
    19   11
        /  \
       25   5
      / \   / \
    17  3  23  24

    Let us create Binary Tree as shown
    above */

    Node* root = newNode(15);
    root->left = newNode(19);
    root->right = newNode(11);

    root->right->left = newNode(25);
    root->right->right = newNode(5);

    root->right->left->left = newNode(17);
    root->right->left->right = newNode(3);
    root->right->right->left = newNode(23);
    root->right->right->right = newNode(24);

    // Function call for printing a max
    // and min element in a tree
    printMinMax(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program find maximum and minimum element
class GFG
{

// A Tree node
static class Node
{
    int key;
    Node left, right;
};

// Utility function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to print a maximum and minimum element
// in a tree without recursion without stack
static void printMinMax(Node root)
{

    if (root == null)
    {
        System.out.print("Tree is empty");
        return;
    }

    Node current = root;

    Node pre;

    // Max variable for storing maximum value
    int max_value = Integer.MIN_VALUE;

    // Min variable for storing minimum value
    int min_value = Integer.MAX_VALUE;

    while (current != null)
    {
        // If left child does nor exists
        if (current.left == null)
        {
            max_value = Math.max(max_value, current.key);
            min_value = Math.min(min_value, current.key);

            current = current.right;
        }
        else
        {

            // Find the inorder predecessor of current
            pre = current.left;
            while (pre.right != null && pre.right !=
                                                current)
                pre = pre.right;

            // Make current as the right child
            // of its inorder predecessor
            if (pre.right == null)
            {
                pre.right = current;
                current = current.left;
            }

            // Revert the changes made in the 'if' part to
            // restore the original tree i.e., fix the
            // right child of predecessor
            else
            {
                pre.right = null;

                max_value = Math.max(max_value, current.key);
                min_value = Math.min(min_value, current.key);

                current = current.right;
            } // End of if condition pre.right == null

        } // End of if condition current.left == null

    } // End of while

    // Finally print max and min value
    System.out.print("Max Value is : " + max_value + "\n");
    System.out.print("Min Value is : " + min_value + "\n");
}

// Driver Code
public static void main(String[] args)
{
    /* 15
    / \
    19 11
        / \
    25 5
    / \ / \
    17 3 23 24

    Let us create Binary Tree as shown
    above */

    Node root = newNode(15);
    root.left = newNode(19);
    root.right = newNode(11);

    root.right.left = newNode(25);
    root.right.right = newNode(5);

    root.right.left.left = newNode(17);
    root.right.left.right = newNode(3);
    root.right.right.left = newNode(23);
    root.right.right.right = newNode(24);

    // Function call for printing a max
    // and min element in a tree
    printMinMax(root);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python program find maximum and minimum element
from sys import maxsize

INT_MAX = maxsize
INT_MIN = -maxsize

# A Tree node
class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

# Function to print a maximum and minimum element
# in a tree without recursion without stack
def printMinMax(root: Node):
    if root is None:
        print("Tree is empty")
        return

    current = root
    pre = Node(0)

    # Max variable for storing maximum value
    max_value = INT_MIN

    # Min variable for storing minimum value
    min_value = INT_MAX

    while current is not None:

        # If left child does nor exists
        if current.left is None:
            max_value = max(max_value, current.key)
            min_value = min(min_value, current.key)

            current = current.right
        else:

            # Find the inorder predecessor of current
            pre = current.left
            while pre.right is not None and pre.right != current:
                pre = pre.right

            # Make current as the right child
            # of its inorder predecessor
            if pre.right is None:
                pre.right = current
                current = current.left

            # Revert the changes made in the 'if' part to
            # restore the original tree i.e., fix the
            # right child of predecessor
            else:
                pre.right = None
                max_value = max(max_value, current.key)
                min_value = min(min_value, current.key)

                current = current.right

            # End of if condition pre->right == NULL

        # End of if condition current->left == NULL

    # End of while

    # Finally print max and min value
    print("Max value is :", max_value)
    print("Min value is :", min_value)

# Driver Code
if __name__ == "__main__":

    # /* 15
    # / \
    # 19 11
    #     / \
    # 25 5
    # / \ / \
    # 17 3 23 24

    # Let us create Binary Tree as shown
    # above */

    root = Node(15)
    root.left = Node(19)
    root.right = Node(11)

    root.right.left = Node(25)
    root.right.right = Node(5)

    root.right.left.left = Node(17)
    root.right.left.right = Node(3)
    root.right.right.left = Node(23)
    root.right.right.right = Node(24)

    # Function call for printing a max
    # and min element in a tree
    printMinMax(root)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program find maximum and minimum element
using System;
class GFG
{

// A Tree node
class Node
{
    public int key;
    public Node left, right;
};

// Utility function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to print a maximum and minimum element
// in a tree without recursion without stack
static void printMinMax(Node root)
{
    if (root == null)
    {
        Console.Write("Tree is empty");
        return;
    }

    Node current = root;

    Node pre;

    // Max variable for storing maximum value
    int max_value = int.MinValue;

    // Min variable for storing minimum value
    int min_value = int.MaxValue;

    while (current != null)
    {
        // If left child does nor exists
        if (current.left == null)
        {
            max_value = Math.Max(max_value,
                                 current.key);
            min_value = Math.Min(min_value,
                                 current.key);

            current = current.right;
        }
        else
        {

            // Find the inorder predecessor of current
            pre = current.left;
            while (pre.right != null &&
                   pre.right != current)
                pre = pre.right;

            // Make current as the right child
            // of its inorder predecessor
            if (pre.right == null)
            {
                pre.right = current;
                current = current.left;
            }

            // Revert the changes made in the 'if' part to
            // restore the original tree i.e., fix the
            // right child of predecessor
            else
            {
                pre.right = null;

                max_value = Math.Max(max_value,
                                     current.key);
                min_value = Math.Min(min_value,    
                                     current.key);

                current = current.right;
            } // End of if condition pre.right == null

        } // End of if condition current.left == null

    } // End of while

    // Finally print max and min value
    Console.Write("Max Value is : " +
                   max_value + "\n");
    Console.Write("Min Value is : " +
                   min_value + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    /* 15
    / \
    19 11
        / \
    25 5
    / \ / \
    17 3 23 24

    Let us create Binary Tree as shown
    above */

    Node root = newNode(15);
    root.left = newNode(19);
    root.right = newNode(11);

    root.right.left = newNode(25);
    root.right.right = newNode(5);

    root.right.left.left = newNode(17);
    root.right.left.right = newNode(3);
    root.right.right.left = newNode(23);
    root.right.right.right = newNode(24);

    // Function call for printing a max
    // and min element in a tree
    printMinMax(root);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program find maximum
// and minimum element

// A Tree node
class Node
{
    constructor()
    {
        this.key = 0;
        this.left = null;
        this.right = null;
    }
};

// Utility function to create a new node
function newNode(key)
{
    var temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to print a maximum and minimum
// element in a tree without recursion
// without stack
function printMinMax(root)
{
    if (root == null)
    {
        document.write("Tree is empty");
        return;
    }

    var current = root;
    var pre;

    // Max variable for storing maximum value
    var max_value = -1000000000;

    // Min variable for storing minimum value
    var min_value = 1000000000;

    while (current != null)
    {

        // If left child does nor exists
        if (current.left == null)
        {
            max_value = Math.max(max_value,
                                 current.key);
            min_value = Math.min(min_value,
                                 current.key);

            current = current.right;
        }
        else
        {

            // Find the inorder predecessor of current
            pre = current.left;
            while (pre.right != null &&
                   pre.right != current)
                pre = pre.right;

            // Make current as the right child
            // of its inorder predecessor
            if (pre.right == null)
            {
                pre.right = current;
                current = current.left;
            }

            // Revert the changes made in the 'if'
            // part to restore the original tree
            // i.e., fix the right child of predecessor
            else
            {
                pre.right = null;

                max_value = Math.max(max_value,
                                     current.key);
                min_value = Math.min(min_value,    
                                     current.key);

                current = current.right;
            } // End of if condition pre.right == null

        } // End of if condition current.left == null

    } // End of while

    // Finally print max and min value
    document.write("Max Value is : " +
                   max_value + "<br>");
    document.write("Min Value is : " +
                   min_value + "<br>");
}

// Driver Code
/* 15
/ \
19 11
    / \
25 5
/ \ / \
17 3 23 24
Let us create Binary Tree as shown
above */
var root = newNode(15);
root.left = newNode(19);
root.right = newNode(11);
root.right.left = newNode(25);
root.right.right = newNode(5);
root.right.left.left = newNode(17);
root.right.left.right = newNode(3);
root.right.right.left = newNode(23);
root.right.right.right = newNode(24);

// Function call for printing a max
// and min element in a tree
printMinMax(root);

// This code is contributed by noob2000

</script>
```

**输出:**

```
Max Value is : 25
Min Value is : 3
```

**时间复杂度:**O(N)
T3】空间复杂度: O(1)