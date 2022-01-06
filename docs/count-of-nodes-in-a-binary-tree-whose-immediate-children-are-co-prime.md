# 二叉树中直接子节点为同素的节点数

> 原文:[https://www . geeksforgeeks . org/二进制树中的节点数-其直系子女是同素的/](https://www.geeksforgeeks.org/count-of-nodes-in-a-binary-tree-whose-immediate-children-are-co-prime/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是计算其直系子节点是同素的节点。

**示例:**

```
Input: 
                  1
                /   \ 
              15     5
             /  \   /  \ 
            11   2 4     15 
                    \    / 
                     2  3  
Output: 2
Explanation: 
Children of 15 (11, 2) are co-prime
Children of 5 (4, 15) are co-prime

Input:
                 7
                /  \ 
              21     14 
             /  \      \
            77   16     3 
           / \         / \
          2   5       10  11
                      /
                     23 
Output:3
Explanation: 
Children of 21 (77, 8) are co-prime
Children of 77 (2, 5) are co-prime
Children of 3 (10, 11) are co-prime 
```

**方法:**想法是:

1.  对树进行[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)
2.  对于每个节点，检查它的两个子节点都不为空
3.  如果为真，则检查两个子的[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)是否为 1。
4.  如果是，那么统计这样的节点并在最后打印。

下面是上述方法的实现:

## C++

```
// C++ program for Counting nodes
// whose immediate children
// are co-prime

#include <bits/stdc++.h>
using namespace std;

// Structure of node
struct Node {
    int key;
    struct Node *left, *right;
};

// Utility function to
// create a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// Function to check and print if
// two nodes are co-prime or not
bool coprime(struct Node* a,
             struct Node* b)
{

    if (__gcd(a->key, b->key) == 1)
        return true;
    else
        return false;
}

// Function to get the count of
// Nodes whose immediate children
// are co-prime in a binary tree
unsigned int getCount(struct Node* node)
{
    // Base Case
    if (!node)
        return 0;

    queue<Node*> q;

    // Do level order traversal
    // starting from root
    int count = 0;
    q.push(node);

    while (!q.empty()) {
        struct Node* temp = q.front();
        q.pop();

        if (temp->left && temp->right) {
            if (coprime(temp->left,
                        temp->right))
                count++;
        }

        if (temp->left != NULL)
            q.push(temp->left);
        if (temp->right != NULL)
            q.push(temp->right);
    }
    return count;
}

// Function to find total
// number of nodes
// In a given binary tree
int findSize(struct Node* node)
{
    // Base condition
    if (node == NULL)
        return 0;

    return 1
           + findSize(node->left)
           + findSize(node->right);
}

// Function to create Tree
// and find the count of nodes
// whose immediate children
// are co-prime
void findCount()
{
    /*         10
            /  \
          48   12
              /  \
            18    35
           / \    / \
          21 29  43 16
                 /
                7
    */

    // Create Binary Tree
    Node* root = newNode(10);
    root->left = newNode(48);
    root->right = newNode(12);

    root->right->left = newNode(18);
    root->right->right = newNode(35);

    root->right->left->left = newNode(21);
    root->right->left->right = newNode(29);
    root->right->right->left = newNode(43);
    root->right->right->right = newNode(16);
    root->right->right->right->left = newNode(7);

    // Print all nodes
    // with Co-Prime children
    cout << getCount(root) << endl;
}

// Driver Code
int main()
{
    // Function Call
    findCount();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Counting nodes
// whose immediate children
// are co-prime
import java.util.*;

class GFG{

// Structure of node
static class Node {
    int key;
    Node left, right;
};

// Utility function to
// create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to check and print if
// two nodes are co-prime or not
static boolean coprime(Node a,
             Node b)
{

    if (__gcd(a.key, b.key) == 1)
        return true;
    else
        return false;
}

// Function to get the count of
// Nodes whose immediate children
// are co-prime in a binary tree
static int getCount(Node node)
{
    // Base Case
    if (node == null)
        return 0;

    Queue<Node> q = new LinkedList<Node>();

    // Do level order traversal
    // starting from root
    int count = 0;
    q.add(node);

    while (!q.isEmpty()) {
        Node temp = q.peek();
        q.remove();

        if (temp.left != null && temp.right != null) {
            if (coprime(temp.left,
                        temp.right))
                count++;
        }

        if (temp.left != null)
            q.add(temp.left);
        if (temp.right != null)
            q.add(temp.right);
    }
    return count;
}

// Function to find total
// number of nodes
// In a given binary tree
static int findSize(Node node)
{
    // Base condition
    if (node == null)
        return 0;

    return 1
           + findSize(node.left)
           + findSize(node.right);
}

// Function to create Tree
// and find the count of nodes
// whose immediate children
// are co-prime
static void findCount()
{
    /*         10
            /  \
          48   12
              /  \
            18    35
           / \    / \
          21 29  43 16
                 /
                7
    */

    // Create Binary Tree
    Node root = newNode(10);
    root.left = newNode(48);
    root.right = newNode(12);

    root.right.left = newNode(18);
    root.right.right = newNode(35);

    root.right.left.left = newNode(21);
    root.right.left.right = newNode(29);
    root.right.right.left = newNode(43);
    root.right.right.right = newNode(16);
    root.right.right.right.left = newNode(7);

    // Print all nodes
    // with Co-Prime children
    System.out.print(getCount(root) +"\n");
}
static int __gcd(int a, int b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}

// Driver Code
public static void main(String[] args)
{
    // Function Call
    findCount();

}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for counting nodes
# whose immediate children
# are co-prime
from collections import deque as queue
from math import gcd as __gcd

# A Binary Tree Node
class Node:

    def __init__(self, key):

        self.data = key
        self.left = None
        self.right = None

# Function to check and prif
# two nodes are co-prime or not
def coprime(a, b):

    if (__gcd(a.data, b.data) == 1):
        return True
    else:
        return False

# Function to get the count of
# Nodes whose immediate children
# are co-prime in a binary tree
def getCount(node):

    # Base Case
    if (not node):
        return 0

    q = queue()

    # Do level order traversal
    # starting from root
    count = 0
    q.append(node)

    while (len(q) > 0):
        temp = q.popleft()
        #q.pop()

        if (temp.left and temp.right):
            if (coprime(temp.left, temp.right)):
                count += 1

        if (temp.left != None):
            q.append(temp.left)
        if (temp.right != None):
            q.append(temp.right)

    return count

# Function to find total
# number of nodes
# In a given binary tree
def findSize(node):

    # Base condition
    if (node == None):
        return 0

    return (1 + findSize(node.left) +
                findSize(node.right))

# Function to create Tree
# and find the count of nodes
# whose immediate children
# are co-prime
def findCount():

    #          10
    #         /  \
    #       48   12
    #           /  \
    #         18    35
    #        / \    / \
    #       21 29  43 16
    #              /
    #             7
    #

    # Create Binary Tree
    root = Node(10)
    root.left = Node(48)
    root.right = Node(12)

    root.right.left = Node(18)
    root.right.right = Node(35)

    root.right.left.left = Node(21)
    root.right.left.right = Node(29)
    root.right.right.left = Node(43)
    root.right.right.right = Node(16)
    root.right.right.right.left = Node(7)

    # Print all nodes
    # with Co-Prime children
    print(getCount(root))

# Driver Code
if __name__ == '__main__':

    # Function Call
    findCount()

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for Counting nodes
// whose immediate children
// are co-prime
using System;
using System.Collections.Generic;

class GFG{

// Structure of node
class Node {
    public int key;
    public Node left, right;
};

// Utility function to
// create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Function to check and print if
// two nodes are co-prime or not
static bool coprime(Node a,
             Node b)
{

    if (__gcd(a.key, b.key) == 1)
        return true;
    else
        return false;
}

// Function to get the count of
// Nodes whose immediate children
// are co-prime in a binary tree
static int getCount(Node node)
{
    // Base Case
    if (node == null)
        return 0;

    List<Node> q = new List<Node>();

    // Do level order traversal
    // starting from root
    int count = 0;
    q.Add(node);

    while (q.Count != 0) {
        Node temp = q[0];
        q.RemoveAt(0);

        if (temp.left != null && temp.right != null) {
            if (coprime(temp.left,
                        temp.right))
                count++;
        }

        if (temp.left != null)
            q.Add(temp.left);
        if (temp.right != null)
            q.Add(temp.right);
    }
    return count;
}

// Function to find total
// number of nodes
// In a given binary tree
static int findSize(Node node)
{
    // Base condition
    if (node == null)
        return 0;

    return 1
           + findSize(node.left)
           + findSize(node.right);
}

// Function to create Tree
// and find the count of nodes
// whose immediate children
// are co-prime
static void findCount()
{
    /*         10
            /  \
          48   12
              /  \
            18    35
           / \    / \
          21 29  43 16
                 /
                7
    */

    // Create Binary Tree
    Node root = newNode(10);
    root.left = newNode(48);
    root.right = newNode(12);

    root.right.left = newNode(18);
    root.right.right = newNode(35);

    root.right.left.left = newNode(21);
    root.right.left.right = newNode(29);
    root.right.right.left = newNode(43);
    root.right.right.right = newNode(16);
    root.right.right.right.left = newNode(7);

    // Print all nodes
    // with Co-Prime children
    Console.Write(getCount(root) +"\n");
}
static int __gcd(int a, int b) 
{ 
    return b == 0? a:__gcd(b, a % b);    
}

// Driver Code
public static void Main(String[] args)
{
    // Function Call
    findCount();
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for counting nodes
// whose immediate children are co-prime

// Structure of node
class Node
{

    // Utility function to
    // create a new node
    constructor(key)
    {
        this.key = key;
        this.left = this.right = null;
    }
}

// Function to check and print if
// two nodes are co-prime or not
function coprime(a, b)
{
    if (__gcd(a.key, b.key) == 1)
        return true;
    else
        return false;
}

// Function to get the count of
// Nodes whose immediate children
// are co-prime in a binary tree
function getCount(node)
{

    // Base Case
    if (node == null)
        return 0;

    let q = [];

    // Do level order traversal
    // starting from root
    let count = 0;
    q.push(node);

    while (q.length != 0)
    {
        let temp = q.shift();

        if (temp.left != null &&
            temp.right != null)
        {
            if (coprime(temp.left,
                        temp.right))
                count++;
        }

        if (temp.left != null)
            q.push(temp.left);
        if (temp.right != null)
            q.push(temp.right);
    }
    return count;
}

// Function to find total
// number of nodes
// In a given binary tree
function findSize(node)
{

    // Base condition
    if (node == null)
        return 0;

    return 1 + findSize(node.left) +
               findSize(node.right);
}

// Function to create Tree
// and find the count of nodes
// whose immediate children
// are co-prime
function findCount()
{

    /*       10
            /  \
          48   12
              /  \
            18    35
           / \    / \
          21 29  43 16
                 /
                7
    */

    // Create Binary Tree
    let root = new Node(10);
    root.left = new Node(48);
    root.right = new Node(12);

    root.right.left = new Node(18);
    root.right.right = new Node(35);

    root.right.left.left = new Node(21);
    root.right.left.right = new Node(29);
    root.right.right.left = new Node(43);
    root.right.right.right = new Node(16);
    root.right.right.right.left = new Node(7);

    // Print all nodes
    // with Co-Prime children
    document.write(getCount(root) + "<br>");
}

function  __gcd(a,b)
{
    return b == 0? a:__gcd(b, a % b);   
}

// Driver Code

// Function Call
findCount();

// This code is contributed by patel2127

</script>
```

**Output:** 

```
3
```

**<u>复杂度分析:</u>**

**时间复杂度:** O(N*logV)，其中 V 是树中节点的权重。

在 bfs 中，树的每个节点都被处理一次，因此如果树中总共有 N 个节点，由于 bfs 而导致的复杂性是 O(N)。此外，在处理每个节点时，为了检查节点值是否是同素的，正在调用内置的 __gcd(A，B)函数，其中 A，B 是节点的权重，并且该函数的复杂度为 O(log(min(A，B))，因此对于每个节点，都有 O(logV)的额外复杂度。因此，时间复杂度为 O(N*logV)。

**辅助空间:** O(w)，其中 w 为树的最大宽度。