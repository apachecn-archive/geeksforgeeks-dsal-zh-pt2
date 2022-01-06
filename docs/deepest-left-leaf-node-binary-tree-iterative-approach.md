# 二叉树中最左边的叶子节点|迭代方法

> 原文:[https://www . geesforgeks . org/最深-左-叶-节点-二叉树-迭代-方法/](https://www.geeksforgeeks.org/deepest-left-leaf-node-binary-tree-iterative-approach/)

给定一棵二叉树，找到最深的叶子节点，它是它的父节点的左子节点。例如，考虑下面的树。最左边的叶子节点是值为 9 的节点。
**例:**

```
Input : 
       1
     /   \
    2     3
  /      /  \  
 4      5    6
        \     \
         7     8
        /       \
       9         10

Output : 9
```

这个问题的递归方法在这里讨论
对于迭代方法，想法类似于[水平顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)
的方法 2，想法是迭代遍历树，每当左边的树节点被推到队列中时，检查它是否是叶节点，如果是叶节点，则更新结果。由于我们一级一级地进行，最后存储的叶节点是最深的一个，

## C++

```
// CPP program to find deepest left leaf
// node of binary tree
#include <bits/stdc++.h>
using namespace std;

// tree node
struct Node {
    int data;
    Node *left, *right;
};

// returns a new tree Node
Node* newNode(int data)
{
    Node* temp = new Node();
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// return the deepest left leaf node
// of binary tree
Node* getDeepestLeftLeafNode(Node* root)
{
    if (!root)
        return NULL;

    // create a queue for level order traversal
    queue<Node*> q;
    q.push(root);

    Node* result = NULL;

    // traverse until the queue is empty
    while (!q.empty()) {
        Node* temp = q.front();
        q.pop();

        // Since we go level by level, the last
        // stored left leaf node is deepest one,
        if (temp->left) {
            q.push(temp->left);
            if (!temp->left->left && !temp->left->right)
                result = temp->left;
        }

        if (temp->right)
            q.push(temp->right);
    }
    return result;
}

// driver program
int main()
{
    // construct a tree
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->right->left = newNode(5);
    root->right->right = newNode(6);
    root->right->left->right = newNode(7);
    root->right->right->right = newNode(8);
    root->right->left->right->left = newNode(9);
    root->right->right->right->right = newNode(10);

    Node* result = getDeepestLeftLeafNode(root);
    if (result)
        cout << "Deepest Left Leaf Node :: "
             << result->data << endl;
    else
        cout << "No result, left leaf not found\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find deepest left leaf
// node of binary tree
import java.util.*;

class GFG
{

// tree node
static class Node
{
    int data;
    Node left, right;
};

// returns a new tree Node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// return the deepest left leaf node
// of binary tree
static Node getDeepestLeftLeafNode(Node root)
{
    if (root == null)
        return null;

    // create a queue for level order traversal
    Queue<Node> q = new LinkedList<>();
    q.add(root);

    Node result = null;

    // traverse until the queue is empty
    while (!q.isEmpty())
    {
        Node temp = q.peek();
        q.remove();

        // Since we go level by level, the last
        // stored left leaf node is deepest one,
        if (temp.left != null)
        {
            q.add(temp.left);
            if (temp.left.left == null &&
                temp.left.right == null)
                result = temp.left;
        }

        if (temp.right != null)
            q.add(temp.right);
    }
    return result;
}

// Driver Code
public static void main(String[] args)
{

    // construct a tree
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.right.left = newNode(5);
    root.right.right = newNode(6);
    root.right.left.right = newNode(7);
    root.right.right.right = newNode(8);
    root.right.left.right.left = newNode(9);
    root.right.right.right.right = newNode(10);

    Node result = getDeepestLeftLeafNode(root);
    if (result != null)
        System.out.println("Deepest Left Leaf Node :: " +
                                            result.data);
    else
        System.out.println("No result, " +
                   "left leaf not found");
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find deepest
# left leaf Binary search Tree

_MIN = -2147483648
_MAX = 2147483648

# Helper function that allocates a new
# node with the given data and None
# left and right poers.                                    
class newnode:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# utility function to return deepest
# left leaf node
def getDeepestLeftLeafNode(root) :

    if (not root):
        return None

    # create a queue for level
    # order traversal
    q = []
    q.append(root)

    result = None

    # traverse until the queue is empty
    while (len(q)):
        temp = q[0]
        q.pop(0)

        if (temp.left):
            q.append(temp.left)
            if (not temp.left.left and
                not temp.left.right):
                result = temp.left

        # Since we go level by level,
        # the last stored right leaf
        # node is deepest one
        if (temp.right):
            q.append(temp.right)        

    return result

# Driver Code
if __name__ == '__main__':

    # create a binary tree
    root = newnode(1)
    root.left = newnode(2)
    root.right = newnode(3)
    root.left.Left = newnode(4)
    root.right.left = newnode(5)
    root.right.right = newnode(6)
    root.right.left.right = newnode(7)
    root.right.right.right = newnode(8)
    root.right.left.right.left = newnode(9)
    root.right.right.right.right = newnode(10)

    result = getDeepestLeftLeafNode(root)
    if result:
        print("Deepest Left Leaf Node ::",
                              result.data)
    else:
        print("No result, Left leaf not found")

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to find deepest left leaf
// node of binary tree
using System;
using System.Collections.Generic;

class GFG
{

// tree node
class Node
{
    public int data;
    public Node left, right;
};

// returns a new tree Node
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// return the deepest left leaf node
// of binary tree
static Node getDeepestLeftLeafNode(Node root)
{
    if (root == null)
        return null;

    // create a queue for level order traversal
    Queue<Node> q = new Queue<Node>();
    q.Enqueue(root);

    Node result = null;

    // traverse until the queue is empty
    while (q.Count != 0)
    {
        Node temp = q.Peek();
        q.Dequeue();

        // Since we go level by level, the last
        // stored left leaf node is deepest one,
        if (temp.left != null)
        {
            q.Enqueue(temp.left);
            if (temp.left.left == null &&
                temp.left.right == null)
                result = temp.left;
        }
        if (temp.right != null)
            q.Enqueue(temp.right);
    }
    return result;
}

// Driver Code
public static void Main(String[] args)
{

    // construct a tree
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.right.left = newNode(5);
    root.right.right = newNode(6);
    root.right.left.right = newNode(7);
    root.right.right.right = newNode(8);
    root.right.left.right.left = newNode(9);
    root.right.right.right.right = newNode(10);

    Node result = getDeepestLeftLeafNode(root);
    if (result != null)
        Console.WriteLine("Deepest Left Leaf Node :: " +
                                           result.data);
    else
        Console.WriteLine("No result, " +
                  "left leaf not found");
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript program to find deepest
    // left leaf node of binary tree

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // returns a new tree Node
    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

    // return the deepest left leaf node
    // of binary tree
    function getDeepestLeftLeafNode(root)
    {
        if (root == null)
            return null;

        // create a queue for level order traversal
        let q = [];
        q.push(root);

        let result = null;

        // traverse until the queue is empty
        while (q.length > 0)
        {
            let temp = q[0];
            q.shift();

            // Since we go level by level, the last
            // stored left leaf node is deepest one,
            if (temp.left != null)
            {
                q.push(temp.left);
                if (temp.left.left == null &&
                    temp.left.right == null)
                    result = temp.left;
            }

            if (temp.right != null)
                q.push(temp.right);
        }
        return result;
    }

    // construct a tree
    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.right.left = newNode(5);
    root.right.right = newNode(6);
    root.right.left.right = newNode(7);
    root.right.right.right = newNode(8);
    root.right.left.right.left = newNode(9);
    root.right.right.right.right = newNode(10);

    let result = getDeepestLeftLeafNode(root);
    if (result != null)
        document.write("Deepest Left Leaf Node :: " +
                                            result.data);
    else
        document.write("No result, " +
                   "left leaf not found");

</script>
```

**输出:**

```
Deepest Left Leaf Node :: 9 
```