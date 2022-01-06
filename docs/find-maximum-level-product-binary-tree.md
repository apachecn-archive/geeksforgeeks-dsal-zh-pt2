# 在二叉树中找到最大级别积

> 原文:[https://www . geesforgeks . org/find-最高级-产品-二叉树/](https://www.geeksforgeeks.org/find-maximum-level-product-binary-tree/)

给定一棵有正节点和负节点的二叉树，任务是在其中找到最大乘积水平。
**例:**

```
Input :               4
                    /   \
                   2    -5
                  / \    /\
                -1   3 -2  6
Output: 36
Explanation :
Product of all nodes of 0'th level is 4
Product of all nodes of 1'th level is -10
Product of all nodes of 0'th level is 36
Hence maximum product is 6

Input :          1
               /   \
              2     3
             / \     \
            4   5     8
                     /  \
                    6    7  
Output :  160
Explanation :
Product of all nodes of 0'th level is 1
Product of all nodes of 1'th level is 6
Product of all nodes of 0'th level is 160
Product of all nodes of 0'th level is 42
Hence maximum product is 160
```

**先决条件:** [二叉树的最大宽度](https://www.geeksforgeeks.org/maximum-width-of-a-binary-tree/)

**做法:**思路是做树的级序遍历。遍历时，分别处理不同级别的节点。对于正在处理的每个级别，计算该级别中节点的乘积，并跟踪最大乘积。

## C++

```
// A queue based C++ program to find maximum product
// of a level in Binary Tree
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
struct Node {
    int data;
    struct Node *left, *right;
};

// Function to find the maximum product of a level in tree
// using level order traversal
int maxLevelProduct(struct Node* root)
{
    // Base case
    if (root == NULL)
        return 0;

    // Initialize result
    int result = root->data;

    // Do Level order traversal keeping track of number
    // of nodes at every level.
    queue<Node*> q;
    q.push(root);
    while (!q.empty()) {

        // Get the size of queue when the level order
        // traversal for one level finishes
        int count = q.size();

        // Iterate for all the nodes in the queue currently
        int product = 1;
        while (count--) {

            // Dequeue an node from queue
            Node* temp = q.front();
            q.pop();

            // Multiply this node's value to current product.
            product = product * temp->data;

            // Enqueue left and right children of
            // dequeued node
            if (temp->left != NULL)
                q.push(temp->left);
            if (temp->right != NULL)
                q.push(temp->right);
        }

        // Update the maximum node count value
        result = max(product, result);
    }

    return result;
}

/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
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

    /* Constructed Binary tree is:
             1
            / \
           2   3
          / \   \
         4   5   8
                / \
               6   7 */
    cout << "Maximum level product is "
         << maxLevelProduct(root) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A queue based Java program to find
// maximum product of a level in Binary Tree
import java.util.*;

class GFG
{

/* A binary tree node has data,
pointer to left child and a
pointer to right child */
static class Node
{
    int data;
    Node left, right;
};

// Function to find the maximum product
// of a level in tree using
// level order traversal
static int maxLevelProduct(Node root)
{
    // Base case
    if (root == null)
        return 0;

    // Initialize result
    int result = root.data;

    // Do Level order traversal keeping track
    // of number of nodes at every level.
    Queue<Node> q = new LinkedList<>();
    q.add(root);
    while (q.size() > 0)
    {

        // Get the size of queue when the level order
        // traversal for one level finishes
        int count = q.size();

        // Iterate for all the nodes
        // in the queue currently
        int product = 1;
        while (count-->0)
        {

            // Dequeue an node from queue
            Node temp = q.peek();
            q.remove();

            // Multiply this node's value
            // to current product.
            product = product* temp.data;

            // Enqueue left and right children of
            // dequeued node
            if (temp.left != null)
                q.add(temp.left);
            if (temp.right != null)
                q.add(temp.right);
        }

        // Update the maximum node count value
        result = Math.max(product, result);
    }
    return result;
}

/* Helper function that allocates
a new node with the given data and
null left and right pointers. */
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Driver code
public static void main(String args[])
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.right = newNode(8);
    root.right.right.left = newNode(6);
    root.right.right.right = newNode(7);

    /* Constructed Binary tree is:
            1
            / \
        2 3
        / \ \
        4 5 8
                / \
            6 7 */
    System.out.print("Maximum level product is " +
                          maxLevelProduct(root) );
}
}

// This code is contributed by Arnub Kundu
```

## 蟒蛇 3

```
# Python3 program to find maximum product
# of a level in Binary Tree

# Helper function that allocates a new
# node with the given data and None left
# and right poers.                                    
class newNode:

    # Construct to create a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Function to find the maximum product
# of a level in tree using level order
# traversal
def maxLevelProduct(root):

    # Base case
    if (root == None):
        return 0

    # Initialize result
    result = root.data

    # Do Level order traversal keeping track
    # of number of nodes at every level.
    q = []
    q.append(root)
    while (len(q)):

        # Get the size of queue when the level
        # order traversal for one level finishes
        count = len(q)

        # Iterate for all the nodes in
        # the queue currently
        product = 1
        while (count):
            count -= 1

            # Dequeue an node from queue
            temp = q[0]
            q.pop(0)

            # Multiply this node's value to
            # current product.
            product = product * temp.data

            # Enqueue left and right children
            # of dequeued node
            if (temp.left != None):
                q.append(temp.left)
            if (temp.right != None):
                q.append(temp.right)

        # Update the maximum node count value
        result = max(product, result)

    return result

# Driver Code
if __name__ == '__main__':

    """
    Let us create Binary Tree
    shown in above example """
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.right.right = newNode(8)
    root.right.right.left = newNode(6)
    root.right.right.right = newNode(7)

    """ Constructed Binary tree is:
            1
            / \
        2 3
        / \ \
        4 5 8
                / \
            6 7 """

    print("Maximum level product is",
               maxLevelProduct(root))

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// A queue based C# program to find
// maximum product of a level in Binary Tree
using System;
using System.Collections.Generic;

class GFG
{

    /* A binary tree node has data,
    pointer to left child and a
    pointer to right child */
    class Node
    {
        public int data;
        public Node left, right;
    };

    // Function to find the maximum product
    // of a level in tree using
    // level order traversal
    static int maxLevelProduct(Node root)
    {
        // Base case
        if (root == null)
        {
            return 0;
        }

        // Initialize result
        int result = root.data;

        // Do Level order traversal keeping track
        // of number of nodes at every level.
        Queue<Node> q = new Queue<Node>();
        q.Enqueue(root);
        while (q.Count > 0)
        {

            // Get the size of queue when the level order
            // traversal for one level finishes
            int count = q.Count;

            // Iterate for all the nodes
            // in the queue currently
            int product = 1;
            while (count-- > 0)
            {

                // Dequeue an node from queue
                Node temp = q.Peek();
                q.Dequeue();

                // Multiply this node's value
                // to current product.
                product = product * temp.data;

                // Enqueue left and right children of
                // dequeued node
                if (temp.left != null)
                {
                    q.Enqueue(temp.left);
                }
                if (temp.right != null)
                {
                    q.Enqueue(temp.right);
                }
            }

            // Update the maximum node count value
            result = Math.Max(product, result);
        }
        return result;
    }

    /* Helper function that allocates
    a new node with the given data and
    null left and right pointers. */
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

        /* Constructed Binary tree is:
            1
            / \
        2 3
        / \ \
        4 5 8
                / \
            6 7 */
        Console.Write("Maximum level product is " +
                            maxLevelProduct(root));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// A queue based Javascript program to find
// maximum product of a level in Binary Tree
/* A binary tree node has data,
pointer to left child and a
pointer to right child */
class Node
{
    constructor()
    {
        this.left = null;
        this.right = null;
        this.data = 0;
    }
};

// Function to find the maximum product
// of a level in tree using
// level order traversal
function maxLevelProduct(root)
{
    // Base case
    if (root == null)
    {
        return 0;
    }
    // Initialize result
    var result = root.data;
    // Do Level order traversal keeping track
    // of number of nodes at every level.
    var q = [];
    q.push(root);
    while (q.length > 0)
    {
        // Get the size of queue when the level order
        // traversal for one level finishes
        var count = q.length;
        // Iterate for all the nodes
        // in the queue currently
        var product = 1;
        while (count-- > 0)
        {
            // Dequeue an node from queue
            var temp = q[0];
            q.shift();
            // Multiply this node's value
            // to current product.
            product = product * temp.data;
            // push left and right children of
            // dequeued node
            if (temp.left != null)
            {
                q.push(temp.left);
            }
            if (temp.right != null)
            {
                q.push(temp.right);
            }
        }
        // Update the maximum node count value
        result = Math.max(product, result);
    }
    return result;
}
/* Helper function that allocates
a new node with the given data and
null left and right pointers. */
function newNode(data)
{
    var node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Driver code
var root = newNode(1);
root.left = newNode(2);
root.right = newNode(3);
root.left.left = newNode(4);
root.left.right = newNode(5);
root.right.right = newNode(8);
root.right.right.left = newNode(6);
root.right.right.right = newNode(7);
/* Constructed Binary tree is:
    1
    / \
2 3
/ \ \
4 5 8
        / \
    6 7 */
document.write("Maximum level product is " +
                    maxLevelProduct(root));

// This code is contributed by famously.
</script>
```

**输出:**

```
Maximum level product is 160
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)