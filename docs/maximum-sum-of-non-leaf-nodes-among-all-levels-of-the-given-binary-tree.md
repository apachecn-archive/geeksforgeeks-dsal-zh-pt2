# 给定二叉树所有层次中非叶节点的最大和

> 原文:[https://www . geeksforgeeks . org/给定二叉树各级非叶节点最大和/](https://www.geeksforgeeks.org/maximum-sum-of-non-leaf-nodes-among-all-levels-of-the-given-binary-tree/)

给定一棵具有正和负节点的二叉树，任务是在给定二叉树的所有级别中找到非叶节点的最大和。

**示例:**

```
Input:
                        4
                      /   \
                     2    -5
                    / \   
                  -1   3 
Output: 4
Sum of all non-leaf nodes at 0th level is 4.
Sum of all non-leaf nodes at 1st level is 2.
Sum of all non-leaf nodes at 2nd level is 0.
Hence maximum sum is 4

Input:
                 1
               /   \
             2      3
           /  \      \
          4    5      8
                    /   \
                   6     7  
Output: 8
```

**方法:**解决上述问题的思路是做树的[级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。遍历时，分别处理不同级别的节点。对于正在处理的每个级别，计算该级别中非叶节点的总和，并跟踪最大总和。

下面是上述方法的实现:

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

// Function to return the maximum sum of non-leaf nodes
// at any level in tree using level order traversal
int maxNonLeafNodesSum(struct Node* root)
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

            // Dequeue a node from queue
            Node* temp = q.front();
            q.pop();

            // Add non-leaf node's value to current sum
            if (temp->left != NULL || temp->right != NULL)
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
    cout << maxNonLeafNodesSum(root) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.LinkedList;
import java.util.Queue;
class GFG{

// A binary tree node has data,
// pointer to left child
// and a pointer to right child
static class Node
{
  int data;
  Node left, right;
  public Node(int data)
  {
    this.data = data;
    this.left = this.right = null;
  }
};

// Function to return the maximum
// sum of non-leaf nodes  at any
// level in tree using level
// order traversal
static int maxNonLeafNodesSum(Node root)
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
    // Get the size of queue
    // when the level order
    // traversal for one
    // level finishes
    int count = q.size();

    // Iterate for all the nodes
    // in the queue currently
    int sum = 0;
    while (count-- > 0)
    {
      // Dequeue a node
      // from queue
      Node temp = q.poll();

      // Add non-leaf node's
      // value to current sum
      if (temp.left != null ||
          temp.right != null)
        sum = sum + temp.data;

      // Enqueue left and right
      // children of dequeued node
      if (temp.left != null)
        q.add(temp.left);
      if (temp.right != null)
        q.add(temp.right);
    }

    // Update the maximum sum
    // of leaf nodes value
    result = max(sum, result);
  }
  return result;
}

static int max(int sum,
               int result)
{
  if (sum > result)
    return sum;
  return result;
}

// Driver code
public static void main(String[] args)
{
  Node root = new Node(1);
  root.left = new Node(2);
  root.right = new Node(3);
  root.left.left = new Node(4);
  root.left.right = new Node(5);
  root.right.right = new Node(8);
  root.right.right.left = new Node(6);
  root.right.right.right = new Node(7);
  System.out.println(maxNonLeafNodesSum(root));
}   
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import queue

# A binary tree node has data, pointer to
# left child and a pointer to right child
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to return the maximum Sum of 
# non-leaf nodes at any level in tree
# using level order traversal
def maxNonLeafNodesSum(root):

    # Base case
    if root == None:
        return 0

    # Initialize result
    result = 0

    # Do Level order traversal keeping track
    # of the number of nodes at every level
    q = queue.Queue()
    q.put(root)
    while not q.empty():

        # Get the size of queue when the level
        # order traversal for one level finishes
        count = q.qsize()

        # Iterate for all the nodes
        # in the queue currently
        Sum = 0
        while count:

            # Dequeue a node from queue
            temp = q.get()

            # Add non-leaf node's value to current Sum
            if temp.left != None or temp.right != None:
                Sum += temp.data

            # Enqueue left and right
            # children of dequeued node
            if temp.left != None:
                q.put(temp.left)
            if temp.right != None:
                q.put(temp.right)

            count -= 1

        # Update the maximum Sum of leaf nodes value
        result = max(Sum, result)

    return result

# Driver code
if __name__ == "__main__":

    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right.right = Node(8)
    root.right.right.left = Node(6)
    root.right.right.right = Node(7)
    print(maxNonLeafNodesSum(root))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections;

class GFG{

// A binary tree node has data,
// pointer to left child
// and a pointer to right child
class Node
{
  public int data;
  public Node left, right;

  public Node(int data)
  {
    this.data = data;
    this.left = this.right = null;
  }
};

// Function to return the maximum
// sum of non-leaf nodes  at any
// level in tree using level
// order traversal
static int maxNonLeafNodesSum(Node root)
{

  // Base case
  if (root == null)
    return 0;

  // Initialize result
  int result = 0;

  // Do Level order traversal keeping track
  // of the number of nodes at every level
  Queue q = new Queue();

  q.Enqueue(root);

  while (q.Count != 0)
  {

    // Get the size of queue
    // when the level order
    // traversal for one
    // level finishes
    int count = q.Count;

    // Iterate for all the nodes
    // in the queue currently
    int sum = 0;

    while (count-- > 0)
    {

      // Dequeue a node
      // from queue
      Node temp = (Node)q.Dequeue();

      // Add non-leaf node's
      // value to current sum
      if (temp.left != null ||
          temp.right != null)
        sum = sum + temp.data;

      // Enqueue left and right
      // children of dequeued node
      if (temp.left != null)
        q.Enqueue(temp.left);
      if (temp.right != null)
        q.Enqueue(temp.right);
    }

    // Update the maximum sum
    // of leaf nodes value
    result = max(sum, result);
  }
  return result;
}

static int max(int sum,
               int result)
{
  if (sum > result)
    return sum;

  return result;
}

// Driver code
public static void Main(string[] args)
{
  Node root = new Node(1);
  root.left = new Node(2);
  root.right = new Node(3);
  root.left.left = new Node(4);
  root.left.right = new Node(5);
  root.right.right = new Node(8);
  root.right.right.left = new Node(6);
  root.right.right.right = new Node(7);
  Console.Write(maxNonLeafNodesSum(root));
}   
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // A binary tree node has data,
    // pointer to left child
    // and a pointer to right child
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Function to return the maximum
    // sum of non-leaf nodes  at any
    // level in tree using level
    // order traversal
    function maxNonLeafNodesSum(root)
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
        // Get the size of queue
        // when the level order
        // traversal for one
        // level finishes
        let count = q.length;

        // Iterate for all the nodes
        // in the queue currently
        let sum = 0;
        while (count-- > 0)
        {
          // Dequeue a node
          // from queue
          let temp = q[0];
          q.shift();

          // Add non-leaf node's
          // value to current sum
          if (temp.left != null ||
              temp.right != null)
            sum = sum + temp.data;

          // Enqueue left and right
          // children of dequeued node
          if (temp.left != null)
            q.push(temp.left);
          if (temp.right != null)
            q.push(temp.right);
        }

        // Update the maximum sum
        // of leaf nodes value
        result = max(sum, result);
      }
      return result;
    }

    function max(sum, result)
    {
      if (sum > result)
        return sum;
      return result;
    }

    let root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right.right = new Node(8);
    root.right.right.left = new Node(6);
    root.right.right.right = new Node(7);
    document.write(maxNonLeafNodesSum(root));

</script>
```

**Output:** 

```
8
```