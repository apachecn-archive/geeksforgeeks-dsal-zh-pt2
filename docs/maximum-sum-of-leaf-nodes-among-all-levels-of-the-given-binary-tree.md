# 给定二叉树所有层次中叶节点的最大和

> 原文:[https://www . geeksforgeeks . org/给定二叉树各级叶节点最大和/](https://www.geeksforgeeks.org/maximum-sum-of-leaf-nodes-among-all-levels-of-the-given-binary-tree/)

给定一棵具有正和负节点的二叉树，任务是在给定二叉树的所有级别中找到叶节点的最大和。
**例:**

```
Input:
                        4
                      /   \
                     2    -5
                    / \   
                  -1   3 
Output: 2
Sum of all leaves at 0th level is 0.
Sum of all leaves at 1st level is -5.
Sum of all leaves at 2nd level is 2.
Hence maximum sum is 2.

Input:
                 1
               /   \
             2      3
           /  \      \
          4    5      8
                    /   \
                   6     7  
Output: 13
```

**方法:**解决上述问题的思路是做[级树的顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。遍历时，分别处理不同级别的节点。对于正在处理的每个级别，计算该级别中叶节点的总和，并跟踪最大总和。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// A binary tree node has data, pointer to left child
// and a pointer to right child
struct Node {
    int data;
    struct Node *left, *right;
};

// Function to return the maximum sum of leaf nodes
// at any level in tree using level order traversal
int maxLeafNodesSum(struct Node* root)
{

    // Base case
    if (root == NULL)
        return 0;

    // Initialize result
    int result = 0;

    // Do Level order traversal keeping track
    // of the number of nodes at every level
    queue<Node*> q;
    q.push(root);
    while (!q.empty()) {

        // Get the size of queue when the level order
        // traversal for one level finishes
        int count = q.size();

        // Iterate for all the nodes in the queue currently
        int sum = 0;
        while (count--) {

            // Dequeue an node from queue
            Node* temp = q.front();
            q.pop();

            // Add leaf node's value to current sum
            if (temp->left == NULL && temp->right == NULL)

                sum = sum + temp->data;

            // Enqueue left and right children of
            // dequeued node
            if (temp->left != NULL)
                q.push(temp->left);
            if (temp->right != NULL)
                q.push(temp->right);
        }

        // Update the maximum sum of leaf nodes value
        result = max(sum, result);
    }

    return result;
}

// Helper function that allocates a new node with the
// given data and NULL left and right pointers
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Driver code
int main()
{
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->right = newNode(8);
    root->right->right->left = newNode(6);
    root->right->right->right = newNode(7);
    cout << maxLeafNodesSum(root) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

// A binary tree node has data,
// pointer to left child and
// a pointer to right child
static class Node
{
    int data;
    Node left, right;
};

// Function to return the maximum sum
// of leaf nodes at any level in tree
// using level order traversal
static int maxLeafNodesSum(Node root)
{

    // Base case
    if (root == null)
        return 0;

    // Initialize result
    int result = 0;

    // Do Level order traversal keeping track
    // of the number of nodes at every level
    Queue<Node> q = new LinkedList<>();
    q.add(root);
    while (!q.isEmpty())
    {

        // Get the size of queue when the level order
        // traversal for one level finishes
        int count = q.size();

        // Iterate for all the nodes
        // in the queue currently
        int sum = 0;
        while (count-- > 0)
        {

            // Dequeue an node from queue
            Node temp = q.peek();
            q.remove();

            // Add leaf node's value to current sum
            if (temp.left == null &&
                temp.right == null)

                sum = sum + temp.data;

            // Enqueue left and right children of
            // dequeued node
            if (temp.left != null)
                q.add(temp.left);
            if (temp.right != null)
                q.add(temp.right);
        }

        // Update the maximum sum of leaf nodes value
        result = Math.max(sum, result);
    }

    return result;
}

// Helper function that allocates a new node with the
// given data and null left and right pointers
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Driver code
public static void main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.right = newNode(8);
    root.right.right.left = newNode(6);
    root.right.right.right = newNode(7);
    System.out.println(maxLeafNodesSum(root));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# A binary tree node has data,
# pointer to left child and
# a pointer to right child
# Helper function that allocates
# a new node with the given data
# and None left and right pointers
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to return the maximum sum
# of leaf nodes at any level in tree
# using level order traversal
def maxLeafNodesSum(root):

    # Base case
    if (root == None):
        return 0

    # Initialize result
    result = 0

    # Do Level order traversal keeping track
    # of the number of nodes at every level
    q = []
    q.append(root)
    while(len(q)):

        # Get the size of queue when the level order
        # traversal for one level finishes
        count = len(q)

        # Iterate for all the nodes
        # in the queue currently
        sum = 0
        while (count):

            # Dequeue an node from queue
            temp = q[0]
            q.pop(0)

            # Add leaf node's value to current sum
            if (temp.left == None and
                temp.right == None):
                sum = sum + temp.data

            # Enqueue left and right children of
            # dequeued node
            if (temp.left != None):
                q.append(temp.left)
            if (temp.right != None):
                q.append(temp.right)
            count -= 1

        # Update the maximum sum
        # of leaf nodes value
        result = max(sum, result)

    return result

# Driver code
root = newNode(1)
root.left = newNode(2)
root.right = newNode(3)
root.left.left = newNode(4)
root.left.right = newNode(5)
root.right.right = newNode(8)
root.right.right.left = newNode(6)
root.right.right.right = newNode(7)
print(maxLeafNodesSum(root))

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// A binary tree node has data,
// pointer to left child and
// a pointer to right child
class Node
{
    public int data;
    public Node left, right;
};

// Function to return the maximum sum
// of leaf nodes at any level in tree
// using level order traversal
static int maxLeafNodesSum(Node root)
{

    // Base case
    if (root == null)
        return 0;

    // Initialize result
    int result = 0;

    // Do Level order traversal keeping track
    // of the number of nodes at every level
    Queue<Node> q = new Queue<Node>();
    q.Enqueue(root);
    while (q.Count != 0)
    {

        // Get the size of queue when the level order
        // traversal for one level finishes
        int count = q.Count;

        // Iterate for all the nodes
        // in the queue currently
        int sum = 0;
        while (count-- > 0)
        {

            // Dequeue an node from queue
            Node temp = q.Peek();
            q.Dequeue();

            // Add leaf node's value to current sum
            if (temp.left == null &&
                temp.right == null)

                sum = sum + temp.data;

            // Enqueue left and right children of
            // dequeued node
            if (temp.left != null)
                q.Enqueue(temp.left);
            if (temp.right != null)
                q.Enqueue(temp.right);
        }

        // Update the maximum sum of leaf nodes value
        result = Math.Max(sum, result);
    }

    return result;
}

// Helper function that allocates a new node with the
// given data and null left and right pointers
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Driver code
public static void Main(String[] args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.right = newNode(8);
    root.right.right.left = newNode(6);
    root.right.right.right = newNode(7);
    Console.WriteLine(maxLeafNodesSum(root));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // A binary tree node has data,
    // pointer to left child and
    // a pointer to right child
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Function to return the maximum sum
    // of leaf nodes at any level in tree
    // using level order traversal
    function maxLeafNodesSum(root)
    {

        // Base case
        if (root == null)
            return 0;

        // Initialize result
        let result = 0;

        // Do Level order traversal keeping track
        // of the number of nodes at every level
        let q = [];
        q.push(root);
        while (q.length > 0)
        {

            // Get the size of queue when the level order
            // traversal for one level finishes
            let count = q.length;

            // Iterate for all the nodes
            // in the queue currently
            let sum = 0;
            while (count-- > 0)
            {

                // Dequeue an node from queue
                let temp = q[0];
                q.shift();

                // Add leaf node's value to current sum
                if (temp.left == null &&
                    temp.right == null)

                    sum = sum + temp.data;

                // Enqueue left and right children of
                // dequeued node
                if (temp.left != null)
                    q.push(temp.left);
                if (temp.right != null)
                    q.push(temp.right);
            }

            // Update the maximum sum of leaf nodes value
            result = Math.max(sum, result);
        }

        return result;
    }

    // Helper function that allocates a new node with the
    // given data and null left and right pointers
    function newNode(data)
    {
        let node = new Node(data);
        return (node);
    }

    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.right = newNode(8);
    root.right.right.left = newNode(6);
    root.right.right.right = newNode(7);
    document.write(maxLeafNodesSum(root));

</script>
```

**Output:** 

```
13
```