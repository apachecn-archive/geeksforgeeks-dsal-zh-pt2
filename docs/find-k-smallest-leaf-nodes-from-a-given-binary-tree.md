# 从给定的二叉树中找到 K 个最小的叶节点

> 原文:[https://www . geeksforgeeks . org/find-k-最小叶节点-来自给定二叉树/](https://www.geeksforgeeks.org/find-k-smallest-leaf-nodes-from-a-given-binary-tree/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)和一个整数 **K** ，任务是从给定的二叉树中找到 **K** 最小的[叶节点。叶节点的数量将始终至少为 **K** 。](https://www.geeksforgeeks.org/print-leaf-nodes-left-right-binary-tree/)

**示例:**

> **输入:**
> **1
> /\
> 2 3
> /\/\
> 4 5 6 7
> /\ \
> 21 8 19
> **输出:** 6 8 19
> **说明:**
> 上述二叉树
> 共有 4 个叶节点，其中 6、8、19 是最小的三个叶节点。**
> 
> ****输入:**
> 11
> /\
> 12 3
> /\/\
> 41 15 61 1
> \
> 8
> **输出:** 1 8 15
> **说明:**
> 上述二叉树
> 共有 4 个叶节点，其中 1、8、15 是最小的三个叶节点。**

****方法:**按照以下步骤解决问题:**

*   **[遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)二叉树。**
*   **检查每个节点是否既不包含左子节点也不包含右子节点。如果发现为真，则该节点是叶节点。将所有这样的节点存储在一个数组中。**
*   **[对叶节点数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序，打印数组中的 **K** 最小叶值。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program of the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Structure of
// binary tree node
struct Node {
    int data;
    Node *left, *right;
};

// Function to create new node
Node* newNode(int data)
{
    Node* temp = new Node();
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Utility function which calculates
// smallest three nodes of all leaf nodes
void storeLeaf(Node* root, vector<int>& arr)
{
    if (!root)
        return;

    // Check if current root is a leaf node
    if (!root->left and !root->right) {
        arr.push_back(root->data);
        return;
    }

    // Traverse the left
    // and right subtree
    storeLeaf(root->left, arr);
    storeLeaf(root->right, arr);
}

// Function to find the K smallest
// nodes of the Binary Tree
void KSmallest(Node* root, int k)
{
    vector<int> arr;
    storeLeaf(root, arr);

    // Sorting the Leaf nodes array
    sort(arr.begin(), arr.end());

    // Loop to print the K smallest
    // Leaf nodes of the array
    for (int i = 0; i < k; i++) {
        if (i < arr.size()) {
            cout << arr[i] << " ";
        }
        else {
            break;
        }
    }
}

// Driver Code
int main()
{
    // Construct binary tree
    Node* root = newNode(1);
    root->left = newNode(2);
    root->left->left = newNode(4);
    root->left->left->left = newNode(21);
    root->left->right = newNode(5);
    root->left->right->right = newNode(8);
    root->right = newNode(3);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->right->right->right = newNode(19);

    // Function Call
    KSmallest(root, 3);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program of the
// above approach
import java.util.*;

class GFG{

// Structure of
// binary tree node
static class Node
{
    int data;
    Node left, right;
};

// Function to create new node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// Utility function which calculates
// smallest three nodes of all leaf nodes
static Vector<Integer> storeLeaf(Node root,
                       Vector<Integer> arr)
{
    if (root == null)
        return arr;

    // Check if current root is a leaf node
    if (root.left == null &&
       root.right == null)
    {
        arr.add(root.data);
        return arr;
    }

    // Traverse the left
    // and right subtree
    arr = storeLeaf(root.left, arr);
    arr = storeLeaf(root.right, arr);
    return arr;
}

// Function to find the K smallest
// nodes of the Binary Tree
static void KSmallest(Node root, int k)
{
    Vector<Integer> arr = new Vector<Integer>();
    arr = storeLeaf(root, arr);

    // Sorting the Leaf nodes array
    Collections.sort(arr);

    // Loop to print the K smallest
    // Leaf nodes of the array
    for(int i = 0; i < k; i++)
    {
        if (i < arr.size())
        {
            System.out.print(arr.get(i) + " ");
        }
        else
        {
            break;
        }
    }
}

// Driver Code
public static void main(String[] args)
{

    // Construct binary tree
    Node root = newNode(1);
    root.left = newNode(2);
    root.left.left = newNode(4);
    root.left.left.left = newNode(21);
    root.left.right = newNode(5);
    root.left.right.right = newNode(8);
    root.right = newNode(3);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.right.right.right = newNode(19);

    // Function call
    KSmallest(root, 3);
}
}

// This code is contributed by Amit Katiyar
```

## **蟒蛇 3**

```
# Python3 program for the
# above approach

# Binary tree node
class Node:
    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# Utility function which calculates
# smallest three nodes of all leaf nodes
def storeLeaf(root: Node,
              arr : list) -> None:

    if (not root):
        return

    # Check if current root
    # is a leaf node
    if (not root.left and
        not root.right):
        arr.append(root.data)
        return

    # Traverse the left
    # and right subtree
    storeLeaf(root.left, arr)
    storeLeaf(root.right, arr)

# Function to find the K smallest
# nodes of the Binary Tree
def KSmallest(root: Node,
              k: int) -> None:

    arr = []
    storeLeaf(root, arr)

    # Sorting the Leaf
    # nodes array
    arr.sort()

    # Loop to print the K smallest
    # Leaf nodes of the array
    for i in range(k):
        if (i < len(arr)):
            print(arr[i], end = " ")
        else:
            break

# Driver Code
if __name__ == "__main__":

    # Construct binary tree
    root = Node(1)
    root.left = Node(2)
    root.left.left = Node(4)
    root.left.left.left = Node(21)
    root.left.right = Node(5)
    root.left.right.right = Node(8)
    root.right = Node(3)
    root.right.left = Node(6)
    root.right.right = Node(7)
    root.right.right.right = Node(19)

    # Function Call
    KSmallest(root, 3)

# This code is contributed by sanjeev2552
```

## **C#**

```
// C# program of the
// above approach
using System;
using System.Collections.Generic;

class GFG{

// Structure of
// binary tree node
class Node
{
    public int data;
    public Node left, right;
};

// Function to create new node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// Utility function which calculates
// smallest three nodes of all leaf nodes
static List<int> storeLeaf(Node root,
                           List<int> arr)
{
    if (root == null)
        return arr;

    // Check if current root is a leaf node
    if (root.left == null &&
       root.right == null)
    {
        arr.Add(root.data);
        return arr;
    }

    // Traverse the left
    // and right subtree
    arr = storeLeaf(root.left, arr);
    arr = storeLeaf(root.right, arr);
    return arr;
}

// Function to find the K smallest
// nodes of the Binary Tree
static void KSmallest(Node root, int k)
{
    List<int> arr = new List<int>();
    arr = storeLeaf(root, arr);

    // Sorting the Leaf nodes array
    arr.Sort();

    // Loop to print the K smallest
    // Leaf nodes of the array
    for(int i = 0; i < k; i++)
    {
        if (i < arr.Count)
        {
            Console.Write(arr[i] + " ");
        }
        else
        {
            break;
        }
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Construct binary tree
    Node root = newNode(1);
    root.left = newNode(2);
    root.left.left = newNode(4);
    root.left.left.left = newNode(21);
    root.left.right = newNode(5);
    root.left.right.right = newNode(8);
    root.right = newNode(3);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.right.right.right = newNode(19);

    // Function call
    KSmallest(root, 3);
}
}

// This code is contributed by Amit Katiyar
```

## **java 描述语言**

```
<script>

    // JavaScript program for the above approach

    // Structure of binary tree node
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Function to create new node
    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

    // Utility function which calculates
    // smallest three nodes of all leaf nodes
    function storeLeaf(root, arr)
    {
        if (root == null)
            return arr;

        // Check if current root is a leaf node
        if (root.left == null &&
           root.right == null)
        {
            arr.push(root.data);
            return arr;
        }

        // Traverse the left
        // and right subtree
        arr = storeLeaf(root.left, arr);
        arr = storeLeaf(root.right, arr);
        return arr;
    }

    // Function to find the K smallest
    // nodes of the Binary Tree
    function KSmallest(root, k)
    {
        let arr = [];
        arr = storeLeaf(root, arr);

        // Sorting the Leaf nodes array
        arr.sort(function(a, b){return a - b});

        // Loop to print the K smallest
        // Leaf nodes of the array
        for(let i = 0; i < k; i++)
        {
            if (i < arr.length)
            {
                document.write(arr[i] + " ");
            }
            else
            {
                break;
            }
        }
    }

    // Construct binary tree
    let root = newNode(1);
    root.left = newNode(2);
    root.left.left = newNode(4);
    root.left.left.left = newNode(21);
    root.left.right = newNode(5);
    root.left.right.right = newNode(8);
    root.right = newNode(3);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.right.right.right = newNode(19);

    // Function call
    KSmallest(root, 3);

</script>
```

****Output:** 

```
6 8 19
```** 

*****时间复杂度:** O(N + L*logL)，这里 L 是叶节点数，N 是节点数。*
***辅助空间:** O(L + logN)***