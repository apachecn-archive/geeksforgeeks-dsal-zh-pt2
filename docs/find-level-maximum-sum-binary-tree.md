# 求二叉树中最大级别和

> 原文:[https://www . geesforgeks . org/find-level-max-sum-二叉树/](https://www.geeksforgeeks.org/find-level-maximum-sum-binary-tree/)

给定一棵有正负节点的二叉树，任务是找出其中的最大和水平。

**示例:**

```
Input :               4
                    /   \
                   2    -5
                  / \    /\
                -1   3 -2  6
Output: 6
Explanation :
Sum of all nodes of 0'th level is 4
Sum of all nodes of 1'th level is -3
Sum of all nodes of 0'th level is 6
Hence maximum sum is 6

Input :          1
               /   \
             2      3
           /  \      \
          4    5      8
                    /   \
                   6     7  
Output :  17
```

这个问题是[最大宽度问题](https://www.geeksforgeeks.org/maximum-width-of-a-binary-tree/)的变种。这个想法是对树进行一次级别顺序遍历。遍历时，分别处理不同级别的节点。对于正在处理的每个级别，计算该级别中节点的总和，并跟踪最大总和。

下面是上述想法的实现:

## C++

```
// A queue based C++ program to find maximum sum
// of a level in Binary Tree
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct Node
{
    int data;
    struct Node *left, *right;
};

// Function to find the maximum sum of a level in tree
// using level order traversal
int maxLevelSum(struct Node* root)
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
    while (!q.empty())
    {
        // Get the size of queue when the level order
        // traversal for one level finishes
        int count = q.size();

        // Iterate for all the nodes in the queue currently
        int sum = 0;
        while (count--)
        {
            // Dequeue an node from queue
            Node* temp = q.front();
            q.pop();

            // Add this node's value to current sum.
            sum = sum + temp->data;

            // Enqueue left and right children of
            // dequeued node
            if (temp->left != NULL)
                q.push(temp->left);
            if (temp->right != NULL)
                q.push(temp->right);
        }

        // Update the maximum node count value
        result = max(sum, result);
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

    /*   Constructed Binary tree is:
                 1
               /   \
             2      3
           /  \      \
          4    5      8
                    /   \
                   6     7    */
    cout << "Maximum level sum is " << maxLevelSum(root)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A queue based Java program to find maximum
// sum of a level in Binary Tree
import java.util.LinkedList;
import java.util.Queue;

class GFG{

// A binary tree node has data, pointer
// to left child and a pointer to right
// child
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

// Function to find the maximum
// sum of a level in tree
// using level order traversal
static int maxLevelSum(Node root)
{

    // Base case
    if (root == null)
        return 0;

    // Initialize result
    int result = root.data;

    // Do Level order traversal keeping
    // track of number of nodes at every
    // level.
    Queue<Node> q = new LinkedList<>();
    q.add(root);
    while (!q.isEmpty())
    {

        // Get the size of queue when the
        // level order traversal for one
        // level finishes
        int count = q.size();

        // Iterate for all the nodes
        // in the queue currently
        int sum = 0;
        while (count-- > 0)
        {

            // Dequeue an node from queue
            Node temp = q.poll();

            // Add this node's value
            // to current sum.
            sum = sum + temp.data;

            // Enqueue left and right children
            // of dequeued node
            if (temp.left != null)
                q.add(temp.left);
            if (temp.right != null)
                q.add(temp.right);
        }

        // Update the maximum node
        // count value
        result = Math.max(sum, result);
    }
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

    /*   Constructed Binary tree is:
                 1
               /   \
             2      3
           /  \      \
          4    5      8
                    /   \
                   6     7    */
    System.out.println("Maximum level sum is " +
                        maxLevelSum(root));
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# A queue based Python3 program to find
# maximum sum of a level in Binary Tree
from collections import deque

# A binary tree node has data, pointer
# to left child and a pointer to right
# child
class Node:

    def __init__(self, key):

        self.data = key
        self.left = None
        self.right = None

# Function to find the maximum sum
# of a level in tree
# using level order traversal
def maxLevelSum(root):

    # Base case
    if (root == None):
        return 0

    # Initialize result
    result = root.data

    # Do Level order traversal keeping
    # track of number
    # of nodes at every level.
    q = deque()
    q.append(root)

    while (len(q) > 0):

        # Get the size of queue when the
        # level order traversal for one
        # level finishes
        count = len(q)

        # Iterate for all the nodes in
        # the queue currently
        sum = 0
        while (count > 0):

            # Dequeue an node from queue
            temp = q.popleft()

            # Add this node's value to current sum.
            sum = sum + temp.data

            # Enqueue left and right children of
            # dequeued node
            if (temp.left != None):
                q.append(temp.left)
            if (temp.right != None):
                q.append(temp.right)

            count -= 1   

        # Update the maximum node count value
        result = max(sum, result)

    return result

# Driver code
if __name__ == '__main__':

    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right.right = Node(8)
    root.right.right.left = Node(6)
    root.right.right.right = Node(7)

    # Constructed Binary tree is:
    #              1
    #            /   \
    #          2      3
    #        /  \      \
    #       4    5      8
    #                 /   \
    #                6     7   
    print("Maximum level sum is", maxLevelSum(root))

# This code is contributed by mohit kumar 29
```

## C#

```
// A queue based C# program to find maximum
// sum of a level in Binary Tree
using System;
using System.Collections.Generic;
class GFG
{

  // A binary tree node has data, pointer
  // to left child and a pointer to right
  // child
  public
    class Node
    {
      public
        int data;
      public
        Node left, right;

      public Node(int data)
      {
        this.data = data;
        this.left = this.right = null;
      }
    };

  // Function to find the maximum
  // sum of a level in tree
  // using level order traversal
  static int maxLevelSum(Node root)
  {

    // Base case
    if (root == null)
      return 0;

    // Initialize result
    int result = root.data;

    // Do Level order traversal keeping
    // track of number of nodes at every
    // level.
    Queue<Node> q = new Queue<Node>();
    q.Enqueue(root);
    while (q.Count != 0)
    {

      // Get the size of queue when the
      // level order traversal for one
      // level finishes
      int count = q.Count;

      // Iterate for all the nodes
      // in the queue currently
      int sum = 0;
      while (count --> 0)
      {

        // Dequeue an node from queue
        Node temp = q.Dequeue();

        // Add this node's value
        // to current sum.
        sum = sum + temp.data;

        // Enqueue left and right children
        // of dequeued node
        if (temp.left != null)
          q.Enqueue(temp.left);
        if (temp.right != null)
          q.Enqueue(temp.right);
      }

      // Update the maximum node
      // count value
      result = Math.Max(sum, result);
    }
    return result;
  }

  // Driver code
  public static void Main(String[] args)
  {
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right.right = new Node(8);
    root.right.right.left = new Node(6);
    root.right.right.right = new Node(7);

    /*   Constructed Binary tree is:
                 1
               /   \
             2      3
           /  \      \
          4    5      8
                    /   \
                   6     7    */
    Console.WriteLine("Maximum level sum is " +
                      maxLevelSum(root));
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// A queue based Javascript program to find maximum
// sum of a level in Binary Tree

    // A binary tree node has data, pointer
// to left child and a pointer to right
// child
    class Node
    {
        constructor(data)
        {
            this.data = data;
            this.left = this.right = null;
        }
    }

// Function to find the maximum
// sum of a level in tree
// using level order traversal   
function maxLevelSum(root)
{
    // Base case
    if (root == null)
        return 0;

    // Initialize result
    let result = root.data;

    // Do Level order traversal keeping
    // track of number of nodes at every
    // level.
    let q = [];
    q.push(root);
    while (q.length!=0)
    {

        // Get the size of queue when the
        // level order traversal for one
        // level finishes
        let count = q.length;

        // Iterate for all the nodes
        // in the queue currently
        let sum = 0;
        while (count-- > 0)
        {

            // Dequeue an node from queue
            let temp = q.shift();

            // Add this node's value
            // to current sum.
            sum = sum + temp.data;

            // Enqueue left and right children
            // of dequeued node
            if (temp.left != null)
                q.push(temp.left);
            if (temp.right != null)
                q.push(temp.right);
        }

        // Update the maximum node
        // count value
        result = Math.max(sum, result);
    }
    return result;
}

// Driver code
let root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
root.right.right = new Node(8);
root.right.right.left = new Node(6);
root.right.right.right = new Node(7);

 /*   Constructed Binary tree is:
                 1
               /   \
             2      3
           /  \      \
          4    5      8
                    /   \
                   6     7    */

document.write("Maximum level sum is " +
                        maxLevelSum(root));

    // This code is contributed by unknown2108
</script>
```

**Output**

```
Maximum level sum is 17
```

**<u>复杂度分析:</u>**

**时间复杂度** : O(N)，其中 N 为树中节点总数。
在水平顺序遍历中，树的每个节点都被处理一次，因此如果树中总共有 N 个节点，由于水平顺序遍历而导致的复杂性是 O(N)。此外，在处理每个节点时，我们会在每个级别保持总和，但是，这不会影响整体时间复杂性。因此，时间复杂度为 O(N)。

**辅助空间:** O(w)，其中 w 为树的最大宽度。
在水平顺序遍历中，保持一个队列，它在任何时刻的最大大小都可以达到二叉树的最大宽度。

本文由 [**沙莎克·米什拉(古卢)**](https://www.facebook.com/shashank.mishra.92167) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。