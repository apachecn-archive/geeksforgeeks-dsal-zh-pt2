# 二叉树中斐波那契路径的计数

> 原文:[https://www . geeksforgeeks . org/Fibonacci 路径在二叉树中的计数/](https://www.geeksforgeeks.org/count-of-fibonacci-paths-in-a-binary-tree/)

给定一棵[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是计算给定二叉树中[斐波那契](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)路径的数量。

> **斐波那契路径**是包含[根到叶路径](https://www.geeksforgeeks.org/given-a-binary-tree-print-all-root-to-leaf-paths/)中所有节点的路径，是[斐波那契数列](https://www.geeksforgeeks.org/python-program-for-nth-multiple-of-a-number-in-fibonacci-series/)的术语。

**示例:**

```
Input:
             0
           /    \
          1      1
         / \    /  \
        1  10  70   1
                   /  \
                  81   2
Output: 2 
Explanation:
There are 2 Fibonacci path for
the above Binary Tree, for x = 3,
Path 1: 0 1 1
Path 2: 0 1 1 2

Input:
             8
           /    \
          4      81
         / \    /  \
        3   2  70   243
                   /   \
                  81   909
Output: 0
```

**方法:**思路是使用[预序树遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。在给定二叉树的前序遍历期间，请执行以下操作:

1.  首先计算二叉树的[高度。](https://www.geeksforgeeks.org/write-a-c-program-to-find-the-maximum-depth-or-height-of-a-tree/)
2.  现在创建一个长度等于树高的向量，这样它包含[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。
3.  如果斐波那契数列或指针的第 i <sup>个</sup>级节点的当前值不等于第 i <sup>个</sup>项，则返回计数。
4.  如果当前节点是叶节点，则将计数增加 1。
5.  用更新的计数递归调用左**和右**子树。****
6.  ****在全递归调用之后，count 的值是给定二叉树的斐波那契路径数。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program to count all of
// Fibonacci paths in a Binary tree

#include <bits/stdc++.h>
using namespace std;

// Vector to store the fibonacci series
vector<int> fib;

// Binary Tree Node
struct node {
    struct node* left;
    int data;
    struct node* right;
};

// Function to create a new tree node
node* newNode(int data)
{
    node* temp = new node;
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

// Function to find the height
// of the given tree
int height(node* root)
{
    int ht = 0;
    if (root == NULL)
        return 0;

    return (max(height(root->left),
                height(root->right))
            + 1);
}

// Function to make fibonacci series
// upto n terms
void FibonacciSeries(int n)
{
    fib.push_back(0);
    fib.push_back(1);
    for (int i = 2; i < n; i++)
        fib.push_back(fib[i - 1]
                      + fib[i - 2]);
}

// Preorder Utility function to count
// exponent path in a given Binary tree
int CountPathUtil(node* root,
                  int i, int count)
{

    // Base Condition, when node pointer
    // becomes null or node value is not
    // a number of pow(x, y )
    if (root == NULL
        || !(fib[i] == root->data)) {
        return count;
    }

    // Increment count when
    // encounter leaf node
    if (!root->left
        && !root->right) {
        count++;
    }

    // Left recursive call
    // save the value of count
    count = CountPathUtil(
        root->left, i + 1, count);

    // Right recursive call and
    // return value of count
    return CountPathUtil(
        root->right, i + 1, count);
}

// Function to find whether
// fibonacci path exists or not
void CountPath(node* root)
{
    // To find the height
    int ht = height(root);

    // Making fibonacci series
    // upto ht terms
    FibonacciSeries(ht);

    cout << CountPathUtil(root, 0, 0);
}

// Driver code
int main()
{
    // Create binary tree
    node* root = newNode(0);

    root->left = newNode(1);
    root->right = newNode(1);

    root->left->left = newNode(1);
    root->left->right = newNode(4);
    root->right->right = newNode(1);
    root->right->right->left = newNode(2);

    // Function Call
    CountPath(root);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program to count all of
// Fibonacci paths in a Binary tree
import java.util.*;

class GFG{

// Vector to store the fibonacci series
static Vector<Integer> fib = new Vector<Integer>();

// Binary Tree Node
static class node {
    node left;
    int data;
    node right;
};

// Function to create a new tree node
static node newNode(int data)
{
    node temp = new node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Function to find the height
// of the given tree
static int height(node root)
{
    if (root == null)
        return 0;

    return (Math.max(height(root.left),
                height(root.right))
            + 1);
}

// Function to make fibonacci series
// upto n terms
static void FibonacciSeries(int n)
{
    fib.add(0);
    fib.add(1);
    for (int i = 2; i < n; i++)
        fib.add(fib.get(i - 1)
                    + fib.get(i - 2));
}

// Preorder Utility function to count
// exponent path in a given Binary tree
static int CountPathUtil(node root,
                int i, int count)
{

    // Base Condition, when node pointer
    // becomes null or node value is not
    // a number of Math.pow(x, y )
    if (root == null
        || !(fib.get(i) == root.data)) {
        return count;
    }

    // Increment count when
    // encounter leaf node
    if (root.left != null
        && root.right != null) {
        count++;
    }

    // Left recursive call
    // save the value of count
    count = CountPathUtil(
        root.left, i + 1, count);

    // Right recursive call and
    // return value of count
    return CountPathUtil(
        root.right, i + 1, count);
}

// Function to find whether
// fibonacci path exists or not
static void CountPath(node root)
{
    // To find the height
    int ht = height(root);

    // Making fibonacci series
    // upto ht terms
    FibonacciSeries(ht);

    System.out.print(CountPathUtil(root, 0, 0));
}

// Driver code
public static void main(String[] args)
{
    // Create binary tree
    node root = newNode(0);

    root.left = newNode(1);
    root.right = newNode(1);

    root.left.left = newNode(1);
    root.left.right = newNode(4);
    root.right.right = newNode(1);
    root.right.right.left = newNode(2);

    // Function Call
    CountPath(root);

}
}

// This code is contributed by 29AjayKumar**
```

## ****蟒蛇 3****

```
**# Python3 program to count all of
# Fibonacci paths in a Binary tree

# Vector to store the fibonacci series
fib = []

# Binary Tree Node
class node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# Function to create a new tree node
def newNode(data):

    temp = node(data)
    return temp

# Function to find the height
# of the given tree
def height(root):

    ht = 0

    if (root == None):
        return 0

    return (max(height(root.left),
                height(root.right)) + 1)

# Function to make fibonacci series
# upto n terms
def FibonacciSeries(n):

    fib.append(0)
    fib.append(1)

    for i in range(2, n):
        fib.append(fib[i - 1] + fib[i - 2])

# Preorder Utility function to count
# exponent path in a given Binary tree
def CountPathUtil(root, i, count):

    # Base Condition, when node pointer
    # becomes null or node value is not
    # a number of pow(x, y )
    if (root == None or not (fib[i] == root.data)):
        return count

    # Increment count when
    # encounter leaf node
    if (not root.left and not root.right):
        count += 1

    # Left recursive call
    # save the value of count
    count = CountPathUtil(root.left, i + 1, count)

    # Right recursive call and
    # return value of count
    return CountPathUtil(root.right, i + 1, count)

# Function to find whether
# fibonacci path exists or not
def CountPath(root):

    # To find the height
    ht = height(root)

    # Making fibonacci series
    # upto ht terms
    FibonacciSeries(ht)

    print(CountPathUtil(root, 0, 0))

# Driver code
if __name__=='__main__':

    # Create binary tree
    root = newNode(0)

    root.left = newNode(1)
    root.right = newNode(1)

    root.left.left = newNode(1)
    root.left.right = newNode(4)
    root.right.right = newNode(1)
    root.right.right.left = newNode(2)

    # Function Call
    CountPath(root)

# This code is contributed by rutvik_56**
```

## ****C#****

```
**// C# program to count all of
// Fibonacci paths in a Binary tree
using System;
using System.Collections.Generic;

class GFG{

// List to store the fibonacci series
static List<int> fib = new List<int>();

// Binary Tree Node
class node {
    public node left;
    public int data;
    public node right;
};

// Function to create a new tree node
static node newNode(int data)
{
    node temp = new node();
    temp.data = data;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Function to find the height
// of the given tree
static int height(node root)
{
    if (root == null)
        return 0;

    return (Math.Max(height(root.left),
                height(root.right))
            + 1);
}

// Function to make fibonacci series
// upto n terms
static void FibonacciSeries(int n)
{
    fib.Add(0);
    fib.Add(1);
    for (int i = 2; i < n; i++)
        fib.Add(fib[i - 1]
                    + fib[i - 2]);
}

// Preorder Utility function to count
// exponent path in a given Binary tree
static int CountPathUtil(node root,
                int i, int count)
{

    // Base Condition, when node pointer
    // becomes null or node value is not
    // a number of Math.Pow(x, y)
    if (root == null
        || !(fib[i] == root.data)) {
        return count;
    }

    // Increment count when
    // encounter leaf node
    if (root.left != null
        && root.right != null) {
        count++;
    }

    // Left recursive call
    // save the value of count
    count = CountPathUtil(
        root.left, i + 1, count);

    // Right recursive call and
    // return value of count
    return CountPathUtil(
        root.right, i + 1, count);
}

// Function to find whether
// fibonacci path exists or not
static void CountPath(node root)
{
    // To find the height
    int ht = height(root);

    // Making fibonacci series
    // upto ht terms
    FibonacciSeries(ht);

    Console.Write(CountPathUtil(root, 0, 0));
}

// Driver code
public static void Main(String[] args)
{
    // Create binary tree
    node root = newNode(0);

    root.left = newNode(1);
    root.right = newNode(1);

    root.left.left = newNode(1);
    root.left.right = newNode(4);
    root.right.right = newNode(1);
    root.right.right.left = newNode(2);

    // Function Call
    CountPath(root);
}
}

// This code is contributed by Princi Singh**
```

## ****java 描述语言****

```
**<script>

    // JavaScript program to count all of
    // Fibonacci paths in a Binary tree

    // Vector to store the fibonacci series
    let fib = [];

    // Binary Tree Node
    class node {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    };

    // Function to create a new tree node
    function newNode(data)
    {
        let temp = new node(data);
        return temp;
    }

    // Function to find the height
    // of the given tree
    function height(root)
    {
        if (root == null)
            return 0;

        return (Math.max(height(root.left),
                    height(root.right))
                + 1);
    }

    // Function to make fibonacci series
    // upto n terms
    function FibonacciSeries(n)
    {
        fib.push(0);
        fib.push(1);
        for (let i = 2; i < n; i++)
            fib.push(fib[i - 1] + fib[i - 2]);
    }

    // Preorder Utility function to count
    // exponent path in a given Binary tree
    function CountPathUtil(root, i, count)
    {

        // Base Condition, when node pointer
        // becomes null or node value is not
        // a number of Math.pow(x, y )
        if (root == null
            || !(fib[i] == root.data)) {
            return count;
        }

        // Increment count when
        // encounter leaf node
        if (root.left != null
            && root.right != null) {
            count++;
        }

        // Left recursive call
        // save the value of count
        count = CountPathUtil(root.left, i + 1, count);

        // Right recursive call and
        // return value of count
        return CountPathUtil(root.right, i + 1, count);
    }

    // Function to find whether
    // fibonacci path exists or not
    function CountPath(root)
    {
        // To find the height
        let ht = height(root);

        // Making fibonacci series
        // upto ht terms
        FibonacciSeries(ht);

        document.write(CountPathUtil(root, 0, 0));
    }

    // Create binary tree
    let root = newNode(0);

    root.left = newNode(1);
    root.right = newNode(1);

    root.left.left = newNode(1);
    root.left.right = newNode(4);
    root.right.right = newNode(1);
    root.right.right.left = newNode(2);

    // Function Call
    CountPath(root);

</script>**
```

******Output:** 

```
2
```****