# 使用级别顺序遍历的二叉树密度

> 原文:[https://www . geeksforgeeks . org/二叉树密度-使用级别-顺序-遍历/](https://www.geeksforgeeks.org/density-of-binary-tree-using-level-order-traversal/)

给定一棵二叉树，通过遍历它找到它的密度。
二叉树的密度定义为:

```
Density of Binary Tree = Size / Height 
```

**示例**:

```
Input : 
 Root of following tree
   10
  /   \
 20   30

Output :  1.5
Height of given tree = 2
Size of given tree = 3

Input :
Root of the following tree
     10
    /   
   20   
 /
30
Output : 1
Height of given tree = 3
Size of given tree = 3 
```

使用[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)可以在单次遍历中找到树的大小和高度。
计算二叉树高度的想法是使用一个“空”指针作为两个级别之间的分隔符。每当遍历过程中出现“空”时，高度就会增加。
为了计算二叉树的大小，在级别顺序遍历过程中遇到的每个新节点都要增加计数器。
最后，用上面的公式计算二叉树的密度。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// A binary tree node
struct Node {
    int data;
    Node *left, *right;
};

// Helper function to allocates a new node
Node* newNode(int data)
{
    Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

// Function to calculate density of Binary Tree
float density(Node* root)
{
    queue<Node*> q;

    // push root to queue first
    q.push(root);

    // push NULL as a separator
    q.push(NULL);
    int height = 1, size = 0;
    while (!q.empty()) {
        Node* t = q.front();
        q.pop();
        if (t)
            size++;
        else {

            // If after popping NULL queue is
            // empty then get out of loop i.e
            // stop the level order traversal.
            if (q.empty())
                break;
            q.push(NULL);
            height++;
            continue;
        }

        // if t has left child
        // then push it to queue
        if (t->left) {
            q.push(t->left);
        }

        // if t has right child
        // then push it to queue
        if (t->right) {
            q.push(t->right);
        }
    }
    return (float)size / height;
}

// Driver code
int main()
{
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);

    cout << density(root) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class Solution
{

// A binary tree node
static class Node
{
    int data;
    Node left, right;
}

// Helper function to allocates a new node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return node;
}

// Function to calculate density of Binary Tree
static float density(Node root)
{
    Queue<Node> q = new LinkedList<Node>();

    // add root to queue first
    q.add(root);

    // add null as a separator
    q.add(null);
    int height = 1, size = 0;
    while (q.size() > 0)
    {
        Node t = q.peek();
        q.remove();
        if (t != null)
            size++;
        else
        {

            // If after removeping null queue is
            // empty then get out of loop i.e
            // stop the level order traversal.
            if (q.size() == 0)
                break;
            q.add(null);
            height++;
            continue;
        }

        // if t has left child
        // then add it to queue
        if (t.left !=null)
        {
            q.add(t.left);
        }

        // if t has right child
        // then add it to queue
        if (t.right != null)
        {
            q.add(t.right);
        }
    }
    return ((float)size )/ height;
}

// Driver code
public static void main(String args[])
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);

    System.out.println(density(root));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Linked List node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Helper function to allocates a new node
def newNode( data) :

    node = Node(0)
    node.data = data
    node.left = node.right = None
    return node

# Function to calculate density of Binary Tree
def density(root) :

    q = []

    # append root to queue first
    q.append(root)

    # append None as a separator
    q.append(None)
    height = 1
    size = 0
    while (len(q) > 0):
        t = q[0]
        q.pop(0)
        if (t != None):
            size = size + 1
        else:

            # If after removeping None queue is
            # empty then get out of loop i.e
            # stop the level order traversal.
            if (len(q) == 0):
                break
            q.append(None)
            height = height + 1
            continue

        # if t has left child
        # then append it to queue
        if (t.left != None) :
            q.append(t.left)

        # if t has right child
        # then append it to queue
        if (t.right != None):

            q.append(t.right)

    return (size ) / height

# Driver code

root = newNode(1)
root.left = newNode(2)
root.right = newNode(3)

print(density(root))

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{

// A binary tree node
public class Node
{
    public int data;
    public Node left, right;
}

// Helper function to allocates a new node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return node;
}

// Function to calculate density of Binary Tree
static float density(Node root)
{
    Queue<Node> q = new Queue<Node>();

    // add root to queue first
    q.Enqueue(root);

    // add null as a separator
    q.Enqueue(null);
    int height = 1, size = 0;
    while (q.Count > 0)
    {
        Node t = q.Peek();
        q.Dequeue();
        if (t != null)
            size++;
        else
        {

            // If after removeping null queue is
            // empty then get out of loop i.e
            // stop the level order traversal.
            if (q.Count == 0)
                break;
            q.Enqueue(null);
            height++;
            continue;
        }

        // if t has left child
        // then add it to queue
        if (t.left !=null)
        {
            q.Enqueue(t.left);
        }

        // if t has right child
        // then add it to queue
        if (t.right != null)
        {
            q.Enqueue(t.right);
        }
    }
    return ((float)size ) / height;
}

// Driver code
public static void Main(String []args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);

    Console.WriteLine(density(root));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// A binary tree node
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
}

// Helper function to allocates a new node
function newNode(data)
{
    var node = new Node();
    node.data = data;
    node.left = node.right = null;
    return node;
}

// Function to calculate density of Binary Tree
function density(root)
{
    var q = [];

    // Add root to queue first
    q.push(root);

    // Add null as a separator
    q.push(null);
    var height = 1, size = 0;

    while (q.length > 0)
    {
        var t = q[0];
        q.shift();

        if (t != null)
            size++;
        else
        {

            // If after removeping null queue is
            // empty then get out of loop i.e
            // stop the level order traversal.
            if (q.length == 0)
                break;

            q.push(null);
            height++;
            continue;
        }

        // If t has left child
        // then add it to queue
        if (t.left != null)
        {
            q.push(t.left);
        }

        // If t has right child
        // then add it to queue
        if (t.right != null)
        {
            q.push(t.right);
        }
    }
    return(size) / height;
}

// Driver code
var root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);

document.write(density(root));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
1.5
```

**时间复杂度:** O(N)