# 求最深奇数层叶节点的深度

> 原文:[https://www . geesforgeks . org/find-最深奇数层节点深度/](https://www.geeksforgeeks.org/find-depth-of-the-deepest-odd-level-node/)

写一个代码来获取二叉树中最深奇数层叶节点的深度。考虑该级别从 1 开始。叶节点的深度是从根到叶(包括叶和根)的路径上的节点数。
例如，考虑下面的树。最深的奇数层节点是值为 9 的节点，该节点的深度为 5。

```
       1
     /   \
    2     3
  /      /  \  
 4      5    6
        \     \
         7     8
        /       \
       9         10
                 /
                11
```

其思想是递归遍历给定的二叉树，并在遍历时维护一个变量“级别”，该变量将存储树中当前节点的级别。如果当前节点是叶节点，则检查“级别”是否为奇数。如果级别是奇数，那么返回它。如果当前节点不是叶子，则递归地在左右子树中找到最大深度，并返回两个深度中的最大值。

## C++

```
// C++ program to find depth of the
// deepest odd level leaf node
#include <bits/stdc++.h>
using namespace std;

// A utility function to find
// maximum of two integers
int max(int x, int y)
{
    return (x > y)? x : y;
}

// A Binary Tree node
struct Node
{
    int data;
    struct Node *left, *right;
};

// A utility function to allocate a
// new tree node
struct Node* newNode(int data)
{
    struct Node* node = (struct Node*) malloc(sizeof(struct Node));
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

// A recursive function to find depth of
// the deepest odd level leaf
int depthOfOddLeafUtil(struct Node *root,
                               int level)
{
    // Base Case
    if (root == NULL)
        return 0;

    // If this node is a leaf and its level
    // is odd, return its level
    if (root->left == NULL &&
        root->right == NULL && level & 1)
        return level;

    // If not leaf, return the maximum value
    // from left and right subtrees
    return max(depthOfOddLeafUtil(root->left, level + 1),
               depthOfOddLeafUtil(root->right, level + 1));
}

/* Main function which calculates the depth
   of deepest odd level leaf. This function
   mainly uses depthOfOddLeafUtil() */
int depthOfOddLeaf(struct Node *root)
{
    int level = 1, depth = 0;
    return depthOfOddLeafUtil(root, level);
}

// Driver Code
int main()
{
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->right->left = newNode(5);
    root->right->right = newNode(6);
    root->right->left->right = newNode(7);
    root->right->right->right = newNode(8);
    root->right->left->right->left = newNode(9);
    root->right->right->right->right = newNode(10);
    root->right->right->right->right->left = newNode(11);

    cout << depthOfOddLeaf(root)
         << " is the required depth";
    getchar();
    return 0;
}

// This code is contributed
// by Akanksha Rai
```

## C

```
// C program to find depth of the deepest odd level leaf node
#include <stdio.h>
#include <stdlib.h>

// A utility function to find maximum of two integers
int max(int x, int y) { return (x > y)? x : y; }

// A Binary Tree node
struct Node
{
    int data;
    struct Node *left, *right;
};

// A utility function to allocate a new tree node
struct Node* newNode(int data)
{
    struct Node* node = (struct Node*) malloc(sizeof(struct Node));
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

// A recursive function to find depth of the deepest odd level leaf
int depthOfOddLeafUtil(struct Node *root,int level)
{
    // Base Case
    if (root == NULL)
        return 0;

    // If this node is a leaf and its level is odd, return its level
    if (root->left==NULL && root->right==NULL && level&1)
        return level;

    // If not leaf, return the maximum value from left and right subtrees
    return max(depthOfOddLeafUtil(root->left, level+1),
            depthOfOddLeafUtil(root->right, level+1));
}

/* Main function which calculates the depth of deepest odd level leaf.
This function mainly uses depthOfOddLeafUtil() */
int depthOfOddLeaf(struct Node *root)
{
    int level = 1, depth = 0;
    return depthOfOddLeafUtil(root, level);
}

// Driver program to test above functions
int main()
{
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->right->left = newNode(5);
    root->right->right = newNode(6);
    root->right->left->right = newNode(7);
    root->right->right->right = newNode(8);
    root->right->left->right->left = newNode(9);
    root->right->right->right->right = newNode(10);
    root->right->right->right->right->left = newNode(11);

    printf("%d is the required depth\n", depthOfOddLeaf(root));
    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find depth of deepest odd level node

// A binary tree node
class Node
{
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    // A recursive function to find depth of the deepest odd level leaf
    int depthOfOddLeafUtil(Node node, int level)
    {
        // Base Case
        if (node == null)
            return 0;

        // If this node is a leaf and its level is odd, return its level
        if (node.left == null && node.right == null && (level & 1) != 0)
            return level;

        // If not leaf, return the maximum value from left and right subtrees
        return Math.max(depthOfOddLeafUtil(node.left, level + 1),
                depthOfOddLeafUtil(node.right, level + 1));
    }

    /* Main function which calculates the depth of deepest odd level leaf.
       This function mainly uses depthOfOddLeafUtil() */
    int depthOfOddLeaf(Node node)
    {
        int level = 1, depth = 0;
        return depthOfOddLeafUtil(node, level);
    }

    public static void main(String args[])
    {
        int k = 45;
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.right.left = new Node(5);
        tree.root.right.right = new Node(6);
        tree.root.right.left.right = new Node(7);
        tree.root.right.right.right = new Node(8);
        tree.root.right.left.right.left = new Node(9);
        tree.root.right.right.right.right = new Node(10);
        tree.root.right.right.right.right.left = new Node(11);
        System.out.println(tree.depthOfOddLeaf(tree.root) +
                                                   " is the required depth");
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program to find depth of the deepest odd level
# leaf node

# A Binary tree node
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# A recursive function to find depth of the deepest
# odd level leaf node
def depthOfOddLeafUtil(root, level):

    # Base Case
    if root is None:
        return 0

    # If this node is leaf and its level is odd, return
    # its level
    if root.left is None and root.right is None and level&1:
        return level

    # If not leaf, return the maximum value from left
    # and right subtrees
    return (max(depthOfOddLeafUtil(root.left, level+1),
                depthOfOddLeafUtil(root.right, level+1)))

# Main function which calculates the depth of deepest odd
# level leaf .
# This function mainly uses depthOfOddLeafUtil()
def depthOfOddLeaf(root):
    level = 1
    depth = 0
    return depthOfOddLeafUtil(root, level)

# Driver program to test above function
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.right.left = Node(5)
root.right.right = Node(6)
root.right.left.right = Node(7)
root.right.right.right = Node(8)
root.right.left.right.left = Node(9)
root.right.right.right.right = Node(10)
root.right.right.right.right.left= Node(11)

print "%d is the required depth" %(depthOfOddLeaf(root))

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
using System;

// C# program to find depth of deepest odd level node

// A binary tree node
public class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

public class BinaryTree
{
    public Node root;

    // A recursive function to find depth of the deepest odd level leaf
    public virtual int depthOfOddLeafUtil(Node node, int level)
    {
        // Base Case
        if (node == null)
        {
            return 0;
        }

        // If this node is a leaf and its level is odd, return its level
        if (node.left == null && node.right == null && (level & 1) != 0)
        {
            return level;
        }

        // If not leaf, return the maximum value from left and right subtrees
        return Math.Max(depthOfOddLeafUtil(node.left, level + 1),
                        depthOfOddLeafUtil(node.right, level + 1));
    }

    /* Main function which calculates the depth of deepest odd level leaf.
    This function mainly uses depthOfOddLeafUtil() */
    public virtual int depthOfOddLeaf(Node node)
    {
        int level = 1, depth = 0;
        return depthOfOddLeafUtil(node, level);
    }

    public static void Main(string[] args)
    {
        int k = 45;
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.right.left = new Node(5);
        tree.root.right.right = new Node(6);
        tree.root.right.left.right = new Node(7);
        tree.root.right.right.right = new Node(8);
        tree.root.right.left.right.left = new Node(9);
        tree.root.right.right.right.right = new Node(10);
        tree.root.right.right.right.right.left = new Node(11);
        Console.WriteLine(tree.depthOfOddLeaf(tree.root) + " is the required depth");
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program to find depth of
// deepest odd level node

// A binary tree node
class Node {
    constructor(val) {
        this.data = val;
        this.left = null;
        this.right = null;
    }
}

    var root;

    // A recursive function to find depth of the
    // deepest odd level leaf
    function depthOfOddLeafUtil(node , level) {
        // Base Case
        if (node == null)
            return 0;

        // If this node is a leaf and its level is odd,
        // return its level
        if (node.left == null && node.right ==
            null && (level & 1) != 0)
            return level;

        // If not leaf, return the maximum value
        // from left and right subtrees
        return Math.max(depthOfOddLeafUtil(node.left, level + 1),
        depthOfOddLeafUtil(node.right, level + 1));
    }

    /*
     * Main function which calculates the
     depth of deepest odd level leaf. This
     * function mainly uses depthOfOddLeafUtil()
     */
    function depthOfOddLeaf(node) {
        var level = 1, depth = 0;
        return depthOfOddLeafUtil(node, level);
    }

        var k = 45;

        root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.right.left = new Node(5);
        root.right.right = new Node(6);
        root.right.left.right = new Node(7);
        root.right.right.right = new Node(8);
        root.right.left.right.left = new Node(9);
        root.right.right.right.right = new Node(10);
        root.right.right.right.right.left = new Node(11);

        document.write(
        depthOfOddLeaf(root) + " is the required depth"
        );

// This code contributed by Rajput-Ji

</script>
```

**输出:**

```
5 is the required depth
```

**时间复杂度:**函数对树做简单遍历，所以复杂度为 O(n)。
**迭代方法**
这个方法是由[曼德普·辛格](https://github.com/msdeep14)贡献的。以迭代的方式遍历树中的每个级别，每当遇到叶节点时，检查级别是否为奇数，如果级别为奇数，则更新结果。

## C++

```
// CPP program to find
// depth of the deepest
// odd level leaf node
// of binary tree
#include <bits/stdc++.h>
using namespace std;

// tree node
struct Node
{
    int data;
    Node *left, *right;
};

// returns a new
// tree Node
Node* newNode(int data)
{
    Node* temp = new Node();
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// return max odd number
// depth of leaf node
int maxOddLevelDepth(Node* root)
{
    if (!root)
        return 0;

    // create a queue
    // for level order
    // traversal
    queue<Node*> q;
    q.push(root);

    int result = INT_MAX;
    int level = 0;

    // traverse until the
    // queue is empty
    while (!q.empty())
    {
        int size = q.size();
        level += 1;

        // traverse for
        // complete level
        while(size > 0)
        {
            Node* temp = q.front();
            q.pop();

            // check if the node is
            // leaf node and level
            // is odd if level is
            // odd, then update result
            if(!temp->left && !temp->right
                      && (level % 2 != 0))
            {
                result = level;
            }

            // check for left child
            if (temp->left)
            {
                q.push(temp->left);
            }

            // check for right child
            if (temp->right)
            {
                q.push(temp->right);
            }
            size -= 1;
        }
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
    root->right->right->right->right->left = newNode(11);

    int result = maxOddLevelDepth(root);

    if (result == INT_MAX)
        cout << "No leaf node at odd level\n";
    else
        cout << result;
        cout << " is the required depth " << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find depth of the deepest
// odd level leaf node of binary tree
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

// return max odd number depth of leaf node
static int maxOddLevelDepth(Node root)
{
    if (root == null)
        return 0;

    // create a queue for level order
    // traversal
    Queue<Node> q = new LinkedList<>();
    q.add(root);

    int result = Integer.MAX_VALUE;
    int level = 0;

    // traverse until the queue is empty
    while (!q.isEmpty())
    {
        int size = q.size();
        level += 1;

        // traverse for complete level
        while(size > 0)
        {
            Node temp = q.peek();
            q.remove();

            // check if the node is leaf node and
            // level is odd if level is odd,
            // then update result
            if(temp.left == null &&
               temp.right == null && (level % 2 != 0))
            {
                result = level;
            }

            // check for left child
            if (temp.left != null)
            {
                q.add(temp.left);
            }

            // check for right child
            if (temp.right != null)
            {
                q.add(temp.right);
            }
            size -= 1;
        }
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
    root.right.right.right.right.left = newNode(11);

    int result = maxOddLevelDepth(root);

    if (result == Integer.MAX_VALUE)
        System.out.println("No leaf node at odd level");
    else
    {
        System.out.print(result);
        System.out.println(" is the required depth ");
    }
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find depth of the deepest
# odd level leaf node of binary tree

INT_MAX = 2**31

# tree node returns a new tree Node
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# return max odd number depth
# of leaf node
def maxOddLevelDepth(root) :

    if (not root):
        return 0

    # create a queue for level order
    # traversal
    q = []
    q.append(root)

    result = INT_MAX
    level = 0

    # traverse until the queue is empty
    while (len(q)) :

        size = len(q)
        level += 1

        # traverse for complete level
        while(size > 0) :

            temp = q[0]
            q.pop(0)

            # check if the node is leaf node
            # and level is odd if level is
            # odd, then update result
            if(not temp.left and not temp.right
                    and (level % 2 != 0)) :

                result = level

            # check for left child
            if (temp.left) :

                q.append(temp.left)

            # check for right child
            if (temp.right) :

                q.append(temp.right)

            size -= 1

    return result

# Driver Code
if __name__ == '__main__':
    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.right.left = newNode(5)
    root.right.right = newNode(6)
    root.right.left.right = newNode(7)
    root.right.right.right = newNode(8)
    root.right.left.right.left = newNode(9)
    root.right.right.right.right = newNode(10)
    root.right.right.right.right.left = newNode(11)

    result = maxOddLevelDepth(root)
    if (result == INT_MAX) :
        print("No leaf node at odd level")
    else:
        print(result, end = "")
        print(" is the required depth ")

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// C# program to find depth of the deepest
// odd level leaf node of binary tree
using System;
using System.Collections.Generic;

class GFG
{

// tree node
public class Node
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

// return max odd number depth of leaf node
static int maxOddLevelDepth(Node root)
{
    if (root == null)
        return 0;

    // create a queue for level order
    // traversal
    Queue<Node> q = new Queue<Node>();
    q.Enqueue(root);

    int result = int.MaxValue;
    int level = 0;

    // traverse until the queue is empty
    while (q.Count != 0)
    {
        int size = q.Count;
        level += 1;

        // traverse for complete level
        while(size > 0)
        {
            Node temp = q.Peek();
            q.Dequeue();

            // check if the node is leaf node and
            // level is odd if level is odd,
            // then update result
            if(temp.left == null &&
               temp.right == null &&
              (level % 2 != 0))
            {
                result = level;
            }

            // check for left child
            if (temp.left != null)
            {
                q.Enqueue(temp.left);
            }

            // check for right child
            if (temp.right != null)
            {
                q.Enqueue(temp.right);
            }
            size -= 1;
        }
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
    root.right.right.right.right.left = newNode(11);

    int result = maxOddLevelDepth(root);

    if (result == int.MaxValue)
        Console.WriteLine("No leaf node at odd level");
    else
    {
        Console.Write(result);
        Console.WriteLine(" is the required depth ");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

      // JavaScript program to find depth of the deepest
      // odd level leaf node of binary tree
      // tree node
      class Node {
        constructor() {
          this.data = 0;
          this.left = null;
          this.right = null;
        }
      }

      // returns a new tree Node
      function newNode(data) {
        var temp = new Node();
        temp.data = data;
        temp.left = temp.right = null;
        return temp;
      }

      // return max odd number depth of leaf node
      function maxOddLevelDepth(root) {
        if (root == null) return 0;

        // create a queue for level order
        // traversal
        var q = [];
        q.push(root);

        var result = 2147483647;
        var level = 0;

        // traverse until the queue is empty
        while (q.length != 0) {
          var size = q.length;
          level += 1;

          // traverse for complete level
          while (size > 0) {
            var temp = q[0];
            q.shift();

            // check if the node is leaf node and
            // level is odd if level is odd,
            // then update result
            if (temp.left == null && temp.right == null &&
            level % 2 != 0) {
              result = level;
            }

            // check for left child
            if (temp.left != null) {
              q.push(temp.left);
            }

            // check for right child
            if (temp.right != null) {
              q.push(temp.right);
            }
            size -= 1;
          }
        }
        return result;
      }

      // Driver Code
      // construct a tree
      var root = newNode(1);
      root.left = newNode(2);
      root.right = newNode(3);
      root.left.left = newNode(4);
      root.right.left = newNode(5);
      root.right.right = newNode(6);
      root.right.left.right = newNode(7);
      root.right.right.right = newNode(8);
      root.right.left.right.left = newNode(9);
      root.right.right.right.right = newNode(10);
      root.right.right.right.right.left = newNode(11);

      var result = maxOddLevelDepth(root);

      if (result == 2147483647)
      document.write("No leaf node at odd level");
      else {
        document.write(result);
        document.write(" is the required depth");
      }

</script>
```

**输出:**

```
5 is the required depth
```

**时间复杂度:**时间复杂度为 O(n)。

本文由 [**钱德拉·普拉卡什**](https://www.facebook.com/chandra.prakash.52643?fref=ts) 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。