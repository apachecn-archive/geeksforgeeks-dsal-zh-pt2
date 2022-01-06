# 所有节点的数字和等于 X 的子树计数

> 原文:[https://www . geeksforgeeks . org/所有节点的数字总和等于 x 的子树计数/](https://www.geeksforgeeks.org/count-of-subtrees-with-digit-sum-of-all-nodes-equals-to-x/)

给定由 **N** 节点和正整数 **X** 组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)。任务是统计节点位数和等于 **X** 的子树个数。

**示例:**

> **输入:** N = 7，X = 29
> 
> 10
> / \
> 2 3
> / \ / \
> 9 3 4 7
> 
> **输出:** 2
> **说明:**整个二叉树是一个数字和等于 29 的子树。
> 
> **输入:** N = 7，X = 14
> 
> 10
> / \
> 2 3
> / \ / \
> 9 3 4 7
> 
> **输出:** 2

**方法:**这个问题是[用给定的和](https://www.geeksforgeeks.org/count-subtress-sum-given-value-x/)计算二叉树中的子树的一个变种。为了解决这个问题，使用任何树遍历用它们的数字和替换所有节点，然后[用和 **X**](https://www.geeksforgeeks.org/count-subtress-sum-given-value-x/) 计数子树。

下面是上述方法的实现。

## C++

```
// C++ implementation for above approach
#include <bits/stdc++.h>

using namespace std;

// Structure of a node of binary tree
struct Node {
    int data;
    Node *left, *right;
};

// Function to get a new node
Node* getNode(int data)
{
    // Allocate space
    Node* newNode
        = (Node*)malloc(sizeof(Node));

    // Put in the data
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// Function to find digit sum of number
int digitSum(int N)
{
    int sum = 0;
    while (N) {
        sum += N % 10;
        N /= 10;
    }
    return sum;
}

// Function to replace all the nodes
// with their digit sums using pre-order
void replaceNodes(Node* root)
{
    if (!root)
        return;

    // Assigning digit sum value
    root->data = digitSum(root->data);

    // Calling left sub-tree
    replaceNodes(root->left);

    // Calling right sub-tree
    replaceNodes(root->right);
}

// Function to count subtrees that
// Sum up to a given value x
int countSubtreesWithSumX(Node* root,
                          int& count, int x)
{
    // If tree is empty
    if (!root)
        return 0;

    // Sum of nodes in the left subtree
    int ls = countSubtreesWithSumX(
        root->left, count, x);

    // Sum of nodes in the right subtree
    int rs = countSubtreesWithSumX(
        root->right, count, x);

    // Sum of nodes in the subtree rooted
    // with 'root->data'
    int sum = ls + rs + root->data;

    // If true
    if (sum == x)
        count++;

    // Return subtree's nodes sum
    return sum;
}

// Utility function to count subtrees that
// sum up to a given value x
int countSubtreesWithSumXUtil(Node* root, int x)
{
    // If tree is empty
    if (!root)
        return 0;

    int count = 0;

    // Sum of nodes in the left subtree
    int ls = countSubtreesWithSumX(
        root->left, count, x);

    // sum of nodes in the right subtree
    int rs = countSubtreesWithSumX(
        root->right, count, x);

    // If tree's nodes sum == x
    if ((ls + rs + root->data) == x)
        count++;

    // Required count of subtrees
    return count;
}

// Driver program to test above
int main()
{
    int N = 7;
    /* Binary tree creation
           10         
          /   \
        2       3
      /  \     /  \  
     9    3    4   7
    */
    Node* root = getNode(10);
    root->left = getNode(2);
    root->right = getNode(3);
    root->left->left = getNode(9);
    root->left->right = getNode(3);
    root->right->left = getNode(4);
    root->right->right = getNode(7);

    // Replacing nodes with their
    // digit sum value
    replaceNodes(root);

    int X = 29;

    cout << countSubtreesWithSumXUtil(root, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for above approach
class GFG{

static int count = 0;

// Structure of a node of binary tree
static class Node {
    int data;
    Node left, right;
};

// Function to get a new node
static Node getNode(int data)
{
    // Allocate space
    Node newNode
        = new Node();

    // Put in the data
    newNode.data = data;
    newNode.left = newNode.right = null;
    return newNode;
}

// Function to find digit sum of number
static int digitSum(int N)
{
    int sum = 0;
    while (N>0) {
        sum += N % 10;
        N /= 10;
    }
    return sum;
}

// Function to replace all the nodes
// with their digit sums using pre-order
static void replaceNodes(Node root)
{
    if (root==null)
        return;

    // Assigning digit sum value
    root.data = digitSum(root.data);

    // Calling left sub-tree
    replaceNodes(root.left);

    // Calling right sub-tree
    replaceNodes(root.right);
}

// Function to count subtrees that
// Sum up to a given value x
static int countSubtreesWithSumX(Node root, int x)
{
    // If tree is empty
    if (root==null)
        return 0;

    // Sum of nodes in the left subtree
    int ls = countSubtreesWithSumX(
        root.left,  x);

    // Sum of nodes in the right subtree
    int rs = countSubtreesWithSumX(
        root.right,  x);

    // Sum of nodes in the subtree rooted
    // with 'root.data'
    int sum = ls + rs + root.data;

    // If true
    if (sum == x)
        count++;

    // Return subtree's nodes sum
    return sum;
}

// Utility function to count subtrees that
// sum up to a given value x
static int countSubtreesWithSumXUtil(Node root, int x)
{
    // If tree is empty
    if (root==null)
        return 0;

    count = 0;

    // Sum of nodes in the left subtree
    int ls = countSubtreesWithSumX(
        root.left,  x);

    // sum of nodes in the right subtree
    int rs = countSubtreesWithSumX(
        root.right,  x);

    // If tree's nodes sum == x
    if ((ls + rs + root.data) == x)
        count++;

    // Required count of subtrees
    return count;
}

// Driver program to test above
public static void main(String[] args)
{
    int N = 7;
    /* Binary tree creation
           10         
          /   \
        2       3
      /  \     /  \  
     9    3    4   7
    */
    Node root = getNode(10);
    root.left = getNode(2);
    root.right = getNode(3);
    root.left.left = getNode(9);
    root.left.right = getNode(3);
    root.right.left = getNode(4);
    root.right.right = getNode(7);

    // Replacing nodes with their
    // digit sum value
    replaceNodes(root);

    int X = 29;

    System.out.print(countSubtreesWithSumXUtil(root, X));

}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation for above approach
using System;
public class GFG{

static int count = 0;

// Structure of a node of binary tree
class Node {
    public int data;
    public Node left, right;
};

// Function to get a new node
static Node getNode(int data)
{
    // Allocate space
    Node newNode
        = new Node();

    // Put in the data
    newNode.data = data;
    newNode.left = newNode.right = null;
    return newNode;
}

// Function to find digit sum of number
static int digitSum(int N)
{
    int sum = 0;
    while (N>0) {
        sum += N % 10;
        N /= 10;
    }
    return sum;
}

// Function to replace all the nodes
// with their digit sums using pre-order
static void replaceNodes(Node root)
{
    if (root==null)
        return;

    // Assigning digit sum value
    root.data = digitSum(root.data);

    // Calling left sub-tree
    replaceNodes(root.left);

    // Calling right sub-tree
    replaceNodes(root.right);
}

// Function to count subtrees that
// Sum up to a given value x
static int countSubtreesWithSumX(Node root, int x)
{
    // If tree is empty
    if (root==null)
        return 0;

    // Sum of nodes in the left subtree
    int ls = countSubtreesWithSumX(
        root.left,  x);

    // Sum of nodes in the right subtree
    int rs = countSubtreesWithSumX(
        root.right,  x);

    // Sum of nodes in the subtree rooted
    // with 'root.data'
    int sum = ls + rs + root.data;

    // If true
    if (sum == x)
        count++;

    // Return subtree's nodes sum
    return sum;
}

// Utility function to count subtrees that
// sum up to a given value x
static int countSubtreesWithSumXUtil(Node root, int x)
{
    // If tree is empty
    if (root==null)
        return 0;

    count = 0;

    // Sum of nodes in the left subtree
    int ls = countSubtreesWithSumX(
        root.left,  x);

    // sum of nodes in the right subtree
    int rs = countSubtreesWithSumX(
        root.right,  x);

    // If tree's nodes sum == x
    if ((ls + rs + root.data) == x)
        count++;

    // Required count of subtrees
    return count;
}

// Driver program to test above
public static void Main(String[] args)
{
    int N = 7;
    /* Binary tree creation
           10         
          /   \
        2       3
      /  \     /  \  
     9    3    4   7
    */
    Node root = getNode(10);
    root.left = getNode(2);
    root.right = getNode(3);
    root.left.left = getNode(9);
    root.left.right = getNode(3);
    root.right.left = getNode(4);
    root.right.right = getNode(7);

    // Replacing nodes with their
    // digit sum value
    replaceNodes(root);

    int X = 29;

    Console.Write(countSubtreesWithSumXUtil(root, X));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

    // JavaScript Program to implement
    // the above approach

    // Structure of a node of binary tree
    class Node {
        constructor(data) {
            this.data = data;
            this.left = null;
            this.right = null;
        }
    };

    // Function to get a new node
    function getNode(data) {
        // Allocate space
        let newNode
            = new Node(data);
        return newNode;
    }

    // Function to find digit sum of number
    function digitSum(N) {
        let sum = 0;
        while (N) {
            sum += N % 10;
            N = Math.floor(N / 10);
        }
        return sum;
    }

    // Function to replace all the nodes
    // with their digit sums using pre-order
    function replaceNodes(root) {
        if (!root)
            return;

        // Assigning digit sum value
        root.data = digitSum(root.data);

        // Calling left sub-tree
        replaceNodes(root.left);

        // Calling right sub-tree
        replaceNodes(root.right);
    }

    // Function to count subtrees that
    // Sum up to a given value x
    function countSubtreesWithSumX(root,
        count, x) {
        // If tree is empty
        if (!root)
            return 0;

        // Sum of nodes in the left subtree
        let ls = countSubtreesWithSumX(
            root.left, count, x);

        // Sum of nodes in the right subtree
        let rs = countSubtreesWithSumX(
            root.right, count, x);

        // Sum of nodes in the subtree rooted
        // with 'root.data'
        let sum = ls + rs + root.data;

        // If true
        if (sum == x)
            count++;

        // Return subtree's nodes sum
        return sum;
    }

    // Utility function to count subtrees that
    // sum up to a given value x
    function countSubtreesWithSumXUtil(root, x) {
        // If tree is empty
        if (!root)
            return 0;

        let count = 0;

        // Sum of nodes in the left subtree
        let ls = countSubtreesWithSumX(
            root.left, count, x);

        // sum of nodes in the right subtree
        let rs = countSubtreesWithSumX(
            root.right, count, x);

        // If tree's nodes sum == x
        if ((ls + rs + root.data) == x)
            count++;

        // Required count of subtrees
        return count;
    }

    // Driver program to test above

    let N = 7;
    /* Binary tree creation
           10         
          /   \
        2       3
      /  \     /  \  
     9    3    4   7
    */
    let root = getNode(10);
    root.left = getNode(2);
    root.right = getNode(3);
    root.left.left = getNode(9);
    root.left.right = getNode(3);
    root.right.left = getNode(4);
    root.right.right = getNode(7);

    // Replacing nodes with their
    // digit sum value
    replaceNodes(root);

    let X = 29;

    document.write(countSubtreesWithSumXUtil(root, X));

// This code is contributed by Potta Lokesh
</script>
```

**Output**

```
1
```

**时间复杂度:** O(N)。
**辅助空间:** O(1)。