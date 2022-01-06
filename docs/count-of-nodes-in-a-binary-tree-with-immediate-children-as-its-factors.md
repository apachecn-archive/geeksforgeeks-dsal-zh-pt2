# 以直系子女为因子的二叉树节点数

> 原文:[https://www . geesforgeks . org/以直系子女为因子的二叉树节点数/](https://www.geeksforgeeks.org/count-of-nodes-in-a-binary-tree-with-immediate-children-as-its-factors/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是打印其直系子节点是其[因子](https://www.geeksforgeeks.org/program-to-find-all-factors-of-a-number-using-recursion/)的节点数。

**示例:**

```
Input: 
                  1
                /   \ 
              15     20
             /  \   /  \ 
            3    5 4     2 
                    \    / 
                     2  3  
Output: 2
Explanation: 
Children of 15 (3, 5)
 are factors of 15
Children of 20 (4, 2)
 are factors of 20

Input:
                  7
                /  \ 
              210   14 
             /  \      \
            70   14     30
           / \         / \
          2   5       10  15
                      /
                     23 
Output:3
Explanation: 
Children of 210 (70, 14)
 are factors of 210
Children of 70 (2, 5)
 are factors of 70
Children of 30 (10, 15)
 are factors of 30
```

**方法:**为了解决这个问题，我们需要以[级别顺序](https://www.geeksforgeeks.org/level-order-tree-traversal/)的方式遍历给定的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，对于每个有两个子节点的节点，检查两个子节点是否都有值，这些值是当前节点值的因子。如果是真的，那么计算这样的节点，并在最后打印出来。

下面是上述方法的实现:

## C++

```
// C++ program for Counting nodes
// whose immediate children
// are its factors

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

// Function to check and print if
// immediate children of a node
// are its factors or not
bool areChilrenFactors(
    struct Node* parent,
    struct Node* a,
    struct Node* b)
{
    if (parent->key % a->key == 0
        && parent->key % b->key == 0)
        return true;
    else
        return false;
}

// Function to get the
// count of full Nodes in
// a binary tree
unsigned int getCount(struct Node* node)
{
    // If tree is empty
    if (!node)
        return 0;
    queue<Node*> q;

    // Do level order traversal
    // starting from root
    int count = 0;
    // Store the number of nodes
    // with both children as factors
    q.push(node);
    while (!q.empty()) {
        struct Node* temp = q.front();
        q.pop();

        if (temp->left && temp->right) {
            if (areChilrenFactors(
                    temp, temp->left,
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

// Function to find total no of nodes
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

// Driver Code
int main()
{
    /*        10
            / \
           40 36
              / \
             18  12
             / \ / \
            2  6 3 4
                  /
                 7
    */

    // Create Binary Tree as shown
    Node* root = newNode(10);

    root->left = newNode(40);
    root->right = newNode(36);

    root->right->left = newNode(18);
    root->right->right = newNode(12);

    root->right->left->left = newNode(2);
    root->right->left->right = newNode(6);
    root->right->right->left = newNode(3);
    root->right->right->right = newNode(4);
    root->right->right->right->left = newNode(7);

    // Print all nodes having
    // children as their factors
    cout << getCount(root) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Counting nodes
// whose immediate children
// are its factors
 import java.util.*;

class GFG{

// A Tree node
static class Node {
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

// Function to check and print if
// immediate children of a node
// are its factors or not
static boolean areChilrenFactors(
    Node parent,
    Node a,
    Node b)
{
    if (parent.key % a.key == 0
        && parent.key % b.key == 0)
        return true;
    else
        return false;
}

// Function to get the
// count of full Nodes in
// a binary tree
static int getCount(Node node)
{
    // If tree is empty
    if (node==null)
        return 0;
    Queue<Node> q = new LinkedList<Node>();

    // Do level order traversal
    // starting from root
    int count = 0;

    // Store the number of nodes
    // with both children as factors
    q.add(node);
    while (!q.isEmpty()) {
        Node temp = q.peek();
        q.remove();

        if (temp.left!=null && temp.right!=null) {
            if (areChilrenFactors(
                    temp, temp.left,
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

// Function to find total no of nodes
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

// Driver Code
public static void main(String[] args)
{
    /*        10
            / \
           40 36
              / \
             18  12
             / \ / \
            2  6 3 4
                  /
                 7
    */

    // Create Binary Tree as shown
    Node root = newNode(10);

    root.left = newNode(40);
    root.right = newNode(36);

    root.right.left = newNode(18);
    root.right.right = newNode(12);

    root.right.left.left = newNode(2);
    root.right.left.right = newNode(6);
    root.right.right.left = newNode(3);
    root.right.right.right = newNode(4);
    root.right.right.right.left = newNode(7);

    // Print all nodes having
    // children as their factors
    System.out.print(getCount(root) +"\n");

}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for counting nodes
# whose immediate children
# are its factors
from collections import deque as queue

# A Binary Tree Node
class Node:

    def __init__(self, key):

        self.data = key
        self.left = None
        self.right = None

# Function to check and print if
# immediate children of a node
# are its factors or not
def areChildrenFactors(parent, a, b):

    if (parent.data % a.data == 0 and
        parent.data % b.data == 0):
        return True
    else:
        return False

# Function to get the
# count of full Nodes in
# a binary tree
def getCount(node):

    # Base Case
    if (not node):
        return 0

    q = queue()

    # Do level order traversal
    # starting from root
    count = 0

    # Store the number of nodes
    # with both children as factors
    q.append(node)

    while (len(q) > 0):
        temp = q.popleft()
        #q.pop()

        if (temp.left and temp.right):
            if (areChildrenFactors(temp, temp.left,
                                         temp.right)):
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

# Driver Code
if __name__ == '__main__':

    # /*        10
    #          / \
    #         40  36
    #            /  \
    #           18   12
    #           / \  / \
    #          2   6 3  4
    #                  /
    #                 7
    #  */

    # Create Binary Tree
    root = Node(10)
    root.left = Node(40)
    root.right = Node(36)

    root.right.left = Node(18)
    root.right.right = Node(12)

    root.right.left.left = Node(2)
    root.right.left.right = Node(6)
    root.right.right.left = Node(3)
    root.right.right.right = Node(4)
    root.right.right.right.left = Node(7)

    # Print all nodes having
    # children as their factors
    print(getCount(root))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for Counting nodes
// whose immediate children
// are its factors
using System;
using System.Collections.Generic;

class GFG{

// A Tree node
class Node {
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

// Function to check and print if
// immediate children of a node
// are its factors or not
static bool areChilrenFactors(
    Node parent,
    Node a,
    Node b)
{
    if (parent.key % a.key == 0
        && parent.key % b.key == 0)
        return true;
    else
        return false;
}

// Function to get the
// count of full Nodes in
// a binary tree
static int getCount(Node node)
{
    // If tree is empty
    if (node == null)
        return 0;
    List<Node> q = new List<Node>();

    // Do level order traversal
    // starting from root
    int count = 0;

    // Store the number of nodes
    // with both children as factors
    q.Add(node);
    while (q.Count != 0) {
        Node temp = q[0];
        q.RemoveAt(0);

        if (temp.left!=null && temp.right != null) {
            if (areChilrenFactors(
                    temp, temp.left,
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

// Function to find total no of nodes
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

// Driver Code
public static void Main(String[] args)
{
    /*        10
            / \
           40 36
              / \
             18  12
             / \ / \
            2  6 3 4
                  /
                 7
    */

    // Create Binary Tree as shown
    Node root = newNode(10);

    root.left = newNode(40);
    root.right = newNode(36);

    root.right.left = newNode(18);
    root.right.right = newNode(12);

    root.right.left.left = newNode(2);
    root.right.left.right = newNode(6);
    root.right.right.left = newNode(3);
    root.right.right.right = newNode(4);
    root.right.right.right.left = newNode(7);

    // Print all nodes having
    // children as their factors
    Console.Write(getCount(root) +"\n");

}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program for Counting nodes
// whose immediate children are its factors

// A Tree node
class Node
{

    // Utility function to create a new node
    constructor(key)
    {
        this.key = key;
        this.left = this.right = null;
    }
}

// Function to check and print if
// immediate children of a node
// are its factors or not
function areChilrenFactors(parent, a, b)
{
    if (parent.key % a.key == 0 &&
        parent.key % b.key == 0)
        return true;
    else
        return false;
}

// Function to get the
// count of full Nodes in
// a binary tree
function getCount(node)
{

    // If tree is empty
    if (node == null)
        return 0;

    let q = [];

    // Do level order traversal
    // starting from root
    let count = 0;

    // Store the number of nodes
    // with both children as factors
    q.push(node);

    while (q.length != 0)
    {
        let temp = q.shift();

        if (temp.left != null &&
            temp.right != null)
        {
            if (areChilrenFactors(
                    temp, temp.left,
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

// Function to find total no of nodes
// In a given binary tree
function findSize(node)
{

    // Base condition
    if (node == null)
        return 0;

    return 1 + findSize(node.left) +
               findSize(node.right);
}

// Driver Code

/*          10
            / \
           40 36
              / \
             18  12
             / \ / \
            2  6 3 4
                  /
                 7
    */

// Create Binary Tree as shown
let root = new Node(10);

root.left = new Node(40);
root.right = new Node(36);

root.right.left = new Node(18);
root.right.right = new Node(12);

root.right.left.left = new Node(2);
root.right.left.right = new Node(6);
root.right.right.left = new Node(3);
root.right.right.right = new Node(4);
root.right.right.right.left = new Node(7);

// Print all nodes having
// children as their factors
document.write(getCount(root) + "<br>");

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
3
```