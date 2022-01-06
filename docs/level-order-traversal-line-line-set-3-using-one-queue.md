# 逐行逐层顺序遍历|集合 3(使用一个队列)

> 原文:[https://www . geesforgeks . org/level-order-遍历-line-line-set-3-使用一个队列/](https://www.geeksforgeeks.org/level-order-traversal-line-line-set-3-using-one-queue/)

给定一个二叉树，逐级打印节点，每一级在一个新的行上。

![Example](img/c8cf26aa3839f4c631be334e5430e6e2.png)

```
Output:
1
2 3
4 5
```

我们在下面的文章中讨论了两种解决方案。
[逐行打印级别顺序遍历|集合 1](https://www.geeksforgeeks.org/print-level-order-traversal-line-line/)
[逐行打印级别顺序遍历|集合 2(使用两个队列)](https://www.geeksforgeeks.org/level-order-traversal-line-line-set-2-using-two-queues/)
本文讨论使用一个队列的不同方法。首先将根元素和一个空元素插入队列。这个空元素充当分隔符。接下来，从队列的顶部弹出，并将其左右节点添加到队列的末尾，然后在队列的顶部打印。继续此过程，直到队列变空。

## C++

```
/* C++ program to print levels 
line by line */
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct node
{
    struct node *left;
    int data;
    struct node *right;
};

// Function to do level order
// traversal line by line
void levelOrder(node *root)
{
    if (root == NULL) return;

    // Create an empty queue for
    // level order traversal
    queue<node *> q;

    // to store front element of 
    // queue.
    node *curr;

    // Enqueue Root and NULL node.
    q.push(root);
    q.push(NULL);

    while (q.size() > 1)
    {
        curr = q.front();
        q.pop();

        // condition to check 
        // occurrence of next 
        // level.
        if (curr == NULL)
        {
           q.push(NULL);
           cout << "\n";
        }

        else {

            // pushing left child of 
            // current node.
            if(curr->left)
            q.push(curr->left);

            // pushing right child of
            // current node.
            if(curr->right)
            q.push(curr->right);

            cout << curr->data << " ";
        }
    }
}

// Utility function to create a
// new tree node
node* newNode(int data)
{
    node *temp = new node;
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

// Driver program to test above
// functions
int main()
{

    // Let us create binary tree
    // shown above
    node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->right = newNode(6);

    levelOrder(root);
    return 0;
}

// This code is contributed by
// Nikhil Jindal.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to do level order
// traversal line by line
import java.util.LinkedList;
import java.util.Queue;

public class GFG {
  static class Node {
    int data;
    Node left;
    Node right;

    Node(int data) {
      this.data = data;
      left = null;
      right = null;
    }
  }

  // Prints level order traversal line
  // by line using two queues.
  static void levelOrder(Node root) {
    if (root == null)
      return;

    Queue<Node> q = new LinkedList<>();

    // Pushing root node into the queue.
    q.add(root);

    // Pushing delimiter into the queue.
    q.add(null);

    // Executing loop till queue becomes
    // empty
    while (!q.isEmpty()) {

      Node curr = q.poll();

      // condition to check the
      // occurence of next level
      if (curr == null) {
        if (!q.isEmpty()) {
          q.add(null);
          System.out.println();
        }
      } else {
        // Pushing left child current node
        if (curr.left != null)
          q.add(curr.left);

        // Pushing right child current node
        if (curr.right != null)
          q.add(curr.right);

        System.out.print(curr.data + " ");
      }
    }
  }

  // Driver function
  public static void main(String[] args) {

    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right.right = new Node(6);

    levelOrder(root);
  }
}

// This code is Contributed by Rishabh Jindal
```

## 蟒蛇 3

```
# Python3 program to print levels
# line by line 
from collections import deque as queue

# A Binary Tree Node
class Node:

    def __init__(self, key):

        self.data = key
        self.left = None
        self.right = None

# Function to do level order
# traversal line by line
def levelOrder(root):

    if (root == None):
        return

    # Create an empty queue for
    # level order traversal
    q = queue()

    # To store front element of
    # queue.
    #node *curr

    # Enqueue Root and None node.
    q.append(root)
    q.append(None)

    while (len(q) > 1):
        curr = q.popleft()
        #q.pop()

        # Condition to check
        # occurrence of next
        # level.
        if (curr == None):
           q.append(None)
           print()

        else:

            # Pushing left child of
            # current node.
            if (curr.left):
                q.append(curr.left)

            # Pushing right child of
            # current node.
            if (curr.right):
                q.append(curr.right)

            print(curr.data, end = " ")

# Driver code
if __name__ == '__main__':

    # Let us create binary tree
    # shown above
    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right.right = Node(6)

    levelOrder(root)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to do level order
// traversal line by line
using System;
using System.Collections;

class GFG 
{
public class Node 
{
    public int data;
    public Node left;
    public Node right;

    public Node(int data) 
    {
        this.data = data;
        left = null;
        right = null;
    }
}

// Prints level order traversal line
// by line using two queues.
static void levelOrder(Node root) 
{
    if (root == null)
    return;

    Queue q = new Queue();

    // Pushing root node into the queue.
    q.Enqueue(root);

    // Pushing delimiter into the queue.
    q.Enqueue(null);

    // Executing loop till queue becomes
    // empty
    while (q.Count>0)
    {

        Node curr = (Node)q.Peek();
        q.Dequeue();

        // condition to check the
        // occurence of next level
        if (curr == null) 
        {
            if (q.Count > 0)
            {
                q.Enqueue(null);
                 Console.WriteLine();
            }
        } 
        else 
        {
            // Pushing left child current node
            if (curr.left != null)
            q.Enqueue(curr.left);

            // Pushing right child current node
            if (curr.right != null)
            q.Enqueue(curr.right);

            Console.Write(curr.data + " ");
        }
    }
}

// Driver code
static public void Main(String []args) 
{

    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right.right = new Node(6);

    levelOrder(root);
}
}

// This code is Contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// Javascript program to do level order
// traversal line by line
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

// Prints level order traversal line
// by line using two queues.
function levelOrder(root)
{
    if (root == null)
      return;

    let q= [];

    // Pushing root node into the queue.
    q.push(root);

    // Pushing delimiter into the queue.
    q.push(null);

    // Executing loop till queue becomes
    // empty
    while (q.length!=0) {

      let curr = q.shift();

      // condition to check the
      // occurence of next level
      if (curr == null) {
          if (q.length!=0) {
          q.push(null);
          document.write("<br>");
        }
      } 
      else {
        // Pushing left child current node
        if (curr.left != null)
          q.push(curr.left);

        // Pushing right child current node
        if (curr.right != null)
          q.push(curr.right);

        document.write(curr.data + " ");
      }
    }
}

// Driver function
let root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
root.right.right = new Node(6);

levelOrder(root);

// This code is contributed by patel2127
</script>
```

**输出:**

```
1
2 3
4 5 6
```

**时间复杂度:** O(n)