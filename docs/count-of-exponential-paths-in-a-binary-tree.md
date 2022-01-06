# 二叉树中指数路径的计数

> 原文:[https://www . geesforgeks . org/二叉树中指数路径的计数/](https://www.geeksforgeeks.org/count-of-exponential-paths-in-a-binary-tree/)

给定一棵[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是计算给定二叉树中指数路径的数量。

> **指数路径**是这样一条路径，其中[根到叶路径](https://www.geeksforgeeks.org/given-a-binary-tree-print-all-root-to-leaf-paths/)包含等于 x <sup>y</sup> 、&的所有节点，其中 x 是最小可能正常数& y 是可变正整数。

**示例:**

```
Input:
             27
           /    \
          9      81
         / \    /  \
        3  10  70   243
                   /   \
                  81   909
Output: 2 
Explanation:
There are 2 exponential path for
the above Binary Tree, for x = 3,
Path 1: 27 -> 9 -> 3
Path 2: 27 -> 81 -> 243 -> 81

Input:
             8
           /    \
          4      81
         / \    /  \
        3   2  70   243
                   /   \
                  81   909
Output: 1
```

**方法:**想法是使用 Preorder [树遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。在给定二叉树的[前序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)期间，执行以下操作:

1.  首先找出 x 的值，其中 x<sup>y</sup>=根& x 是最小可能的& y > 0。
2.  如果节点的当前值对于某些 y > 0 不等于 x <sup>y</sup> ，或者指针变为**空**，则返回计数。
3.  如果当前节点是叶节点，则将计数增加 1。
4.  用更新的计数递归调用左**和右**子树。****
5.  ****在所有递归调用之后，count 的值是给定二叉树的指数路径数。****

******以下是上述方法的实现:******

## ****C++****

```
**// C++ program to find the count
// exponential paths in Binary Tree

#include <bits/stdc++.h>
using namespace std;

// A Tree node
struct Node {
    int key;
    struct Node *left, *right;
};

// Function to create a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left
        = temp->right
        = NULL;
    return (temp);
}

// function to find x
int find_x(int n)
{
    if (n == 1)
        return 1;

    double num, den, p;

    // Take log10 of n
    num = log10(n);

    int x, no;

    for (int i = 2; i <= n; i++) {
        den = log10(i);

        // Log(n) with base i
        p = num / den;

        // Raising i to the power p
        no = (int)(pow(i, int(p)));

        if (abs(no - n) < 1e-6) {
            x = i;
            break;
        }
    }

    return x;
}

// function To check
// whether the given node
// equals to x^y for some y>0
bool is_key(int n, int x)
{
    double p;

    // Take logx(n) with base x
    p = log10(n) / log10(x);

    int no = (int)(pow(x, int(p)));

    if (n == no)
        return true;

    return false;
}

// Utility function to count
// the exponent path
// in a given Binary tree
int evenPaths(struct Node* node,
              int count, int x)
{

    // Base Condition, when node pointer
    // becomes null or node value is not
    // a number of pow(x, y )
    if (node == NULL
        || !is_key(node->key, x)) {
        return count;
    }

    // Increment count when
    // encounter leaf node
    if (!node->left
        && !node->right) {
        count++;
    }

    // Left recursive call
    // save the value of count
    count = evenPaths(
        node->left, count, x);

    // Right recursive call and
    // return value of count
    return evenPaths(
        node->right, count, x);
}

// function to count exponential paths
int countExpPaths(
    struct Node* node, int x)
{
    return evenPaths(node, 0, x);
}

// Driver Code
int main()
{

    // create Tree
    Node* root = newNode(27);
    root->left = newNode(9);
    root->right = newNode(81);

    root->left->left = newNode(3);
    root->left->right = newNode(10);

    root->right->left = newNode(70);
    root->right->right = newNode(243);
    root->right->right->left = newNode(81);
    root->right->right->right = newNode(909);

    // retrieve the value of x
    int x = find_x(root->key);

    // Function call
    cout << countExpPaths(root, x);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program to find the count
// exponential paths in Binary Tree
import java.util.*;
import java.lang.*;

class GFG{

// Structure of a Tree node
static class Node
{
    int key;
    Node left, right;
}

// Function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to find x
static int find_x(int n)
{
    if (n == 1)
        return 1;

    double num, den, p;

    // Take log10 of n
    num = Math.log10(n);

    int x = 0, no = 0;

    for(int i = 2; i <= n; i++)
    {
        den = Math.log10(i);

        // Log(n) with base i
        p = num / den;

        // Raising i to the power p
        no = (int)(Math.pow(i, (int)p));

        if (Math.abs(no - n) < 1e-6)
        {
            x = i;
            break;
        }
    }
    return x;
}

// Function to check whether the
// given node equals to x^y for some y>0
static boolean is_key(int n, int x)
{
    double p;

    // Take logx(n) with base x
    p = Math.log10(n) / Math.log10(x);

    int no = (int)(Math.pow(x, (int)p));

    if (n == no)
        return true;

    return false;
}

// Utility function to count
// the exponent path in a
// given Binary tree
static int evenPaths(Node node, int count,
                                int x)
{

    // Base Condition, when node pointer
    // becomes null or node value is not
    // a number of pow(x, y )
    if (node == null || !is_key(node.key, x))
    {
        return count;
    }

    // Increment count when
    // encounter leaf node
    if (node.left == null &&
       node.right == null)
    {
        count++;
    }

    // Left recursive call
    // save the value of count
    count = evenPaths(node.left,
                      count, x);

    // Right recursive call and
    // return value of count
    return evenPaths(node.right,
                     count, x);
}

// Function to count exponential paths
static int countExpPaths(Node node, int x)
{
    return evenPaths(node, 0, x);
} 

// Driver code
public static void main(String[] args)
{

    // Create Tree
    Node root = newNode(27);
    root.left = newNode(9);
    root.right = newNode(81);

    root.left.left = newNode(3);
    root.left.right = newNode(10);

    root.right.left = newNode(70);
    root.right.right = newNode(243);
    root.right.right.left = newNode(81);
    root.right.right.right = newNode(909);

    // Retrieve the value of x
    int x = find_x(root.key);

    // Function call
    System.out.println(countExpPaths(root, x));
}
}

// This code is contributed by offbeat**
```

## ****蟒蛇 3****

```
**# Python3 program to find the count
# exponential paths in Binary Tree
import math

# Structure of a Tree node
class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

# Function to create a new node
def newNode(key):
    temp = Node(key)
    return temp

# Function to find x
def find_x(n):
    if n == 1:
        return 1

    # Take log10 of n
    num = math.log10(n)

    x, no = 0, 0

    for i in range(2, n + 1):
        den = math.log10(i)

        # Log(n) with base i
        p = num / den

        # Raising i to the power p
        no = int(pow(i, int(p)))

        if abs(no - n) < 1e-6:
            x = i
            break
    return x

# Function to check whether the
# given node equals to x^y for some y>0
def is_key(n, x):
    # Take logx(n) with base x
    p = math.log10(n) / math.log10(x)

    no = int(pow(x, int(p)))

    if n == no:
        return True
    return False

# Utility function to count
# the exponent path in a
# given Binary tree
def evenPaths(node, count, x):
    # Base Condition, when node pointer
    # becomes null or node value is not
    # a number of pow(x, y )
    if node == None or not is_key(node.key, x):
        return count

    # Increment count when
    # encounter leaf node
    if node.left == None and node.right == None:
        count+=1

    # Left recursive call
    # save the value of count
    count = evenPaths(node.left, count, x)

    # Right recursive call and
    # return value of count
    return evenPaths(node.right, count, x)

# Function to count exponential paths
def countExpPaths(node, x):
    return evenPaths(node, 0, x)

# Create Tree
root = newNode(27)
root.left = newNode(9)
root.right = newNode(81)

root.left.left = newNode(3)
root.left.right = newNode(10)

root.right.left = newNode(70)
root.right.right = newNode(243)
root.right.right.left = newNode(81)
root.right.right.right = newNode(909)

# Retrieve the value of x
x = find_x(root.key)

# Function call
print(countExpPaths(root, x))

# This code is contributed by divyeshrabadiya07.**
```

## ****C#****

```
**// C# program to find the count
// exponential paths in Binary Tree
using System;

class GFG{

// Structure of a Tree node
public class Node
{
    public int key;
    public Node left, right;
}

// Function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to find x
static int find_x(int n)
{
    if (n == 1)
        return 1;

    double num, den, p;

    // Take log10 of n
    num = Math.Log10(n);

    int x = 0, no = 0;

    for(int i = 2; i <= n; i++)
    {
        den = Math.Log10(i);

        // Log(n) with base i
        p = num / den;

        // Raising i to the power p
        no = (int)(Math.Pow(i, (int)p));

        if (Math.Abs(no - n) < 0.000001)
        {
            x = i;
            break;
        }
    }
    return x;
}

// Function to check whether the
// given node equals to x^y for some y>0
static bool is_key(int n, int x)
{
    double p;

    // Take logx(n) with base x
    p = Math.Log10(n) / Math.Log10(x);

    int no = (int)(Math.Pow(x, (int)p));

    if (n == no)
        return true;

    return false;
}

// Utility function to count
// the exponent path in a
// given Binary tree
static int evenPaths(Node node, int count,
                                int x)
{

    // Base Condition, when node pointer
    // becomes null or node value is not
    // a number of pow(x, y )
    if (node == null || !is_key(node.key, x))
    {
        return count;
    }

    // Increment count when
    // encounter leaf node
    if (node.left == null &&
       node.right == null)
    {
        count++;
    }

    // Left recursive call
    // save the value of count
    count = evenPaths(node.left,
                      count, x);

    // Right recursive call and
    // return value of count
    return evenPaths(node.right,
                     count, x);
}

// Function to count exponential paths
static int countExpPaths(Node node, int x)
{
    return evenPaths(node, 0, x);
} 

// Driver code
public static void Main(string[] args)
{

    // Create Tree
    Node root = newNode(27);
    root.left = newNode(9);
    root.right = newNode(81);

    root.left.left = newNode(3);
    root.left.right = newNode(10);

    root.right.left = newNode(70);
    root.right.right = newNode(243);
    root.right.right.left = newNode(81);
    root.right.right.right = newNode(909);

    // Retrieve the value of x
    int x = find_x(root.key);

    // Function call
    Console.Write(countExpPaths(root, x));
}
}

// This code is contributed by rutvik_56**
```

## ****java 描述语言****

```
**<script>

// Javascript program to find the count
// exponential paths in Binary Tree

// Structure of a Tree node
class Node
{
    constructor(key)
    {
        this.left = null;
        this.right = null;
        this.key = key;
    }
}

// Function to create a new node
function newNode(key)
{
    let temp = new Node(key);
    return (temp);
}

// Function to find x
function find_x(n)
{
    if (n == 1)
        return 1;

    let num, den, p;

    // Take log10 of n
    num = Math.log10(n);

    let x = 0, no = 0;

    for(let i = 2; i <= n; i++)
    {
        den = Math.log10(i);

        // Log(n) with base i
        p = num / den;

        // Raising i to the power p
        no = parseInt(Math.pow(
            i, parseInt(p, 10)), 10);

        if (Math.abs(no - n) < 1e-6)
        {
            x = i;
            break;
        }
    }
    return x;
}

// Function to check whether the
// given node equals to x^y for some y>0
function is_key(n, x)
{
    let p;

    // Take logx(n) with base x
    p = Math.log10(n) / Math.log10(x);

    let no = parseInt(Math.pow(
        x, parseInt(p, 10)), 10);

    if (n == no)
        return true;

    return false;
}

// Utility function to count
// the exponent path in a
// given Binary tree
function evenPaths(node, count, x)
{

    // Base Condition, when node pointer
    // becomes null or node value is not
    // a number of pow(x, y )
    if (node == null || !is_key(node.key, x))
    {
        return count;
    }

    // Increment count when
    // encounter leaf node
    if (node.left == null &&
       node.right == null)
    {
        count++;
    }

    // Left recursive call
    // save the value of count
    count = evenPaths(node.left,
                      count, x);

    // Right recursive call and
    // return value of count
    return evenPaths(node.right,
                     count, x);
}

// Function to count exponential paths
function countExpPaths(node, x)
{
    return evenPaths(node, 0, x);
}

// Driver code

// Create Tree
let root = newNode(27);
root.left = newNode(9);
root.right = newNode(81);

root.left.left = newNode(3);
root.left.right = newNode(10);

root.right.left = newNode(70);
root.right.right = newNode(243);
root.right.right.left = newNode(81);
root.right.right.right = newNode(909);

// Retrieve the value of x
let x = find_x(root.key);

// Function call
document.write(countExpPaths(root, x));

// This code is contributed by mukesh07 

</script>**
```

******Output:** 

```
2
```****